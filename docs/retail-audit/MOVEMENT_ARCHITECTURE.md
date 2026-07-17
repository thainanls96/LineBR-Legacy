# Movement — Arquitetura (aCis 409)

> **Sprint 004 — auditoria read-only.** Nenhum arquivo Java, datapack, SQL ou config foi alterado.
> Base: `source/aCis_gameserver/java` (aCis 409, commit `55ff8a4e`).

---

## 1. Mapa de componentes

```
CLIENTE (L2 Interlude)
   │  MoveBackwardToLocation / ValidatePosition / CannotMoveAnymore / RequestChangeMoveType
   ▼
network/clientpackets ──▶ model/actor/ai/type/*AI  ──▶ model/actor/move/*Move ──▶ geoengine/GeoEngine
   ▲                                                          │                        │
   └──── network/serverpackets (MoveToLocation, MoveToPawn,  │                    pathfinding/PathFinder
         StopMove, ValidateLocation) ◀── broadcastPacket ────┘                    geodata/ABlock…
```

## 2. Classes de movimento (`net.sf.l2j.gameserver.model.actor.move`)

| Classe | Papel |
|--------|-------|
| **`CreatureMove<T extends Creature>`** | **Núcleo genérico.** Estado do movimento, tick, pathfinding, follow. Base de todos. |
| **`PlayerMove extends CreatureMove<Player>`** | Movimento do jogador. Sobrescreve `moveToLocation`, `updatePosition`, `calculatePath`, follows. Adiciona `moveToPawn`. |
| **`SummonMove`** | Movimento de summon/pet. |
| **`BoatMove`** | Movimento de embarcação. |

### Estado interno (CreatureMove)
`_destination` (Location) · `_geoPath` (fila de nós) · `_task` (ScheduledFuture do tick) · `_followTask` · `_pawn` (alvo seguido) · `_offset` · `_xAccurate/_yAccurate` (posição fracionária) · `_blocked` · `_moveTypes` · flags de debug (`_isDebugMove`, `_isDebugPath`).
`PlayerMove` adiciona: `_instant` (Instant), `_moveTimeStamp` (contador de ticks), `_zAccurate`.

### API principal (CreatureMove)
| Método | Linha | Função |
|--------|------:|--------|
| `moveToLocation(Location, boolean pathfinding)` | 136 | Inicia movimento: calcula path, define destino/heading, registra task, **broadcast `MoveToLocation`** |
| `registerMoveTask()` | 214 | **`ThreadPool.scheduleAtFixedRate(..., 100, 100)`** → tick de **100 ms** |
| `cancelMoveTask()` | 237 | Cancela o tick |
| `moveToNextRoutePoint()` | 246 | Avança para o próximo nó do geopath |
| `updatePosition(boolean firstRun)` | 291 | **Coração:** calcula e aplica a nova posição a cada tick |
| `maybeMoveToLocation(loc, offset, pathfinding, isShiftPressed)` | 433 | Entrada da IA; respeita `isShiftPressed` e `isMovementDisabled` |
| `maybeStartOffensiveFollow` / `maybeStartFriendlyFollow` | 393 / 421 | Decide iniciar follow |
| `startOffensiveFollow` / `startFriendlyFollow` | 556 / 543 | Cria follow task (**1 s**) |
| `stop()` | 452 | Cancela tasks, `revalidateZone(true)`, **broadcast `StopMove`** |
| `calculatePath(ox,oy,oz,tx,ty,tz)` | 493 | Pathfinding via GeoEngine |
| `findPacketToSend()` | 479 | Escolhe `MoveToLocation` vs `MoveToPawn` |
| `addGeoPathFailCount` / `resetGeoPathFailCount` | 629+ | Contador de falhas de path (config `MaxGeopathFailCount`) |

## 3. Enums
- **`enums/actors/MoveType`** — `GROUND(0)`, `SWIM(1)`, `FLY(2)`.
- **`enums/MoveDirectionType`** — direção de movimento.

## 4. Packets

### Cliente → Servidor (`network/clientpackets`)
| Packet | Papel |
|--------|-------|
| **`MoveBackwardToLocation`** | **Entrada principal.** targetX/Y/Z + originX/Y/Z + `_moveMovement` (0=teclado, 1=mouse) |
| **`ValidatePosition`** | Reconciliação de posição (x/y/z/heading/boatId) |
| `CannotMoveAnymore` | Cliente informa bloqueio |
| `CannotMoveAnymoreInVehicle` | Idem, em embarcação |
| `RequestChangeMoveType` | Alterna caminhar/correr |
| `RequestMoveToLocationInVehicle` | Movimento dentro de barco |

### Servidor → Cliente (`network/serverpackets`)
`MoveToLocation` · `MoveToPawn` (follow/ataque) · `MoveToLocationInVehicle` · `StopMove` · `StopMoveInVehicle` · `ChangeMoveType` · **`ValidateLocation`** (corrige o cliente) · `GetOnVehicle` (resync em barco) · `ExOrcMove` · `ExServerPrimitive` (debug GM).

## 5. GeoEngine e pathfinding (`gameserver/geoengine`)
| Componente | Papel |
|------------|-------|
| **`GeoEngine`** | Fachada: `canMoveToTarget`, `canFlyToTarget`, `findPath(...,playable,debug)` (linha 1751), `getValidLocation`, `getValidFlyLocation`, `getHeight` |
| **`pathfinding/PathFinder`**, **`pathfinding/Node`** | A* (pesos/heurística configuráveis) |
| **`geodata/`** | `ABlock` (base), `BlockFlat`, `BlockComplex`, `BlockMultilayer`, variantes `*Dynamic`, `BlockNull`, `GeoStructure` (`CELL_HEIGHT` etc.), `IGeoObject`, `IBlockDynamic` (objetos dinâmicos: portas/cercas) |

**Config (`geoengine.properties`):** `GeoDataPath`, `GeoDataType = L2OFF`, `MaxGeopathFailCount = 50`, `PartOfCharacterHeight = 75`, `MaxObstacleHeight = 32`, `MoveWeight = 10`, `MoveWeightDiag = 14`, `ObstacleWeight = 30`, `HeuristicWeight = 12`, `MaxIterations = 10000` + **lista de regiões a carregar**.

> ⚠️ **Estado atual do LineBR:** o runtime preservado roda **sem arquivos de geodata** (lista de regiões removida) → `findPath` indisponível na prática; movimento cai no comportamento sem pathfinding. Ver [ENVIRONMENT_SETUP.md](../ENVIRONMENT_SETUP.md).

## 6. IA envolvida (`model/actor/ai/type`)
| Classe | Ganchos de movimento |
|--------|----------------------|
| `CreatureAI` | `maybeMoveToLocation(loc, 0, true, false)` (L232) |
| `PlayableAI` | **`tryToMoveTo(Location, Boat)`** (L392) ← entrada do packet · **`tryToFollow(Creature, isShiftPressed)`** (L335) · interact `offset 36, pathfinding=false` (L223) |
| `PlayerAI` | ataque → `maybeMoveToPawn(target, physicalAttackRange, shift)` (L188) · skill → `maybeMoveToPawn(target, castRange, shift)` (L261) · signet → `maybeMoveToLocation(loc, castRange, false, shift)` (L248) · `maybeMoveToPawn(target, 100, shift)` (L437) |
| `NpcAI` | `maybeMoveToLocation(...)` (L206/216/661) · interact `offset 36` (L239) |
| `SummonAI` | `tryToFollow(owner, false)` (L263) |

**Eventos de chegada:** `AiEventType.ARRIVED` / `AiEventType.ARRIVED_BLOCKED` (disparados ao fim do tick).

## 7. Velocidade (`model/actor/status`)
- `CreatureStatus.getMoveSpeed()` → `calcStat(Stats.RUN_SPEED, baseMoveSpeed)`.
- **`PlayerStatus.getRealMoveSpeed(boolean isStillWalking)`**:
  `base = isInWater ? baseSwimSpeed : ((isStillWalking || !isRunning) ? baseWalkSpeed : baseRunSpeed)`
  → malus de **SwampZone** (`(100 + zone.getMoveBonus())/100`) → **penalidade de grade de armadura** (`base *= Math.pow(0.84, armorGradePenalty)`) → `calcStat(Stats.RUN_SPEED, ...)`.
- `PetStatus.getMoveSpeed()` — malus de swamp próprio. `BoatStatus.getMoveSpeed()` — velocidade fixa setável.
- Efeitos/funcs: `EffectSilentMove`, `FuncMoveSpeed`.

## 8. Colisão
- **Estática:** `GeoEngine.canMoveToTarget(...)` a cada tick (GROUND).
- **Dinâmica:** `IBlockDynamic`/`IGeoObject` (portas/cercas) — bloqueio detectado no tick → `_blocked = true` → `ARRIVED_BLOCKED`.
- **Raio de colisão:** `getCollisionRadius()` de ator e alvo somados nos cálculos de follow/ataque; `getCollisionHeight()` usado para corrigir o Z alvo.

## 9. Water / Fly / Boat
- **Water (SWIM):** `WaterZone`; se `GeoEngine.getHeight(...) - waterZone.getWaterZ() < -20` → `maxZ = waterZone.getWaterZ()` (clamp). Velocidade usa `baseSwimSpeed`.
- **Fly (FLY):** `canFlyToTarget(ox,oy,oz,32,tx,ty,tz)` / `getValidFlyLocation(...,32,...)`; **único tipo que ignora o check de Z** (junto de barco).
- **Boat:** `BoatMove` + `BoatInfo` + `BoatDock` (pontos de embarque/desembarque, conversão mundo↔barco). Movimento real do jogador é suspenso a bordo ("otherwise GeoEngine will be confused").
