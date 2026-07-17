# Mapa de Dependências entre Sistemas — LineBR Legacy

> Define **qual sistema deve ser auditado primeiro**. Derivado da arquitetura real da aCis 409 (EV-001/EV-003).
> Regra: **auditar um sistema antes de suas dependências produz baseline sobre areia.**

---

## 1. Camadas (de baixo para cima)

```
┌─ L5 · CONTEÚDO ─────────────────────────────────────────────────┐
│  Quests · Seven Signs/Festival · Manor · Castle/Siege           │
│  Olympiad → Hero · Raid/Grand Boss · Events · Wedding           │
└───────────────────────────▲─────────────────────────────────────┘
┌─ L4 · ECONOMIA E SOCIAL ──┴─────────────────────────────────────┐
│  Drops → Spoil/Sweep · Craft/Recipe · Trade/Store/Warehouse     │
│  Economy · Clan/Alliance · Party/CC · Fishing · Pets/Summons    │
└───────────────────────────▲─────────────────────────────────────┘
┌─ L3 · JOGABILIDADE ───────┴─────────────────────────────────────┐
│  Skills (cast/buffs/abnormals) · AI · Aggro/Hate · NPC          │
└───────────────────────────▲─────────────────────────────────────┘
┌─ L2 · COMBATE ────────────┴─────────────────────────────────────┐
│  Target · Attack · Physical/Magic Damage · Formulas             │
└───────────────────────────▲─────────────────────────────────────┘
┌─ L1 · ESPAÇO ─────────────┴─────────────────────────────────────┐
│  GeoData → Pathfinding → Movement → Collision · Zones           │
└───────────────────────────▲─────────────────────────────────────┘
┌─ L0 · INFRAESTRUTURA ─────┴─────────────────────────────────────┐
│  Network/mmocore · Packets · ThreadPool · Database · World      │
└─────────────────────────────────────────────────────────────────┘
```

## 2. Cadeia crítica (a ordem que importa)

```
GeoData ──▶ Pathfinding ──▶ Movement ──▶ Target ──▶ Combat ──▶ Skills ──▶ AI/Aggro
   │                            │                       │          │         │
   └────────── Collision ───────┘                       └──────────┴────▶ NPC/Boss
                                                                            │
                                              Drops ◀───────────────────────┘
                                                │
                                    Spoil/Sweep · Craft · Economy
                                                │
                              Quests · Manor · Castle/Siege · Olympiad ──▶ Hero
```

## 3. Dependências detalhadas

| Sistema | **Depende de** | **É usado por** | Nota |
|---------|----------------|-----------------|------|
| **GeoData** (B01) | Database, arquivos de geodata | Pathfinding, Movement, Collision, Combat (LoS), AI | ⛔ **raiz de tudo no espaço** |
| **Pathfinding** (B02) | GeoData | Movement, AI | inoperante sem geodata |
| **Movement** (B03) | GeoData, Pathfinding, ThreadPool, Zones, World | AI, Combat, NPC, Boat, Pets/Summons | 🟡 auditado |
| **Collision** (B04) | GeoData | Movement, Combat | |
| **Zones** (B05) | World | Movement (`revalidateZone` no tick), Combat, Castle, Events | hot path |
| **Target** (C01) | World/knownlist, Zones | Attack, Skills | |
| **Attack/Damage** (C02–C05) | Target, Movement (alcance), Formulas, Stats | Skills, AI, Drops | |
| **Skills** (D01–D05) | Combat, Stats, Effects | AI, Olympiad, Clan | |
| **AI / Aggro** (E01–E03) | Movement, Combat, Skills | NPC, Raid/Grand Boss | acoplado a Movement (`ARRIVED`/`ARRIVED_BLOCKED`) |
| **NPC** (E04) | AI, Movement, Spawn/Territory | Drops, Quests, Bosses | |
| **Drops** (G05) | NPC, Combat (kill), Items | Spoil, Sweep, Economy | |
| **Spoil/Sweep** (G06/G07) | Drops, Skills | Economy, Craft | |
| **Craft/Recipe** (G08) | Items, Economy | Manor, Economy | |
| **Economy** (G13) | Drops, Craft, Trade, Stores | Castle (taxas), Manor, Clan | pilar do Manifesto |
| **Quests** (F01–F03) | NPC, Items, Economy, Scripting | Seven Signs, conteúdo | 857 scripts |
| **Seven Signs** (F04–F06) | Quests, NPC, Zones, Teleport | Festival, Catacombs/Necropolis | Catacombs = datapack, não sistema |
| **Castle/Siege** (I01–I02) | Clan, Combat, Zones, NPC | Manor, Economy | |
| **Olympiad** (I05) | Combat, Skills, Zones | Hero | |
| **Hero** (I06) | Olympiad | Clan, Cursed Weapon | |
| **Pets/Summons** (J01/J02) | Movement, AI, Combat, Items | — | `SummonMove`, `PetStatus` |
| **Packets/Network/ThreadPool** (K01–K03) | — | **tudo** | ⚠️ áreas sensíveis |

## 4. Acoplamentos perigosos (mapeados)

| Acoplamento | Risco | Origem |
|-------------|:-----:|--------|
| Movement ↔ AI (bidirecional: `maybeMove*` ↔ `ARRIVED`) | 🔴 | Sprint 004 |
| Movement → ThreadPool (tick 100 ms no pool global) | 🔴 | ⚠️ ThreadPool é área sensível |
| Movement → Zones (`revalidateZone` a cada tick) | 🟠 | custo × 10/s × atores |
| Tudo → GeoData (LoS, Z, colisão) | 🔴 | raiz |
| `PlayerMove` **não herda** de `CreatureMove` na prática (reimplementa) | 🟠 | armadilha: corrigir um não corrige o outro |

## 5. Consequência para a ordem de auditoria

**GeoData é a raiz.** Auditar Movement (feito), Combat, AI ou NPC sem geodata significa documentar um sistema que **não está operando como projetado** — parte das conclusões seria inválida quando a geodata entrar.

➡️ Por isso o [ROADMAP_BASELINE](ROADMAP_BASELINE.md) começa por **obter evidência/dados** (Fase 00) e por **GeoData** (Fase 01), e não por sistemas "mais interessantes" como Combat ou Skills.

## 6. Sistemas independentes (podem ser auditados em paralelo)
Sem dependência da cadeia crítica — bons candidatos para trabalho paralelo:
`Friends` (H04) · `Mail` (H05) · `Community Board` (H06) · `Macros/Shortcuts` (A12) · `Party Matching` (H03) · `Auction` (G12) · `Wedding/Couple` (H07) · `Admin Commands` (K05)
