# Registro de Decisões — Monetização

> Decisões de monetização do LineBR Legacy.
> **Cada entrada registra também as tensões e riscos conhecidos** — não para reabrir decisões do Owner, mas porque um Decision Log serve para o leitor de daqui a dois anos entender **o que foi trocado por quê**. Registro que só guarda o lado bom é propaganda, não memória.

---

## Índice
| ID | Descrição | Status |
|----|-----------|:------:|
| [M-001](#m-001--economia-exclusivamente-adena) | Economia exclusivamente Adena | ✅ Decidido |
| [M-002](#m-002--sistema-vip-em-três-tiers) | Sistema VIP em três tiers | ✅ Decidido |
| [M-003](#m-003--warehouse--inventory-expandidos-no-vip) | Warehouse/Inventory expandidos no VIP | ✅ Decidido |
| [M-004](#m-004--auto-loot-exclusivo-do-vip-gold) | Auto Loot exclusivo do VIP Gold | ✅ **Decidido pelo Owner** |
| [M-005](#m-005--marketplace-p2p-venda-só-para-vip) | Marketplace P2P (venda só VIP) | ✅ Decidido |
| [M-006](#m-006--taxas-do-marketplace-como-adena-sink) | Taxas do Marketplace como Adena Sink | 🟡 Recomendado (futuro) |
| [M-007](#m-007--o-projeto-se-paga-ou-é-bancado) | O projeto se paga ou é bancado? | 🔴 **EM ABERTO** |
| [M-008](#m-008--lista-de-features-proibidas) | Lista de features proibidas | ✅ Decidido (imutável) |

---

### M-001 · Economia exclusivamente Adena
| | |
|---|---|
| **Descrição** | Só Adena circula. Sem moeda premium. Sem NPC vendendo itens próprios. Servidor nunca cria itens nem Adena |
| **Motivação** | Defesa estrutural contra inflação artificial e P2W indireto |
| **Alternativas descartadas** | Moeda premium (❌ vira P2W por transitividade); loja de itens do servidor (❌ mata craft/spoil) |
| **Impacto** | 🟢 Muito positivo. É a decisão mais forte de todo o documento |
| **Status** | ✅ Decidido |

### M-002 · Sistema VIP em três tiers
| | |
|---|---|
| **Descrição** | Bronze / Silver / Gold, cumulativos. Ver [VIP_SYSTEM](VIP_SYSTEM.md) |
| **Motivação** | Receita **recorrente** — única fonte previsível sem vender poder |
| **Alternativas descartadas** | Só doação (receita instável); tier único (menos escalável) |
| **Impacto** | Alto — espinha dorsal do modelo |
| **Risco registrado** | Pressão permanente para ampliar benefícios sob aperto financeiro → mitigado por escopo congelado + [FORBIDDEN_FEATURES](../constitution/FORBIDDEN_FEATURES.md) |
| **Status** | ✅ Decidido |

### M-003 · Warehouse / Inventory expandidos no VIP
| | |
|---|---|
| **Descrição** | Bronze expandido → Silver maior → Gold máximo |
| **Motivação** | Conveniência de logística; economiza tempo (menos viagens ao warehouse) |
| **Fato técnico (EV-001)** | Na aCis 409 estes limites são **mecânica de classe**: `MaximumSlotsForNoDwarf = 80` · **`ForDwarf = 100`**; `WarehouseNoDwarf = 100` · **`ForDwarf = 120`** · `Clan = 200`. O **Dwarf tem +20 slots nativos** como vantagem de classe |
| **Tensão registrada** | ⚠️ Se um VIP não-Dwarf superar os slots nativos do Dwarf, a vantagem de classe do Dwarf é **neutralizada por pagamento**. Logística é poder econômico no L2 (transporte de materiais = capacidade de comércio). O documento anterior do projeto ([game-design/MONETIZATION §4](../archive/MONETIZATION_PHILOSOPHY.game-design.superseded.md)) listava "warehouse/inventário maior" como **nunca vender** — esta decisão **supera** aquele item |
| **Mitigação sugerida** | Teto do VIP **≤** limite nativo do Dwarf (ex.: não-Dwarf VIP chega no máximo a 100/120, nunca acima); Dwarf VIP mantém o degrau relativo |
| **Impacto** | Médio — depende inteiramente dos números escolhidos (pendência V-1) |
| **Status** | ✅ Decidido (números em aberto) |

### M-004 · Auto Loot exclusivo do VIP Gold
| | |
|---|---|
| **Descrição** | Auto Loot existe, exclusivo Gold. Coleta Adena, drops comuns, materiais, recipes, parts, equipamentos comuns, itens de farm. **Não** funciona em Raid Boss, Boss, Eventos e drops de Boss |
| **Motivação** | **Aprovada pelo Owner.** Economiza tempo (não substitui o esforço de matar o mob) |
| **Fato técnico (EV-001)** | Auto Loot **existe na aCis 409** como **config global** (`AutoLoot = False` por padrão) + `AutoLootRaid` separado (também `False`). A distinção "farm comum × raid" **coincide** com a arquitetura nativa. Porém, **não há suporte nativo por jogador** → VIP-exclusivo exige **código custom** |
| **Tensões registradas** | ⚠️ (1) **Não é retail** — o Interlude não tinha Auto Loot → é custom ([ADR-003](../adr/ADR-003-retail-first.md) exige enquadramento). (2) **Teste do competidor:** dois jogadores idênticos farmando o mesmo spot — o Gold coleta sem parar, o não-VIP para para lootar → **diferença de Adena/hora**. É vantagem econômica adquirível com dinheiro. (3) A exclusão de Raid/Boss/Eventos **reduz** o impacto competitivo direto, mas não elimina o diferencial de farm |
| **Alternativas não escolhidas** | Auto Loot global para todos (config nativa, `AutoLoot = True` — zero custom, zero P2W, mas zero receita); sem Auto Loot (retail puro) |
| **Impacto** | Alto — é o benefício de maior valor percebido e o de maior tensão com a filosofia |
| **Status** | ✅ **Decidido pelo Owner — não está em discussão** |

### M-005 · Marketplace P2P (venda só para VIP)
| | |
|---|---|
| **Descrição** | Só itens de jogadores; pagamento em Adena; comprador = qualquer um; vendedor = só VIP. Limites: 3/10/20 anúncios; Gold com destaque |
| **Motivação** | Conveniência de comércio + valor para o VIP; nunca injeta itens/Adena |
| **Fato técnico (EV-001)** | **Não existe na aCis 409** (0 arquivos) → custom completo (dados, packets/BBS, SQL, UI) |
| **Tensões registradas** | ⚠️ (1) **Não é retail**. (2) **Vender é privilégio pago** → o VIP participa da economia num canal que o não-VIP não acessa (comprar todos podem; **vender**, não). (3) Todo sistema de troca é **vetor de dupe** — o risco mais grave da economia. (4) Pode **esvaziar Giran** ([WORLD_IMPORTANCE](../design/WORLD_IMPORTANCE.md): "Giran vazia = servidor morto") |
| **Mitigação** | Taxas em Adena (M-006); auditoria anti-dupe obrigatória antes de implementar |
| **Status** | ✅ Decidido |

### M-006 · Taxas do Marketplace como Adena Sink
| | |
|---|---|
| **Descrição** | Taxa de publicação + taxa sobre venda, ambas em Adena |
| **Motivação** | Criar **dreno** de Adena proporcional à atividade econômica |
| **Impacto** | 🟢 Positivo — dos drenos possíveis, é um dos mais eficientes (incide sobre riqueza circulante) |
| **Recomendação técnica** | Nascer **junto** com o Marketplace. Introduzir taxa depois, num mercado acostumado a ser grátis, é politicamente muito mais caro |
| **Status** | 🟡 Recomendado (futuro) — apenas documentado |

### M-007 · O projeto se paga ou é bancado?
| | |
|---|---|
| **Descrição** | O LineBR Legacy precisa de receita, ou o Owner banca porque quer que exista? |
| **Motivação** | Define a **pressão** sobre a política. É a pergunta que precede todas as outras de monetização |
| **Alternativas** | (a) bancado — VIP é bônus, pressão zero; (b) se paga — VIP é essencial, pressão permanente; (c) híbrido |
| **Impacto** | 🔴 Máximo — determina a resistência do projeto no dia em que a conta apertar |
| **Status** | 🔴 **EM ABERTO** (espelha [game-design D-003](../design/DECISION_LOG.md)) |

### M-008 · Lista de features proibidas
| | |
|---|---|
| **Descrição** | Lista permanente do que nunca será vendido ([FORBIDDEN_FEATURES](../constitution/FORBIDDEN_FEATURES.md)) |
| **Motivação** | Decidir a frio o que será testado a quente |
| **Impacto** | 🟢 Máximo — é a espinha dorsal da integridade |
| **Regra** | A lista **só cresce**. Remover item exigiria ADR que supere o ADR-003 e o Princípio Final |
| **Status** | ✅ Decidido (imutável) |

---

## Decisões em aberto
```
M-007 (banca × se paga)  ──▶  pressão sobre o escopo do VIP  ──▶  integridade a longo prazo
```

## Template
```
### M-NNN · <título>
| Descrição | |
| Motivação | |
| Fato técnico | (EV-NNN) |
| Alternativas | |
| Tensões registradas | |
| Impacto | |
| Status | ✅ / 🟡 / 🔴 / ⛔ |
```
