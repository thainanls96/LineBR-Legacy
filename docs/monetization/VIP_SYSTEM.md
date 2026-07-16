# Sistema VIP — LineBR Legacy

> Decisão oficial do Owner. **Nada implementado** — documento de registro.
> Governado pela Regra Mestra: *"Todo benefício pago deve economizar tempo, nunca substituir esforço."*

---

## Categorias

Três categorias, cumulativas: **VIP Bronze → VIP Silver → VIP Gold**.

## VIP Bronze

| Benefício | Categoria |
|-----------|-----------|
| Nickname (mudança) | identidade |
| Título (mudança) | identidade |
| Sexo (mudança) | identidade |
| Nick colorido | identidade visual |
| Título colorido | identidade visual |
| **Warehouse expandido** | logística |
| **Inventory expandido** | logística |
| **Offline Shop** — 1 personagem | conveniência |
| **Marketplace** — acesso a vender | conveniência |
| **Até 3 anúncios** no Marketplace | conveniência |

## VIP Silver

**Inclui todos os benefícios do Bronze**, mais:

| Benefício |
|-----------|
| **Offline Shop** — 2 personagens |
| **10 anúncios** no Marketplace |
| Mais alterações visuais |
| **Warehouse maior** (que Bronze) |
| **Inventory maior** (que Bronze) |

## VIP Gold

**Inclui todos os benefícios do Silver**, mais:

| Benefício |
|-----------|
| **Offline Shop** — 3 personagens |
| **20 anúncios** no Marketplace |
| **Anúncios destacados** (destaque visual) |
| **Warehouse máximo** |
| **Inventory máximo** |
| ⭐ **AUTO LOOT** (exclusivo Gold) |

---

## Auto Loot — VIP Gold (decisão aprovada, não está em discussão)

**Coleta automaticamente:**
- Adena
- Drops comuns
- Materiais
- Recipes
- Parts
- Equipamentos comuns
- Itens normais de farm

**NÃO funciona em:**
- ❌ Raid Boss
- ❌ Boss
- ❌ Eventos
- ❌ Drops de Boss

> A exclusão de Raid/Boss/Eventos preserva a disputa nos momentos de maior valor competitivo — que é onde o loot manual mais importa.

---

## Resumo comparativo

| Benefício | Bronze | Silver | Gold |
|-----------|:------:|:------:|:----:|
| Identidade (nick/título/sexo/cores) | ✅ | ✅ + | ✅ + |
| Warehouse expandido | ✅ | ✅✅ | ✅✅✅ máx |
| Inventory expandido | ✅ | ✅✅ | ✅✅✅ máx |
| Offline Shop | 1 char | 2 chars | 3 chars |
| Marketplace — anúncios | 3 | 10 | 20 |
| Anúncios destacados | ❌ | ❌ | ✅ |
| **Auto Loot** | ❌ | ❌ | ✅ |

---

## Fatos técnicos relevantes (EV-001 — aCis 409)

Registrados para orientar qualquer implementação futura:

| Item | Situação na base |
|------|------------------|
| **Auto Loot** | existe como **config global** (`AutoLoot = False`; `AutoLootRaid = False` separado). **Não** há suporte nativo por jogador → VIP-exclusivo exige **código custom** |
| **Offline Shop** | ❌ **não existe** na aCis 409 (0 arquivos) → custom completo |
| **Marketplace** | ❌ **não existe** na aCis 409 (0 arquivos) → custom completo |
| **Inventory (nativo)** | `MaximumSlotsForNoDwarf = 80` · **`MaximumSlotsForDwarf = 100`** |
| **Warehouse (nativo)** | `MaximumWarehouseSlotsForNoDwarf = 100` · **`MaximumWarehouseSlotsForDwarf = 120`** · `Clan = 200` |

> ⚠️ **Nota permanente:** os limites de inventário/warehouse são, na aCis 409 (e no Interlude), uma **mecânica de classe** — o Dwarf possui **+20 slots** nativos como vantagem de raça/classe. Qualquer expansão vendida precisa considerar o impacto sobre essa identidade. Registrado em [DECISION_LOG M-003](DECISION_LOG.md).

## Pendências de definição (não decididas)
| # | Pendência |
|---|-----------|
| V-1 | Valores numéricos exatos de warehouse/inventory por tier |
| V-2 | Duração/renovação de cada tier (mensal? vitalício?) |
| V-3 | Preço de cada tier |
| V-4 | "Mais alterações visuais" (Silver) — quais exatamente |
| V-5 | Escopo congelado: como impedir que o VIP "cresça" com o tempo |
