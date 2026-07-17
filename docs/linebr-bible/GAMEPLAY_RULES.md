# Regras de Gameplay — LineBR Legacy

> ✅ Decisões aprovadas pelo Owner.

---

## Skills — APROVADO

| Regra | Valor | 📌 Fato (EV-001) |
|-------|-------|------------------|
| **Learning Skills** | **Manual** | ✅ `AutoLearnSkills = False` é o **default nativo** da aCis → **zero custom** |
| **Aquisição** | **Compradas com SP** | nativo (retail) |
| **Guild Masters** | **Obrigatórios** | nativo (retail) — o jogador vai ao NPC aprender |

> ✅ **Totalmente retail e sem custo técnico.** Esta decisão apenas confirma o comportamento nativo.

## Teleport — APROVADO

| Regra | Valor |
|-------|-------|
| **Teleport** | **Retail** (custo em Adena, conforme o original) |

> Preserva [P-10](../game-design/DESIGN_PRINCIPLES.md) — *nenhuma feature pode diminuir a importância da exploração*. O custo de deslocamento é o que dá **tamanho** ao mundo.

🔴 **PENDENTE:** teleport gratuito (se haverá, para quem, até que level) → [OPEN_DECISIONS](OPEN_DECISIONS.md).

## NPC Buffer

| Regra | Valor |
|-------|-------|
| **Existe** | ✅ Sim, **gratuito** |
| **Até qual level** | 🔴 **PENDENTE DE DECISÃO DO OWNER** |

📌 **FATO (EV-001):** a aCis 409 **possui buffer nativo** — `SchemeBuffer.java` + `BufferManager.java`. Habilitar não exige código custom (é datapack/spawn/config). O **limite por level**, porém, precisa ser verificado se é suportado nativamente.

⚠️ **Registro de tensão:** o [SOCIAL_PHILOSOPHY §1](../game-design/SOCIAL_PHILOSOPHY.md) e a decisão **D-006** (Sprint 007, status *Proposto*) diziam *"sem buffer NPC gratuito — mata a classe de suporte e a interdependência"*. A decisão atual do Owner **supera** D-006. A limitação por level é justamente a mitigação: buffer no early game (onde não há suporte disponível) sem matar o Buffer humano no mid/end game. **O level escolhido determina o impacto** — daí ser pendência, não detalhe.

## Outras regras de gameplay

| Regra | Valor |
|-------|-------|
| Rates XP/SP | Escalonadas por faixa → [PROGRESSION](PROGRESSION.md) |
| Adena / Drop / Spoil / Craft / Quest | 1x / 1x / 1x / 100% / Retail → [ECONOMY](ECONOMY.md) |
| Auto Loot | **Apenas VIP Gold**, farm comum; ❌ Raid/Boss/Eventos → [SERVER_SERVICES](SERVER_SERVICES.md) |
| Enchant (safe / máximo) | 🔴 **PENDENTE** → [OPEN_DECISIONS](OPEN_DECISIONS.md) |
| Dual Box | 🔴 **PENDENTE** → [OPEN_DECISIONS](OPEN_DECISIONS.md) |
| Geodata | 🔴 **PENDENTE** → [OPEN_DECISIONS](OPEN_DECISIONS.md) |
| Death / perda de XP | **Retail** |
| Karma / PK | **Retail** → [PVP_AND_PVE](PVP_AND_PVE.md) |

## Princípio regente
Tudo o que **não** está listado como custom aprovada em [CUSTOM_SYSTEMS](CUSTOM_SYSTEMS.md) segue o comportamento **retail/nativo da aCis 409**. Na dúvida: **retail** ([ADR-003](../ADR/ADR-003-retail-first.md)).
