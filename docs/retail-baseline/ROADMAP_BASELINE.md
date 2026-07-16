# Roadmap da Baseline — LineBR Legacy

> Ordem oficial de construção da Baseline Retail. Derivada do [DEPENDENCY_MAP](DEPENDENCY_MAP.md).
> **Nenhuma implementação** em nenhuma fase — a Baseline é documental. Implementação só depois, sistema a sistema, pela [CHANGE_ACCEPTANCE_POLICY](../retail-knowledge-base/CHANGE_ACCEPTANCE_POLICY.md).

---

## ⚠️ Fase 00 — Aquisição de Evidência *(pré-requisito absoluto)*
> **Não é auditoria. É o que torna a auditoria capaz de concluir algo sobre o retail.**

| # | Objetivo | Destrava | Ref |
|:-:|----------|----------|-----|
| 00.1 | **Obter geodata Interlude (formato L2OFF)** e habilitar as 139 regiões | GeoData, Pathfinding, Movement, Collision, Combat (LoS), AI | [U-002](UNKNOWN_BEHAVIORS.md) |
| 00.2 | **Obter cliente oficial Interlude** (referência de comportamento observável) | quase todos | U-001 |
| 00.3 | **Obter referência L2OFF/PTS** + montar **captura de pacotes** | escala ★★★★ | U-001 |
| 00.4 | **Recuperar patch notes NCSoft 2007** (Wayback) e arquivar | rates, fórmulas declaradas | U-021 |

**Sem a Fase 00, todo sistema para em 🟢 "Baseline criada" e nenhum chega a 🔵 "Retail validado".**
⚖️ Cautela: material da NCSoft é proprietário — usar como **referência de observação**, nunca redistribuir.

---

## Fase 01 — Fundamento espacial
| Ordem | Sistema | Status | Nota |
|:-----:|---------|:------:|------|
| 1 | **GeoData** (B01) | 🔴 | raiz de tudo; depende de 00.1 para ser auditável de verdade |
| 2 | **Pathfinding** (B02) | 🔴 | depende de GeoData |
| 3 | **Movement** (B03) | 🟡 | **auditado** — revisitar após geodata (conclusões podem mudar) |
| 4 | **Collision** (B04) | 🔴 | |
| 5 | **Zones** (B05) | 🔴 | hot path do movimento |

## Fase 02 — Combate
| Ordem | Sistema | Nota |
|:-----:|---------|------|
| 6 | **Target** (C01) | base de tudo em combate |
| 7 | **Attack** (C02) | fluxo |
| 8 | **Physical Damage** (C03) | `Formulas` |
| 9 | **Magic Damage** (C04) | `Formulas` |
| 10 | **Critical/Hit/Miss/Shield** (C05) | |
| 11 | PvP/PK/Karma (C06) · Duel (C07) | |

## Fase 03 — Skills, IA e NPC
| Ordem | Sistema |
|:-----:|---------|
| 12 | **Skills / Cast / Reuse** (D01, D02) |
| 13 | **Buffs/Debuffs/Abnormals + Stacking** (D03, D04) |
| 14 | **AI (core/Intention)** (E01) |
| 15 | **Aggro / Hate** (E03) |
| 16 | **NpcAI** (E02) · **NPC spawn/respawn** (E04) |
| 17 | Enchant Skill (D05) |

## Fase 04 — Economia
| Ordem | Sistema |
|:-----:|---------|
| 18 | **Drops** (G05) |
| 19 | **Spoil** (G06) · **Sweep** (G07) |
| 20 | **Items / Inventory / Equip** (G01, G02) |
| 21 | **Craft / Recipe** (G08) |
| 22 | **Trade / Private Store / Warehouse** (G09–G11) |
| 23 | **Economy** (G13) — consolidação |
| 24 | Enchant Item (G03) · Augmentation (G04) |

## Fase 05 — Personagem e sessão
| Ordem | Sistema |
|:-----:|---------|
| 25 | Login (A01) · Character Create/Select/Delete (A02–A04) |
| 26 | Spawn / Death / Respawn / Resurrection (A05–A08) |
| 27 | Subclass (A09) · Noblesse (A10) · Henna (A11) |
| 28 | Teleport (B06) |

## Fase 06 — Conteúdo
| Ordem | Sistema |
|:-----:|---------|
| 29 | **Quest Engine / States / Rewards** (F01–F03) |
| 30 | **Seven Signs** (F04) · Festival (F05) · Catacombs/Necropolis (F06) |
| 31 | Raid Boss (E05) · Grand Boss (E06) |
| 32 | Manor (G14) · Fishing (G15) |

## Fase 07 — Social e territorial
| Ordem | Sistema |
|:-----:|---------|
| 33 | Party (H01) · Command Channel (H02) · Party Matching (H03) |
| 34 | Clan (H08) · Alliance (H09) · Clan Skills (H10) |
| 35 | **Castle** (I01) · **Siege** (I02) · Clan Hall (I03) · Fortress (I04) |
| 36 | Pets (J01) · Servitors (J02) |

## Fase 08 — Endgame
| Ordem | Sistema |
|:-----:|---------|
| 37 | **Olympiad** (I05) → **Hero** (I06) |
| 38 | Cursed Weapon (I07) · Rainbow Springs (I08) |

## Fase 09 — Periféricos e infra
| Ordem | Sistema |
|:-----:|---------|
| 39 | Friends (H04) · Mail (H05) · BBS (H06) · Wedding (H07) · Macros/Shortcuts (A12) |
| 40 | Boat (B07) · Events (K06) · Derby (F07) · Auction (G12) |
| 41 | ⚠️ Packets (K01) · Network (K02) · ThreadPool (K03) — **por último**, áreas sensíveis |
| 42 | Admin Commands (K05) · Database (K04) · Scripting (K07) |

---

## Trilha paralela (sem dependência da cadeia crítica)
Podem ser auditados a qualquer momento por quem tiver tempo ocioso, sem bloquear a cadeia:
`Friends` · `Mail` · `BBS` · `Macros/Shortcuts` · `Party Matching` · `Auction` · `Wedding` · `Admin Commands`

## Critério de conclusão de cada sistema
1. Documento pelo [SYSTEM_TEMPLATE](SYSTEM_TEMPLATE.md) completo (sem seção vazia)
2. Diferenças com ★ e `EV-NNN`
3. Incógnitas em [UNKNOWN_BEHAVIORS](UNKNOWN_BEHAVIORS.md); hipóteses em [RETAIL_ASSUMPTIONS](RETAIL_ASSUMPTIONS.md)
4. [SYSTEM_CATALOG](SYSTEM_CATALOG.md) → 🟢 (ou 🔵 se houver evidência ★★★★+)
5. Commit `docs(baseline): <sistema>`

## Estimativa honesta
63 sistemas · 1 auditado. Nas fases 01–09 há **~40 auditorias substanciais**. Com a profundidade da Sprint 004 (real, com `arquivo:linha`), isso é **trabalho de muitos meses**. A Baseline é um ativo de **anos**, não de semanas — e é exatamente por isso que ela precisa ser construída **na ordem certa**, uma vez só.
