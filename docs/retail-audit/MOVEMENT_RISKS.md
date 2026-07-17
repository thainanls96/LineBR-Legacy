# Movement — Dependências e Riscos (aCis 409)

> Cobre a ETAPA 3 (dependências/acoplamento) e a ETAPA 5 (classificação de risco).

---

## 1. Quem chama quem (grafo de chamadas)

```
clientpackets/MoveBackwardToLocation ──▶ PlayableAI.tryToMoveTo ──▶ CreatureMove.maybeMoveToLocation
clientpackets/ValidatePosition ──▶ (só mede) ──▶ serverpackets/ValidateLocation | GetOnVehicle
PlayerAI (attack/skill/interact) ──▶ PlayerMove.maybeMoveToPawn ──▶ PlayerMove.moveToPawn
NpcAI / SummonAI / CreatureAI ──▶ CreatureMove.maybeMoveToLocation
PlayableAI.tryToFollow ──▶ maybeStartOffensive/FriendlyFollow ──▶ start*Follow ──▶ *followTask (1s)

CreatureMove.moveToLocation ──▶ calculatePath ──▶ GeoEngine.{canMoveToTarget, findPath, getValidLocation}
                            └──▶ registerMoveTask ──▶ ThreadPool.scheduleAtFixedRate(100ms)
                                    └──▶ updatePosition ──▶ GeoEngine.getHeight / canMoveToTarget
                                                        ──▶ Creature.setXYZ ──▶ World/WorldRegion (knownlist)
                                                        ──▶ Creature.revalidateZone ──▶ ZoneManager
                                                        ──▶ broadcastPacket ──▶ MoveToLocation/MoveToPawn
                                    └──▶ (fim) ──▶ AI.notifyEvent(ARRIVED | ARRIVED_BLOCKED)
updatePosition ──▶ CreatureStatus.getMoveSpeed / PlayerStatus.getRealMoveSpeed ──▶ Stats.RUN_SPEED, ZoneId.SWAMP
```

## 2. Quem depende de quem (acoplamento)

| Componente | Depende de | Natureza do acoplamento |
|------------|-----------|--------------------------|
| `CreatureMove` / `PlayerMove` | **GeoEngine**, **ThreadPool**, `World`/`WorldRegion`, `ZoneManager`, `*Status`, serverpackets, `AI` | **Alto** — é o hub do subsistema |
| `*AI` | `CreatureMove` (via `_actor.getMove()`) | Médio — unidirecional (AI → Move) |
| `MoveBackwardToLocation` | `PlayableAI`, `BoatInfo`/`BoatDock`, `MathUtil`, `Config` | Médio |
| `ValidatePosition` | `PlayerMove.getMoveType()`, `PlayerStatus.getMoveSpeed()`, `World` | Baixo (leitura) |
| `GeoEngine` | `geodata/*`, `pathfinding/*`, config | Isolado atrás de fachada |
| `Creature.setXYZ` | `World`, `WorldRegion`, knownlist | **Crítico** — reposiciona no mundo |

**Pontos de acoplamento notáveis**
- **Move ↔ AI bidirecional na prática:** AI chama `maybeMove*`; Move notifica `ARRIVED`/`ARRIVED_BLOCKED` de volta. Mudar a semântica de chegada quebra IA.
- **Move ↔ GeoEngine:** toda decisão de trajeto/Z passa pela fachada. Sem geodata, o comportamento muda drasticamente.
- **Move ↔ ThreadPool:** o tick de 100 ms é agendado no pool global (**ThreadPool é área proibida**).
- **Move ↔ Zone/World:** `revalidateZone` roda **a cada tick** — alterações aqui têm custo multiplicado por (nº de atores em movimento × 10/s).
- **Duplicação Player vs Creature:** `moveToLocation`, `updatePosition` e `calculatePath` estão **reimplementados** em `PlayerMove` (não reaproveitam o pai). Alterar o pai **não** afeta jogadores — armadilha clássica.

## 3. Classes críticas

| Classe | Por quê |
|--------|---------|
| **`CreatureMove`** | Núcleo de todo movimento de NPC/summon/boat |
| **`PlayerMove`** | Núcleo do movimento do jogador (caminho separado!) |
| **`GeoEngine`** | Determina trajeto, Z e colisão de tudo que se move |
| **`Creature.setXYZ`** | Reposiciona o objeto no `World`/região (knownlist, visibilidade) |
| **`ValidatePosition`** | Única barreira contra desync/teleport-hack no cliente |
| **`PlayerStatus.getRealMoveSpeed`** | Define velocidade real (walk/run/swim + malus) |

## 4. Métodos que JAMAIS devem ser alterados sem extremo cuidado

| Método | Risco se alterado |
|--------|-------------------|
| `PlayerMove.updatePosition` / `CreatureMove.updatePosition` | Executa **10×/s por ator em movimento**. Erro = teleporte, tremor, travamento, ou queda de performance global |
| `CreatureMove.registerMoveTask` | Mexer no período (100 ms) altera **toda** a física percebida e a carga do ThreadPool |
| `CreatureMove.calculatePath` / `PlayerMove.calculatePath` | Erro = personagens atravessando parede ou travando |
| `Creature.setXYZ` | Corrompe knownlist/regiões → objetos invisíveis ou fantasma |
| `ValidatePosition.runImpl` | Afrouxar = permitir speed/teleport hack; apertar = "borracha" (rubber-banding) |
| `PlayerStatus.getRealMoveSpeed` | Afeta velocidade de **todos** os jogadores e o cálculo do próprio tick |
| `GeoEngine.canMoveToTarget` / `findPath` | Núcleo de colisão; regressões silenciosas e difíceis de detectar |

## 5. Classificação de risco por componente

| Componente | Risco | Motivo |
|------------|:-----:|--------|
| **`PlayerMove.updatePosition`** | 🔴 **CRÍTICO** | Hot path 10×/s por jogador; define posição autoritativa; qualquer erro é visível e global |
| **`CreatureMove.updatePosition`** | 🔴 **CRÍTICO** | Idem para todos os NPCs (volume muito maior) |
| **`GeoEngine`** (canMoveToTarget/findPath/getHeight) | 🔴 **CRÍTICO** | Colisão e trajeto de tudo; falha = atravessar parede/travar |
| **`Creature.setXYZ` / World / knownlist** | 🔴 **CRÍTICO** | Integridade espacial do mundo |
| **`registerMoveTask` / ThreadPool** | 🔴 **CRÍTICO** | Período do tick = física do jogo + carga global. **Área proibida** |
| **`ValidatePosition`** | 🟠 **ALTO** | Segurança anti-cheat vs conforto do jogador |
| **`calculatePath`** | 🟠 **ALTO** | Pathfinding; efeitos sutis e difíceis de reproduzir |
| **`PlayerStatus.getRealMoveSpeed`** | 🟠 **ALTO** | Velocidade percebida por todos; toca balanceamento |
| **Follow tasks** (`offensive/friendlyFollowTask`) | 🟠 **ALTO** | Combate/PvE dependem; 1 s de granularidade |
| **`MoveBackwardToLocation`** (validações) | 🟡 **MÉDIO** | Porta de entrada; mudanças afetam UX diretamente, mas o escopo é contido |
| **Boat / `BoatMove` / `BoatDock`** | 🟡 **MÉDIO** | Complexo, porém isolado e de uso restrito |
| **`MoveType` / `MoveDirectionType`** | 🟡 **MÉDIO** | Enums usados em ramificações críticas |
| **Packets de movimento** (MoveToLocation/Pawn/StopMove) | 🟡 **MÉDIO** | **Protocolo — área proibida**; erro = dessincronia visual |
| **Flags de debug** (`_isDebugMove`, `_isDebugPath`, `ExServerPrimitive`) | 🟢 **BAIXO** | Só para GM; sem efeito em gameplay |
| **`describeMovementTo`** | 🟢 **BAIXO** | Diagnóstico |
| **`geoPathFailCount`** | 🟢 **BAIXO** | Contador auxiliar |

## 6. Armadilhas identificadas (para quem for mexer no futuro)
1. **Player NÃO usa o código do pai.** `PlayerMove` reimplementa `moveToLocation`/`updatePosition`/`calculatePath`. Corrigir só em `CreatureMove` **não** afeta jogadores (e vice-versa).
2. **Duas matemáticas diferentes.** NPC: `speed/10` (assume tick exato). Player: tempo real (`Instant`) — mais preciso, porém sensível a *jitter* do ThreadPool.
3. **Arredondamento divergente.** `CreatureMove` usa `(int)` (trunca); `PlayerMove` usa `Math.round`. Mesma trajetória → posições ligeiramente distintas.
4. **`revalidateZone` roda a cada tick** — otimizar ali é tentador e perigoso (efeitos em zonas/eventos).
5. **`_destination` é mutado** (`setZ`, `set`) dentro do tick — cuidado com aliasing (é por isso que `clone()` existe em vários pontos).
6. **Sem geodata, `findPath` não opera** — testes de movimento no ambiente atual não exercitam pathfinding real.
