# Movement — Fluxo de Execução (aCis 409)

> Ciclo completo, rastreado no código. Referências `Arquivo:linha` são do commit `55ff8a4e`.

---

## 1. Fluxo principal — clique de movimento do jogador

```
[CLIENTE] jogador clica no chão
   │  MoveBackwardToLocation { targetX/Y/Z, originX/Y/Z, _moveMovement }
   ▼
[1] MoveBackwardToLocation.readImpl()                       (clientpackets/MoveBackwardToLocation.java:34)
   │   _moveMovement: 0 = teclado/setas · 1 = mouse
   │   BufferUnderflow → Config.L2WALKER_PROTECTION → logout (anti-bot)
   ▼
[2] runImpl() — VALIDAÇÕES                                  (:59)
   ├── _moveMovement == 0        → ActionFailed  ❌ (bloqueia teclado)      (:68)
   ├── player.isOutOfControl()   → ActionFailed                              (:75)
   ├── moveSpeed == 0            → ActionFailed + CANT_MOVE_TOO_ENCUMBERED   (:82)
   ├── player.cancelActiveEnchant()                                          (:90)
   ├── _targetZ += player.getCollisionHeight()   (piso → altura da cabeça)   (:93)
   ├── TeleportMode ONE_TIME/FULL_TIME → teleportTo() e retorna (GM)         (:96)
   ├── distância origem→alvo > 9900 → ActionFailed                           (:110)
   └── em barco? → ramo BoatDock (ver §4)                                    (:116)
   ▼
[3] player.getAI().tryToMoveTo(targetLoc, null)             (:125 → PlayableAI.java:392)
   ▼
[4] CreatureMove.maybeMoveToLocation(dest, offset, pathfinding, isShiftPressed)   (CreatureMove.java:433)
   ├── já está em isIn3DRadius(dest, offset) → return false (não move)
   └── !isMovementDisabled() && !isShiftPressed → moveToLocation(...)
   ▼
[5] PlayerMove.moveToLocation(destination, pathfinding)      (PlayerMove.java:111)
   ├── se já havia task → updatePosition(true)   (fecha o movimento anterior)
   ├── _instant = Instant.now()
   ├── _xAccurate/_yAccurate/_zAccurate = posição atual
   ├── _geoPath.clear()
   ├── pathfinding? → calculatePath(...)  ──────────────▶ §2 GeoEngine
   ├── _destination.set(destination)
   ├── getPosition().setHeadingTo(destination)
   ├── registerMoveTask()                ──────────────▶ §3 tick
   └── broadcastPacket(new MoveToLocation(actor, destination))   ▶ CLIENTE + arredores
```

## 2. GeoEngine / pathfinding (`calculatePath`)

```
PlayerMove.calculatePath(ox,oy,oz, tx,ty,tz)                 (PlayerMove.java:419)
   ├── MoveType.FLY?  → GeoEngine.canFlyToTarget(ox,oy,oz, 32, tx,ty,tz) → OK: return null
   ├── senão          → GeoEngine.canMoveToTarget(ox,oy,oz, tx,ty,tz)    → OK: return null (caminho livre)
   ├── MoveType != GROUND → GeoEngine.getValidFlyLocation(ox,oy,oz,32,tx,ty,tz,debug)
   └── GROUND:
        path = GeoEngine.findPath(ox,oy,oz, tx,ty,tz, playable=true, debug)   (GeoEngine.java:1751)
        ├── path.size() < 2 → [CreatureMove] addGeoPathFailCount()  +  getValidLocation(...)   ← fallback
        └── path.size() >= 2 → resetGeoPathFailCount() · _geoPath.addAll(path) · return _geoPath.poll()
```
> `MaxGeopathFailCount = 50` (geoengine.properties) limita falhas consecutivas.
> **Sem arquivos de geodata** (estado atual do LineBR) o pathfinding não opera.

## 3. Tick de movimento (o coração)

```
registerMoveTask()  →  ThreadPool.scheduleAtFixedRate( tick , 100ms , 100ms )    (CreatureMove.java:214)

  ┌── tick (a cada 100 ms) ──────────────────────────────────────────────┐
  │  updatePosition(false)                                               │
  │    ├─ task nulo / ator invisível            → true (fim)             │
  │    ├─ _pawn deixou de ser conhecido         → true (fim)             │
  │    ├─ [PlayerMove] timePassed = Duration.between(_instant, now)      │
  │    ├─ [PlayerMove] _moveTimeStamp++                                  │
  │    ├─ _pawn != null && !firstRun → _destination = _pawn.getPosition()│
  │    ├─ GROUND → _destination.setZ(GeoEngine.getHeight(_destination))  │
  │    ├─ leftDistance = GROUND ? √(dx²+dy²) : √(dx²+dy²+dz²)            │
  │    ├─ passedDistance:                                                │
  │    │    • CreatureMove (NPC): getMoveSpeed() / 10        (tick fixo) │
  │    │    • PlayerMove:  getRealMoveSpeed(_moveTimeStamp<=5)           │
  │    │                    / (1000d / timePassed)      (tempo real)     │
  │    ├─ SWIM/boat/FLY → maxZ = waterZone.getWaterZ() (se afundado >20) │
  │    ├─ passedDistance < leftDistance ?                                │
  │    │    SIM → fraction = passed/left; _xAccurate += dx*fraction …    │
  │    │          nextZ = GeoEngine.getHeight(nextX,nextY,curZ+2*CELL_H) │
  │    │    NÃO → next = _destination (chegou)                           │
  │    ├─ GROUND && !GeoEngine.canMoveToTarget(cur→next)                 │
  │    │        → _blocked = true; return true            (porta/cerca)  │
  │    ├─ _pawn != null → setHeadingTo(nextX,nextY)  (ANTES do setXYZ)   │
  │    ├─ _actor.setXYZ(nextX, nextY, nextZ)          ← POSIÇÃO SERVIDOR │
  │    ├─ _actor.revalidateZone(false)                    ← zonas        │
  │    └─ return (passedDistance >= leftDistance)  ou  chegou ao pawn    │
  │                                                                      │
  │  se updatePosition == true  &&  !moveToNextRoutePoint()              │
  │     └─ ThreadPool.execute:                                           │
  │          cancelMoveTask()                                            │
  │          _actor.revalidateZone(true)                                 │
  │          AI.notifyEvent(ARRIVED)  ou  ARRIVED_BLOCKED (se _blocked)  │
  └──────────────────────────────────────────────────────────────────────┘
```

### Próximo nó do geopath
```
moveToNextRoutePoint()                                       (CreatureMove.java:246)
   ├── task nulo / geoPath vazio → false
   ├── moveSpeed <= 0 || isMovementDisabled() → false
   ├── destination = _geoPath.poll()
   ├── _destination.set(destination) · setHeadingTo(destination)
   └── broadcastPacket(new MoveToLocation(actor, destination))   ▶ novo segmento
```

## 4. Reconciliação cliente ↔ servidor

```
[CLIENTE] envia periodicamente ValidatePosition { x, y, z, heading, boatId }
   ▼
ValidatePosition.runImpl()                                   (clientpackets/ValidatePosition.java:36)
   ├── player nulo / isTeleporting / isInObserverMode → return
   ├── TeleportMode.CAMERA_MODE → setRegion + setXYZ(cliente) e return       (GM)
   ├── player.isFalling(_z) → return          ("evita jumping durante queda")
   ├── em barco: dist = boatPos.distance2D(x,y); dist > 500 → GetOnVehicle (resync)
   └── normal:  dist = GROUND ? distance2D(x,y) : distance3D(x,y,z)
                dist > moveSpeed && !isBoatMovement → sendPacket(ValidateLocation(player))
```
> **Modelo:** o servidor é **autoritativo**. No fluxo normal a posição do cliente **nunca** é adotada — apenas medida. Se o desvio exceder **1 segundo de movimento** (`moveSpeed`), o servidor **corrige o cliente** com `ValidateLocation`.
> Javadoc de `updatePosition` (CreatureMove.java:284-285) confirma: *"the current server position can differ from the current client position… client send regularly a ValidatePosition packet to eventually correct the gap… it's always the server position that is used in range calculation."*

## 5. Follow (perseguir alvo)

```
PlayableAI.tryToFollow(target, isShiftPressed)               (PlayableAI.java:335)
   ▼
maybeStartOffensiveFollow(target, weaponAttackRange)         (CreatureMove.java:393)
   │   totalRadius = attackRange + actor.collisionRadius + target.collisionRadius
   │   (+50 se o ator é Npc e o alvo está se movendo)
   ▼
startOffensiveFollow / startFriendlyFollow  →  followTask a cada 1 s        (:543/:556)
   ▼
[PlayerMove] offensiveFollowTask(target, offset)             (PlayerMove.java:355)
   ├── !knows(target) → AI.tryToIdle()
   ├── já em raio (2D se GROUND, senão 3D) → return
   ├── moveOk = GeoEngine.getValidLocation(actor, target)
   ├── isPathClear = MathUtil.checkIfInRange(offset, target, moveOk, true)
   │      SIM → moveToPawn(target, offset)   → broadcast MoveToPawn
   │      NÃO → moveToLocation(moveOk, false)  (obstáculo: porta fechando)
   └── (friendlyFollowTask: idem, sem o teste de obstáculo)
```

### MoveToPawn vs MoveToLocation
`findPacketToSend()` (CreatureMove.java:479) / `isOnLastPawnMoveGeoPath()` (:468):
- seguindo um pawn **no último trecho do geopath** → **`MoveToPawn`**;
- caso contrário (ainda percorrendo path fixo) → **`MoveToLocation`**.

## 6. Parada de movimento
```
CreatureMove.stop()                                          (CreatureMove.java:452)
   ├── sem _task e sem _followTask → return
   ├── cancelFollowTask() · cancelMoveTask()
   ├── _actor.revalidateZone(true)
   └── broadcastPacket(new StopMove(_actor))     ▶ CLIENTE + arredores
```
Cliente também pode informar bloqueio via `CannotMoveAnymore` / `CannotMoveAnymoreInVehicle`.
Alternância caminhar/correr: `RequestChangeMoveType` → `ChangeMoveType`.

## 7. Ciclo resumido (visão do enunciado)
| Etapa | Onde acontece |
|-------|---------------|
| Cliente envia pacote | `MoveBackwardToLocation` |
| Packet recebido | `readImpl()` → `runImpl()` |
| **Validação** | arrow-key, out-of-control, moveSpeed, 9900, teleport mode, boat |
| **GeoEngine** | `calculatePath` → `canMoveToTarget` / `findPath` / `getValidLocation` |
| **Collision** | `canMoveToTarget` a cada tick (+ `IBlockDynamic` p/ portas) → `_blocked` |
| **Movimentação** | `registerMoveTask` (100 ms) → `updatePosition` → `setXYZ` |
| **Broadcast** | `MoveToLocation` / `MoveToPawn` / `StopMove` |
| **Atualização do mundo** | `revalidateZone()` a cada tick; `setRegion` / knownlist |
| **Resposta ao cliente** | `ValidateLocation` (correção) · `ActionFailed` (recusa) |
