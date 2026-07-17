# Progressão — LineBR Legacy

> ✅ **RATES APROVADAS PELO OWNER.** Esta decisão resolve a pendência D-001 do game-design.

---

## Rates de XP — APROVADO

| Faixa de level | Rate |
|:--------------:|:----:|
| **1 ~ 30** | **3x** |
| **30 ~ 60** | **2x** |
| **60 ~ 75** | **1x** |
| **75 ~ 80** | **0.75x** |

## Rates de SP — APROVADO

**Mesmo comportamento da XP:**

| Faixa de level | Rate |
|:--------------:|:----:|
| **1 ~ 30** | **3x** |
| **30 ~ 60** | **2x** |
| **60 ~ 75** | **1x** |
| **75 ~ 80** | **0.75x** |

---

## Características desta curva

| Faixa | Efeito |
|-------|--------|
| 1–30 | **Acelerado** — reduz o atrito de entrada |
| 30–60 | **Suavizado** — atravessa a faixa de maior evasão |
| 60–75 | **Retail puro** |
| 75–80 | **Mais lento que o retail** — o end game é **mais duro** que o original |

> **Nota de design:** a curva é **decrescente e termina abaixo de 1x**. Não é um servidor "rate alto" — é um servidor de **arranque facilitado e topo endurecido**. O 75–80 a `0.75x` torna o nível máximo **mais raro** do que no Interlude original.

## 📌 FATOS (EV-001 — aCis 409)

| Fato | Valor |
|------|-------|
| Rate nativa da source oficial e do runtime Base Zero | **`RateXp = 1.` · `RateSp = 1.`** (x1 puro) |
| Suporte nativo a rate **por faixa de level** | ❌ **não existe** — a aCis tem rate **global** única |

⚠️ **Consequência técnica:** rates escalonadas por faixa de level **exigem código custom**. Não é uma configuração — é uma alteração no cálculo de XP/SP. Deve ser registrada como custom em [CUSTOM_SYSTEMS](CUSTOM_SYSTEMS.md) e receber ADR ([ADR-003](../ADR/ADR-003-retail-first.md)).

## ⚠️ Relação com Retail First

Esta curva **diverge** do Interlude retail (x1 em todas as faixas). É uma **decisão consciente do Owner** e exige ADR de enquadramento.

**Ponto forte da decisão (registro técnico):** as rates de **economia permanecem intocadas** — Adena 1x, Drop 1x, Spoil 1x, Craft 100% ([ECONOMY](ECONOMY.md)). Isso preserva a cadeia econômica do Interlude (drop → spoil → craft → Dwarf → mercado), que é o que normalmente morre em servidores de rate alta. **O boost é de tempo, não de riqueza.**

**Consequência a observar:** com XP 3x e Drop 1x na faixa 1–30, o jogador **sobe de nível mais rápido do que se equipa**. Ele chegará ao 30 com equipamento relativamente pior que no retail. Isso não é erro — é um efeito previsível desta combinação, e vale acompanhar quando o servidor abrir.

## Demais mecanismos de progressão

| Mecanismo | Regra |
|-----------|-------|
| Drop | **1x** ([ECONOMY](ECONOMY.md)) |
| Spoil | **1x** |
| Craft | **100%** |
| Quest | **Retail** |
| Enchant | 🔴 **PENDENTE DE DECISÃO DO OWNER** (safe enchant, máximo) → [OPEN_DECISIONS](OPEN_DECISIONS.md) |
| Learning Skills | **Manual**, com SP, via Guild Masters ([GAMEPLAY_RULES](GAMEPLAY_RULES.md)) |
| Raid Boss / Grand Boss | Retail — importantes ([PVP_AND_PVE](PVP_AND_PVE.md)) |
| Seven Signs | Retail — importante ([QUESTS_AND_WORLD](QUESTS_AND_WORLD.md)) |
| Noblesse / Subclass | Quest obrigatória — nada pulado |
| Olympiad → Hero | Retail ([PVP_AND_PVE](PVP_AND_PVE.md)) |
