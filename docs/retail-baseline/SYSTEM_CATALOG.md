# Catálogo de Sistemas — LineBR Legacy (Baseline Retail)

> **Catálogo canônico.** Supera o `retail-knowledge-base/SYSTEM_INDEX.md` (que deve ser removido na consolidação).
> Coluna **Existe na aCis 409?** verificada por busca no código/datapack do commit `55ff8a4e` — **não** por suposição.

## Legenda
🔴 **Não auditado** · 🟡 **Em auditoria** · 🟢 **Baseline criada** · 🔵 **Retail validado**

> 🔵 exige evidência **≥ ★★★★** sobre o retail. O projeto **ainda não possui nenhuma** ⇒ **nenhum sistema pode ser 🔵 hoje**.

---

## A. Sessão e personagem
| # | Sistema | Status | Existe na aCis 409? (evidência) |
|:-:|---------|:------:|-------------------------------|
| A01 | Login / Autenticação | 🔴 | ✅ `net.sf.l2j.loginserver` (55 `.java`) |
| A02 | Character Creation | 🔴 | ✅ clientpackets `CharacterCreate` |
| A03 | Character Selection | 🔴 | ✅ `CharSelectInfo` |
| A04 | Character Delete / Restore | 🔴 | ✅ `CharacterDelete`, `CharacterRestore` |
| A05 | Spawn (entrada no mundo) | 🔴 | ✅ `EnterWorld`, `World`/`WorldRegion` |
| A06 | Death | 🔴 | ✅ `Creature.doDie`, `CreatureStatus` |
| A07 | Respawn / Restart Point | 🔴 | ✅ `restartPointAreas.xml` |
| A08 | Resurrection | 🔴 | ✅ handlers de skill + `RequestRestartPoint` |
| A09 | Subclass | 🔴 | ✅ 1 `.java` + datapack |
| A10 | Noblesse | 🔴 | ✅ 2 `.java` |
| A11 | Henna (dyes) | 🔴 | ✅ 17 `.java` |
| A12 | Shortcuts / Macros | 🔴 | ✅ 8 + 6 `.java` |

## B. Espaço e movimento
| # | Sistema | Status | Existe na aCis 409? |
|:-:|---------|:------:|---------------------|
| B01 | **GeoData** | 🔴 | ✅ `geoengine/geodata` (10 `.java`) · ⛔ **arquivos de geodata ausentes no LineBR** |
| B02 | **Pathfinding** | 🔴 | ✅ `geoengine/pathfinding` (`PathFinder`, `Node`) · inoperante sem geodata |
| B03 | **Movement** | 🟡 | ✅ `actor/move` (4 `.java`) — **auditado (Sprint 004)**: [MOVEMENT_*](../retail-audit/) |
| B04 | Collision | 🔴 | ✅ via `GeoEngine.canMoveToTarget` + `IBlockDynamic` |
| B05 | Zones | 🔴 | ✅ `zone/type` (~25 tipos: Peace, Arena, Boss, Water, Swamp, Jail…) |
| B06 | Teleport | 🔴 | ✅ 25 `.java` + `instantTeleports.xml` |
| B07 | Boat | 🔴 | ✅ `BoatMove`, `BoatDock`, `BoatInfo` (parcialmente mapeado na Sprint 004) |

## C. Combate
| # | Sistema | Status | Existe na aCis 409? |
|:-:|---------|:------:|---------------------|
| C01 | Target | 🔴 | ✅ `Action`, target handlers (25) |
| C02 | Attack (fluxo) | 🔴 | ✅ `Creature.doAttack`, `CreatureAttack` |
| C03 | Physical Damage | 🔴 | ✅ `Formulas` |
| C04 | Magic Damage | 🔴 | ✅ `Formulas` |
| C05 | Critical / Hit / Miss / Shield | 🔴 | ✅ `Formulas` |
| C06 | PvP / PK / Karma | 🔴 | ✅ `PlayerPvP`/karma no `Player` |
| C07 | Duel | 🔴 | ✅ `DuelManager` |

## D. Skills e efeitos
| # | Sistema | Status | Existe na aCis 409? |
|:-:|---------|:------:|---------------------|
| D01 | Skill Engine | 🔴 | ✅ `SkillTable`, 74 skill handlers |
| D02 | Cast / Cooldown / Reuse | 🔴 | ✅ `CreatureCast` |
| D03 | Buffs / Debuffs / Abnormals | 🔴 | ✅ `AbnormalEffect`, `EffectList` |
| D04 | Stacking / Slots | 🔴 | ✅ `effects/` + `stackType` |
| D05 | Enchant Skill | 🔴 | ✅ `enchantSkills.xml` (1.7 MB) |

## E. IA e NPCs
| # | Sistema | Status | Existe na aCis 409? |
|:-:|---------|:------:|---------------------|
| E01 | AI (core / Intention / Desires) | 🔴 | ✅ `actor/ai` + `ai/type` |
| E02 | NpcAI | 🔴 | ✅ `NpcAI.java` |
| E03 | Aggro / Hate | 🔴 | ✅ 2 + 5 `.java` |
| E04 | NPC (spawn/respawn/despawn) | 🔴 | ✅ `Spawn`, `Territory`, `SpawnManager` |
| E05 | Raid Boss | 🔴 | ✅ 14 `.java` |
| E06 | Grand Boss | 🔴 | ✅ 2 `.java` + scripts de AI |
| E07 | Walkers / Routes | 🔴 | ✅ `WalkerRoute` |

## F. Quests e conteúdo
| # | Sistema | Status | Existe na aCis 409? |
|:-:|---------|:------:|---------------------|
| F01 | Quest Engine | 🔴 | ✅ `scripting/Quest`, `QuestState` (857 scripts no runtime) |
| F02 | Quest States / Vars | 🔴 | ✅ `QuestState` (⚠️ **não existe** classe `QuestVars` no 409) |
| F03 | Quest Rewards | 🔴 | ✅ via `QuestState` |
| F04 | Seven Signs | 🔴 | ✅ `SevenSignsManager`, `SevenSignsRecords` |
| F05 | Festival (Seven Signs) | 🔴 | ✅ 4 `.java` |
| F06 | **Catacombs / Necropolis** | 🔴 | ⚠️ **Não é sistema Java.** Vive no datapack (22 xml/sql + 40 html) + `SevenSignsManager` + `DungeonGatekeeper`/`DungeonTeleporter` |
| F07 | Derby Track | 🔴 | ✅ eventos no runtime |

## G. Itens e economia
| # | Sistema | Status | Existe na aCis 409? |
|:-:|---------|:------:|---------------------|
| G01 | Items / Inventory | 🔴 | ✅ `itemcontainer` (`ItemContainer`, `Inventory`…) |
| G02 | Equip / Paperdoll | 🔴 | ✅ `Inventory` |
| G03 | Enchant Item | 🔴 | ✅ `RequestEnchantItem` |
| G04 | Augmentation | 🔴 | ✅ `augmentations.sql` |
| G05 | Drops | 🔴 | ✅ `DropData`/`DropCategory` |
| G06 | Spoil | 🔴 | ✅ 4 `.java` |
| G07 | Sweep | 🔴 | ✅ 2 `.java` |
| G08 | Craft / Recipe | 🔴 | ✅ 22 `.java` + `buylists.sql` |
| G09 | Private Store | 🔴 | ✅ 16 `.java` |
| G10 | Trade | 🔴 | ✅ `TradeList` |
| G11 | Warehouse | 🔴 | ✅ 11 `.java` |
| G12 | Auction (clan hall) | 🔴 | ✅ 2 `.java` + `auctions.sql` |
| G13 | Economy (adena/taxas) | 🔴 | ✅ disperso (shops, taxas de castelo) |
| G14 | Manor | 🔴 | ✅ 9 `.java` + `castle_manor_*.sql` |
| G15 | Fishing | 🔴 | ✅ 12 `.java` + `FishingZone` |

## H. Social e grupos
| # | Sistema | Status | Existe na aCis 409? |
|:-:|---------|:------:|---------------------|
| H01 | Party | 🔴 | ✅ `Party` |
| H02 | Command Channel | 🔴 | ✅ 2 `.java` |
| H03 | Party Matching | 🔴 | ✅ 8 `.java` |
| H04 | Friends | 🔴 | ✅ 16 `.java` |
| H05 | Mail | 🔴 | ✅ 4 `.java` + `bbs_mail.sql` |
| H06 | Community Board (BBS) | 🔴 | ✅ `bbs_*` (5 tabelas) + `Pagination` |
| H07 | **Wedding / Couple** | 🔴 | ✅ **existe** — 2 + 9 `.java` (`couples` no runtime) |
| H08 | Clan | 🔴 | ✅ `ClanTable`, `clan_data.sql` |
| H09 | Alliance | 🔴 | ✅ 6 `.java` |
| H10 | Pledge / Clan Skills | 🔴 | ✅ `clan_skills.sql` |

## I. Endgame e territorial
| # | Sistema | Status | Existe na aCis 409? |
|:-:|---------|:------:|---------------------|
| I01 | Castle | 🔴 | ✅ 17 `.java` + `castle*.sql` |
| I02 | Siege | 🔴 | ✅ 20 `.java` |
| I03 | Clan Hall | 🔴 | ✅ `clanhall` (44 registros no seed) |
| I04 | Fortress / Sieges especiais | 🔴 | ✅ agendamentos vistos no runtime |
| I05 | Olympiad | 🔴 | ✅ 21 `.java` + `olympiad_*.sql` |
| I06 | Hero | 🔴 | ✅ 10 `.java` |
| I07 | Cursed Weapon | 🔴 | ✅ 8 `.java` |
| I08 | Rainbow Springs | 🔴 | ✅ `rainbowsprings_attacker_list.sql` |

## J. Companheiros
| # | Sistema | Status | Existe na aCis 409? |
|:-:|---------|:------:|---------------------|
| J01 | Pets | 🔴 | ✅ `PetStatus`, `pets.sql` |
| J02 | Servitors / Summons | 🔴 | ✅ `SummonMove`, `SummonAI` |

## K. Infraestrutura
| # | Sistema | Status | Existe na aCis 409? |
|:-:|---------|:------:|---------------------|
| K01 | Packets / Protocol | 🔴 | ✅ `network/clientpackets` + `serverpackets` ⚠️ sensível |
| K02 | Network (mmocore) | 🔴 | ✅ `commons` (61 `.java`) ⚠️ sensível |
| K03 | ThreadPool | 🔴 | ✅ `commons/pool` ⚠️ sensível (tick de movimento depende) |
| K04 | Database / Persistence | 🔴 | ✅ `ConnectionPool` (65 tabelas) |
| K05 | Admin Commands | 🔴 | ✅ 93 handlers |
| K06 | Events (Derby, Fishing Champ…) | 🔴 | ✅ vistos no runtime |
| K07 | Scripting Engine | 🔴 | ✅ 857 scripts + 6 agendados |

---

## Resumo
| Status | Qtd |
|--------|----:|
| 🔴 Não auditado | 62 |
| 🟡 Em auditoria / auditado | 1 (Movement) |
| 🟢 Baseline criada | **0** |
| 🔵 Retail validado | **0** |

**Total: 63 sistemas catalogados.**

> **Nota metodológica:** "Existe na aCis 409" é fato verificado (★★★★★ **sobre a aCis**). Não diz **nada** sobre o retail — inclusive porque a aCis pode ter sistemas que o retail não tinha, e vice-versa. Confirmar a existência retail de cada sistema é parte do trabalho de baseline.
