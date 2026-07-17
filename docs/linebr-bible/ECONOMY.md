# Economia — LineBR Legacy

> ✅ Decisões aprovadas pelo Owner.

---

## Rates econômicas — APROVADO

| Item | Rate |
|------|:----:|
| **Adena** | **1x** |
| **Drop** | **1x** |
| **Spoil** | **1x** |
| **Craft** | **100%** |
| **Quest** | **Retail** |

📌 **FATO (EV-001):** estes valores **coincidem com as rates nativas** da aCis 409 (`RateDropCurrency = 1.`, `RateDropItems = 1.`, `RateDropSpoil = 1.`, `RateQuestReward = 1.`). **Zero custom necessário** para a economia.

> **Registro técnico:** manter a economia em 1x enquanto a XP é acelerada é a decisão que **protege a cadeia econômica do Interlude** (drop → spoil → craft → Dwarf → mercado). É o que separa este servidor de um "mid-rate" — aqui o jogador ganha **tempo**, nunca **riqueza**.

## Regras estruturais — APROVADO

| # | Regra |
|:-:|-------|
| E-1 | A economia utiliza **exclusivamente Adena** |
| E-2 | **Nenhuma moeda premium circula no jogo** |
| E-3 | **Nenhuma moeda substitui Adena** |
| E-4 | **Nenhum NPC vende itens próprios** |
| E-5 | O **Marketplace apenas conecta jogadores** |
| E-6 | **Todo item existente veio de algum jogador** |
| E-7 | **O servidor NUNCA cria itens** |
| E-8 | **O servidor NUNCA cria Adena** |

## Marketplace

| Regra | Valor |
|-------|-------|
| Localização | **Giran** ([QUESTS_AND_WORLD](QUESTS_AND_WORLD.md)) |
| Pagamento | **Apenas Adena** |
| Itens | **Somente de jogadores** — servidor nunca vende, nunca cria |
| Comprador | Qualquer jogador |
| Vendedor | **Somente VIP** ([SERVER_SERVICES](SERVER_SERVICES.md)) |
| Anúncios | Bronze 3 · Silver 10 · Gold 20 (Gold com destaque) |

### Taxa do Marketplace
✅ **DECISÃO APROVADA PARA IMPLEMENTAÇÃO FUTURA.**
- Taxa de publicação em Adena
- Taxa sobre venda em Adena
- **Objetivo:** funcionar como **Adena Sink**
- **Valores:** 🔴 **não definidos** → [OPEN_DECISIONS](OPEN_DECISIONS.md)

📌 **FATO (EV-001):** Marketplace **não existe** na aCis 409 (0 arquivos) → ⚠️ **custom completo**.

## Adena Sinks (drenos)
Fontes de saída de Adena da economia:
- Compra em NPC (shots, potions, flechas) — dreno contínuo
- Craft (materiais, taxas)
- **Enchant** (scrolls + destruição de item) — o maior dreno do jogo
- Teleport (retail)
- Taxas de castelo
- **Taxa do Marketplace** (aprovada, futura)

## Proteção anti-inflação
A defesa estrutural são as regras **E-7 e E-8**: o servidor **nunca cria itens nem Adena**. Não há injeção externa de valor. Tudo que circula foi produzido no mundo, por jogadores, jogando.

## Proibido
Ver [SERVER_RULES](SERVER_RULES.md): RMT, compra/venda de Adena, dupes, exploits.
Ver [CUSTOM_SYSTEMS](CUSTOM_SYSTEMS.md): nunca vender Adena, itens, XP, SP, poder.
