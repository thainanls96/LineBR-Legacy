# Marketplace — LineBR Legacy

> Decisão oficial do Owner. **Nada implementado.**

---

## Regras oficiais

| # | Regra |
|:-:|-------|
| MP-1 | O Marketplace vende **apenas itens de jogadores** |
| MP-2 | **O servidor nunca vende itens** |
| MP-3 | **O servidor nunca cria itens** |
| MP-4 | **O servidor nunca cria Adena** |
| MP-5 | **Comprador:** qualquer jogador (VIP ou não) |
| MP-6 | **Pagamento:** exclusivamente **Adena** |
| MP-7 | **Vendedor:** somente VIP |

> **Consequência estrutural:** o Marketplace é um **canal**, não uma fonte. Todo item nele veio do mundo, dropado/craftado/spoilado por um jogador. Nenhum valor novo entra na economia por meio dele.

## Limites de anúncios

| Tier | Anúncios | Destaque visual |
|------|:--------:|:---------------:|
| **Bronze** | 3 | ❌ |
| **Silver** | 10 | ❌ |
| **Gold** | 20 | ✅ **sim** |

## Recomendação futura (apenas documentada — não implementar)

**Taxas em Adena como *Adena Sink*:**
1. **Taxa de publicação** — cobrada ao criar o anúncio (em Adena), independentemente de vender.
2. **Taxa sobre venda** — percentual em Adena sobre a transação concluída.

**Objetivo:** funcionar como **dreno de Adena** (*sink*), retirando moeda de circulação a cada transação.

### Por que isto importa (análise)
A economia do Interlude depende do equilíbrio **faucet ≤ sink** ([ECONOMY_PHILOSOPHY](../game-design/ECONOMY_PHILOSOPHY.md)). Um Marketplace **sem taxa** é neutro na criação de Adena, mas é **negativo** para os drenos existentes: ele **substitui** o comércio presencial em Giran, que hoje carrega custos implícitos (tempo, deslocamento, teleporte). Ou seja: sem taxa, o Marketplace **remove** drenos indiretos sem repor nenhum.

Com taxa, ele passa a ser **um dos drenos mais eficientes possíveis** — porque incide sobre a riqueza que efetivamente circula, e escala junto com a atividade econômica.

**Recomendação técnica:** se o Marketplace for implementado, a **taxa deveria vir junto, não depois**. Introduzir taxa em um mercado já acostumado a ser gratuito é politicamente muito mais caro do que nascer com ela.

> Apenas documentado. Não implementar. Valores não definidos.

## Fato técnico (EV-001)
**O Marketplace NÃO existe na aCis 409** (0 arquivos). Seria uma **customização completa**: modelo de dados, packets, UI (HTML do datapack), persistência (SQL), e integração com inventário/warehouse.

Implicações a considerar em qualquer implementação futura:
- **Protocolo:** ⚠️ o Interlude não tem UI nativa de marketplace → provável uso de Community Board (BBS) + HTML, que **é** nativo.
- **Segurança:** todo sistema de troca é vetor de **dupe** — o risco mais grave da economia ([ECONOMY §11](../game-design/ECONOMY_PHILOSOPHY.md)).
- **Retail First:** é custom → exige ADR ([ADR-003](../ADR/ADR-003-retail-first.md)).

## Pendências
| # | Pendência |
|---|-----------|
| MP-a | Valores das taxas (publicação e venda) |
| MP-b | Duração do anúncio |
| MP-c | Onde o item fica custodiado enquanto anunciado |
| MP-d | Interface (BBS nativo × custom) |
| MP-e | Auditoria anti-dupe obrigatória antes de qualquer implementação |
