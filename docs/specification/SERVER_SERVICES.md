# Serviços do Servidor — LineBR Legacy

> ✅ Consolidação da Sprint 008. **Não alterado.**
> Fonte completa: [docs/monetization/](../monetization/)

---

## Regras mestras

> **"Todo benefício pago deve economizar tempo, nunca substituir esforço."**
> **"...nunca porque gastou mais dinheiro."**

## Sistema VIP

Três categorias cumulativas: **Bronze → Silver → Gold**.

### VIP Bronze
Nickname · Título · Sexo · Nick colorido · Título colorido · **Warehouse expandido** · **Inventory expandido** · **Offline Shop (1 personagem)** · **Marketplace** · **até 3 anúncios**

### VIP Silver
*Inclui Bronze* + **Offline Shop (2 personagens)** · **10 anúncios** · mais alterações visuais · **Warehouse maior** · **Inventory maior**

### VIP Gold
*Inclui Silver* + **Offline Shop (3 personagens)** · **20 anúncios** · **anúncios destacados** · **Warehouse máximo** · **Inventory máximo** · ⭐ **AUTO LOOT**

### Auto Loot (exclusivo VIP Gold)
| Coleta | NÃO funciona em |
|--------|-----------------|
| Adena · Drops comuns · Materiais · Recipes · Parts · Equipamentos comuns · Itens normais de farm | ❌ Raid Boss · ❌ Boss · ❌ Eventos · ❌ Drops de Boss |

## Marketplace
Em **Giran** · só itens de jogadores · pagamento **só Adena** · comprador: qualquer um · vendedor: **só VIP** · anúncios 3/10/20 (Gold destacado) · **taxa em Adena aprovada para implementação futura** (valores 🔴 pendentes).

## Serviços administrativos
Mudança de Nick · Sexo · Título · Cor do Nick · Cor do Título · Clan Rename · Alliance Rename · Recuperação de personagem deletado · Recuperação de conta · Recuperação de PIN · Recuperação administrativa de itens (**casos comprovados**).

> Todos são **administrativos**. Nenhum altera gameplay.

## 📌 Fatos técnicos (EV-001)
| Item | Situação na aCis 409 |
|------|----------------------|
| VIP | ❌ não existe → custom |
| Marketplace | ❌ 0 arquivos → custom |
| Offline Shop | ❌ 0 arquivos → custom |
| Auto Loot | ⚠️ config **global** (`AutoLoot = False`; `AutoLootRaid` separado) → VIP-exclusivo exige custom |
| Inventory nativo | `NoDwarf = 80` · **`Dwarf = 100`** |
| Warehouse nativo | `NoDwarf = 100` · **`Dwarf = 120`** · `Clan = 200` |

⚠️ **Registro (M-003):** inventário/warehouse são **mecânica de classe** — o Dwarf tem **+20 slots nativos**. Mitigação sugerida: teto do VIP **≤** limite nativo do Dwarf, preservando a vantagem de classe. 🔴 Números pendentes.

## Pendências
🔴 Preços · duração/renovação dos tiers · números exatos de warehouse/inventory · "mais alterações visuais" (Silver) · valores das taxas do Marketplace → [OPEN_DECISIONS](OPEN_DECISIONS.md)

## Proibido
[monetization/FORBIDDEN_FEATURES.md](../constitution/FORBIDDEN_FEATURES.md) — lista permanente e imutável.
