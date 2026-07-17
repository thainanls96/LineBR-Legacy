# Decisões Pendentes — LineBR Legacy

> 🔴 **PENDENTE DE DECISÃO DO OWNER.** Nada aqui pode ser assumido nem implementado.

---

## Bloqueadores técnicos (impedem o servidor de funcionar como Interlude)

### OD-01 · Geodata 🔴🔴 **CRÍTICO**
| | |
|---|---|
| **Questão** | Obter e habilitar a geodata Interlude (formato L2OFF)? |
| **Situação** | 📌 A aCis lê `GeoDataType = L2OFF`, mas **os arquivos não existem** no LineBR. As 139 regiões foram removidas da config para o servidor subir |
| **Impacto** | 🔴 **Sem geodata não há pathfinding nem colisão de terreno.** PvP, PvE, AI e movimento **não se comportam como Interlude** |
| **Ref** | [UNKNOWN_BEHAVIORS U-002](../knowledge/baseline/UNKNOWN_BEHAVIORS.md) · [ROADMAP_BASELINE Fase 00](../knowledge/baseline/ROADMAP_BASELINE.md) |

---

## Gameplay

### OD-02 · NPC Buffer — até qual level?
| | |
|---|---|
| **Questão** | O buffer gratuito atende até que level? |
| **Situação** | ✅ Buffer aprovado (O-34). 📌 aCis tem buffer nativo (`SchemeBuffer`) |
| **Impacto** | Quanto mais alto o level, maior o dano ao Buffer humano e à interdependência ([SOCIAL_SYSTEMS](SOCIAL_SYSTEMS.md)) |

### OD-03 · Teleport gratuito
| | |
|---|---|
| **Questão** | Haverá teleport gratuito? Para quem, até que level? |
| **Situação** | ✅ Teleport Retail aprovado (O-33) |
| **Impacto** | Teleport barato encolhe o mundo ([P-10](../constitution/DESIGN_PRINCIPLES.md)) |

### OD-04 · Dual Box
| | |
|---|---|
| **Questão** | Permitido? Quantas janelas? Restrito em Olympiad/Siege? |
| **Impacto** | Afeta PvP, Olympiad, economia e o jogo social |
| **Nota** | 📌 A aCis 409 possui `dualbox` (auditoria antiga registrou `DualboxManager` na base customizada da VPS; **na aCis 409 limpa é preciso verificar**) |

### OD-05 · Safe Enchant
| | |
|---|---|
| **Questão** | Qual o nível de safe enchant? |
| **Impacto** | Define o maior **dreno de Adena** do jogo ([ECONOMY](ECONOMY.md)) |

### OD-06 · Enchant máximo
| | |
|---|---|
| **Questão** | Há teto de enchant? Qual? |
| **Impacto** | Define o topo de poder e a escassez de itens |

### OD-07 · Eventos
| | |
|---|---|
| **Questão** | Quais eventos existirão? |
| **Restrição** | ❌ Nenhum evento pode **criar itens ou Adena** (E-7/E-8) |

### OD-08 · Horários
| | |
|---|---|
| **Questão** | Horários de Siege, Olympiad, Seven Signs, raids, eventos |
| **Impacto** | Define o ritmo semanal e o público (fuso BR) |

---

## Customs — pendências de viabilização

### OD-09 · Hero Dynasty Skin — como viabilizar? ⚠️
| | |
|---|---|
| **Questão** | O Dynasty **não existe** no Interlude. Como exibir a skin? |
| **Situação** | 📌 **FATO (EV-001):** "dynasty" = **0 arquivos** em xml/java/html. Topo do Interlude = `draconic`, `imperial crusader`, `major arcana`. Dynasty é de chronicle **posterior** |
| **Consequência** | O **cliente Interlude do jogador provavelmente não possui o modelo 3D** do Dynasty → a skin não renderizaria |
| **Alternativas** | (a) **patch de cliente obrigatório** para todos os jogadores; (b) usar um set **existente no cliente Interlude** como skin de Hero; (c) revisar a decisão |
| **Status** | 🔴 **PENDENTE** — a decisão cosmética está aprovada (O-92..O-94); falta decidir **como** viabilizá-la |

### OD-10 · VIP — números e preços
Warehouse/inventory por tier · preços · duração/renovação · "mais alterações visuais" (Silver) · escopo congelado.
⚠️ **Mitigação sugerida (M-003):** teto do VIP **≤** limite nativo do Dwarf (📌 `Dwarf = 100` slots / `120` warehouse), preservando a vantagem de classe.

### OD-11 · Taxas do Marketplace — valores
✅ Taxa aprovada (O-29). 🔴 Valores não definidos. **Recomendação:** nascer junto com o Marketplace.

---

## Negócio

### OD-12 · O projeto se paga ou é bancado? 🔴
| | |
|---|---|
| **Questão** | O LineBR Legacy precisa de receita, ou o Owner banca porque quer que exista? |
| **Impacto** | Define a **pressão** sobre a política de monetização — e a resistência do projeto no dia em que a conta apertar |
| **Ref** | [monetization/DECISION_LOG M-007](../monetization/DECISION_LOG.md) · [game-design/DECISION_LOG D-003](../design/DECISION_LOG.md) |

### OD-13 · População-alvo
| | |
|---|---|
| **Questão** | O servidor assume ser nicho ou busca massa? |
| **Impacto** | É a causa-raiz da pressão por facilitar. O Interlude foi desenhado para milhares |
| **Nota** | As rates aprovadas (O-10/O-11) já respondem **parcialmente**: arranque facilitado + topo endurecido = servidor para quem quer ficar |

---

## Operação

### OD-14 · Política de punição
Aviso/ban/duração para bot, walker, exploit, dupe, RMT.

### OD-15 · Detecção de bot/walker
Método. 📌 A aCis tem `L2WALKER_PROTECTION` nativo.

### OD-16 · Processo de denúncia
Como jogadores reportam.

---

## Resumo
| Categoria | Pendências |
|-----------|-----------:|
| 🔴 Bloqueador crítico | 1 (**Geodata**) |
| Gameplay | 7 |
| Customs | 3 |
| Negócio | 2 |
| Operação | 3 |
| **Total** | **16** |

> **Prioridade sugerida:** **OD-01 (Geodata)** antes de tudo — sem ela, nenhuma decisão de gameplay pode ser validada, porque o servidor não se comporta como Interlude.
