# Monetização — LineBR Legacy

> Documentação **permanente** da filosofia de monetização do projeto.
> **Nada aqui está implementado.** Esta pasta é registro de decisão e política — não especificação técnica de entrega.

---

## Filosofia oficial (imutável)

> **"Todo benefício pago deve economizar tempo, nunca substituir esforço."** — Regra Mestra

> **"Se um jogador chegar ao topo do servidor, isso deve acontecer porque ele jogou melhor, organizou melhor seu clã e dedicou mais tempo ao jogo — nunca porque gastou mais dinheiro."** — Princípio Final

Base imutável do projeto: **Retail First · Interlude 2007 · Sem Pay To Win · Todo poder é conquistado jogando.**

## Documentos

| Arquivo | Conteúdo |
|---------|----------|
| [MONETIZATION_PHILOSOPHY.md](MONETIZATION_PHILOSOPHY.md) | Filosofia, economia (só Adena), regras mestras |
| [VIP_SYSTEM.md](VIP_SYSTEM.md) | VIP Bronze / Silver / Gold — benefícios oficiais |
| [MARKETPLACE.md](MARKETPLACE.md) | Marketplace P2P (só itens de jogadores) |
| [SERVICE_POLICY.md](SERVICE_POLICY.md) | Serviços administrativos |
| [FORBIDDEN_FEATURES.md](FORBIDDEN_FEATURES.md) | Lista permanente do que **nunca** será vendido |
| [BUSINESS_MODEL.md](BUSINESS_MODEL.md) | Modelo de receita e sustentabilidade |
| [DECISION_LOG.md](DECISION_LOG.md) | Registro de decisões (M-001…) |

## Relação com os demais documentos do projeto

| Documento | Relação |
|-----------|---------|
| [game-design/MONETIZATION_PHILOSOPHY.md](../game-design/MONETIZATION_PHILOSOPHY.md) | ⚠️ **Superado por esta pasta.** Era exploratório (apresentava opções); esta pasta traz as **decisões do Owner**. Consolidar na fusão das branches |
| [game-design/DESIGN_PRINCIPLES.md](../game-design/DESIGN_PRINCIPLES.md) | P-11 (anti-P2W) é a raiz desta política |
| [ADR-003 Retail First](../ADR/ADR-003-retail-first.md) | Governa o que pode divergir do Interlude |
| [retail-knowledge-base/CHANGE_ACCEPTANCE_POLICY](../retail-knowledge-base/CHANGE_ACCEPTANCE_POLICY.md) | Rege como qualquer item daqui poderia um dia ser implementado |

## Estado

**Nada implementado.** Nenhum sistema, NPC, VIP, Marketplace ou Auto Loot existe no servidor. Toda entrega desta sprint é documental.

**Fatos técnicos verificados** na base (EV-001 — aCis 409, commit `55ff8a4e`):
| Item | Situação real na aCis 409 |
|------|---------------------------|
| **Auto Loot** | ✅ existe como **config global** (`AutoLoot = False` por padrão; `AutoLootRaid` separado, também False). **Não** é por jogador — VIP-exclusivo exigiria código custom |
| **Offline Shop** | ❌ **não existe** (0 arquivos) — seria custom completo |
| **Marketplace** | ❌ **não existe** (0 arquivos) — seria custom completo |
| **Inventário** | mecânica de **classe**: `NoDwarf = 80` · **`Dwarf = 100`** |
| **Warehouse** | mecânica de **classe**: `NoDwarf = 100` · **`Dwarf = 120`** · `Clan = 200` |

> Estes fatos estão registrados porque qualquer implementação futura precisará considerá-los — e porque a auditoria da sprint os levantou. Ver [DECISION_LOG](DECISION_LOG.md).
