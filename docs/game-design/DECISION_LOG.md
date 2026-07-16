# Registro de Decisões de Design — LineBR Legacy

> Toda decisão de **game design** vive aqui. (Decisões de **arquitetura** vivem em [`docs/ADR/`](../ADR/).)
> Decisões **em aberto** são tão importantes quanto as fechadas — e são declaradas como tal.

---

## Índice
| ID | Descrição | Status |
|----|-----------|:------:|
| [D-001](#d-001--rates-do-servidor-x1-retail-vs-mid-rate) | Rates do servidor (x1 vs mid) | 🔴 **EM ABERTO — bloqueia tudo** |
| [D-002](#d-002--modelo-de-monetização) | Modelo de monetização | 🔴 **EM ABERTO** |
| [D-003](#d-003--o-projeto-se-paga-ou-é-bancado) | O projeto se paga ou é bancado? | 🔴 **EM ABERTO** |
| [D-004](#d-004--escopo-do-game-design-bible) | Escopo do Game Design Bible | ✅ Decidido |
| [D-005](#d-005--seven-signs-mantido) | Seven Signs mantido | ✅ Decidido |
| [D-006](#d-006--sem-buffer-npc-gratuito) | Sem buffer NPC gratuito | 🟡 Proposto |
| [D-007](#d-007--população-alvo) | População-alvo | 🔴 **EM ABERTO** |

---

### D-001 · Rates do servidor (x1 retail vs mid-rate)
| | |
|---|---|
| **Descrição** | Definir as rates de XP/SP/Adena/Drop/Spoil/Quest do LineBR Legacy |
| **Fato verificado** | **EV-001/EV-002:** source oficial **e** runtime Base Zero estão em **x1** (`RateXp=1.`, `RateSp=1.`, `RateDropCurrency=1.`, `RateDropItems=1.`, `RateDropSpoil=1.`). As rates mid (x20/x10/x5) eram do **antigo LineBR customizado da VPS** — base diferente, não a nossa |
| **Motivação** | Determina **toda** a economia, progressão, jornada e vida social. Não é "uma config" — é a identidade do servidor |
| **Alternativas** | **(a) x1 retail puro** — máxima fidelidade; jornada de meses; craft/spoil/Dwarf plenos; ⚠️ risco altíssimo de esvaziar na faixa 52–61 com pouca população. **(b) Mid-rate** — retenção maior; ⚠️ quebra o encadeamento XP→drop→craft→enchant, esvazia regiões, fere Retail First frontalmente. **(c) x1 com ajustes pontuais documentados** — meio-termo; ⚠️ meio-termos em economia costumam juntar as desvantagens dos dois |
| **Impacto** | 🔴 **Máximo.** [ECONOMY](ECONOMY_PHILOSOPHY.md), [PROGRESSION](PROGRESSION_PHILOSOPHY.md), [PLAYER_JOURNEY](PLAYER_JOURNEY.md) e [SOCIAL](SOCIAL_PHILOSOPHY.md) **não podem ser finalizados** sem esta decisão |
| **Status** | 🔴 **EM ABERTO** |
| **Nota** | Mid-rate **contradiz** o [ADR-003](../ADR/ADR-003-retail-first.md) e a filosofia declarada. Se for a escolha, exige ADR próprio assumindo que o projeto **não** é Retail First puro — o que é legítimo, mas precisa ser dito em voz alta, não decidido por omissão |

### D-002 · Modelo de monetização
| | |
|---|---|
| **Descrição** | Como (e se) o servidor gera receita |
| **Motivação** | Sustentabilidade sem P2W ([P-11](DESIGN_PRINCIPLES.md)) |
| **Alternativas** | doação pura · doação + cosmético · clube cosmético recorrente · (proibido: qualquer coisa com poder) |
| **Impacto** | Alto — define confiança da comunidade |
| **Status** | 🔴 **EM ABERTO** → [MONETIZATION_PHILOSOPHY](MONETIZATION_PHILOSOPHY.md) |
| **Depende de** | D-003 |

### D-003 · O projeto se paga ou é bancado?
| | |
|---|---|
| **Descrição** | O LineBR Legacy **precisa** de receita, ou o dono banca porque quer que exista? |
| **Motivação** | É a pergunta que **precede** D-002. Sem ela, monetização vira improviso sob pressão |
| **Alternativas** | (a) bancado (custo baixo, liberdade total, sem pressão de P2W) · (b) se paga (exige monetização, cria pressão permanente) · (c) híbrido (bancado + doação) |
| **Impacto** | Alto — define a resistência do projeto no dia em que a conta apertar |
| **Status** | 🔴 **EM ABERTO** |

### D-004 · Escopo do Game Design Bible
| | |
|---|---|
| **Descrição** | O Bible **não** desenha o jogo — o design é o da NCSoft (Retail First) |
| **Motivação** | Um "Game Design Bible" num projeto de restauração conflita com Retail First se tentar criar design |
| **Alternativas descartadas** | Bible como autoridade de design criativo (❌ viraria licença para custom) |
| **Impacto** | Estrutural — evita que os próprios documentos justifiquem violar o ADR-003 |
| **Status** | ✅ **Decidido** — o Bible explicita intenção, documenta entendimento e decide o que o retail não dita |

### D-005 · Seven Signs mantido
| | |
|---|---|
| **Descrição** | Seven Signs permanece ativo, mesmo dando trabalho |
| **Motivação** | Pilar de identidade do Interlude; transforma farm em política coletiva |
| **Alternativas descartadas** | Desligar "por simplicidade" (❌ prática comum em privados, perde pilar) |
| **Impacto** | Médio-alto (conteúdo 55+, Catacombs/Necropolis, economia coletiva) |
| **Status** | ✅ **Decidido** (Retail First — não havia o que decidir, na verdade) |

### D-006 · Sem buffer NPC gratuito
| | |
|---|---|
| **Descrição** | Não haverá NPC buffer completo/gratuito |
| **Motivação** | Mata a classe de suporte e a interdependência social ([SOCIAL §1](SOCIAL_PHILOSOPHY.md)) |
| **Alternativas** | (a) nenhum buffer (retail) · (b) buffer limitado pago (custom) · (c) buffer completo (❌) |
| **Impacto** | Alto no jogo social |
| **Status** | 🟡 **Proposto** — decorre do Retail First; formalizar se houver pressão contrária |

### D-007 · População-alvo
| | |
|---|---|
| **Descrição** | O servidor assume ser pequeno/nicho ou busca massa? |
| **Motivação** | O Interlude foi desenhado para milhares. Com 30–50 jogadores, party/mercado/siege/Olympiad não funcionam — e é daí que nasce a pressão por mid-rate e P2W |
| **Alternativas** | (a) nicho assumido (x1 puro, comunidade pequena e fiel) · (b) buscar massa (pressão por facilitar) |
| **Impacto** | 🔴 **Máximo** — é a causa-raiz de D-001 e D-002 |
| **Status** | 🔴 **EM ABERTO** |

---

## Decisões em aberto que **bloqueiam** o design
```
D-007 (população-alvo)  ──┬──▶  D-001 (rates)  ──▶  Economia · Progressão · Jornada · Social
                          └──▶  D-003 (banca?) ──▶  D-002 (monetização)
```
> **D-007 é a raiz.** Responder "para quem é este servidor?" resolve, por consequência, rates e monetização. Decidir rates antes de saber a população-alvo é escolher a resposta antes da pergunta.

## Template
```
### D-NNN · <título>
| Descrição | |
| Motivação | |
| Alternativas | (a) … (b) … |
| Impacto | |
| Status | 🔴 aberto / 🟡 proposto / ✅ decidido / ⛔ descartado |
| Depende de | |
```
