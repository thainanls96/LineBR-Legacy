# Filosofia de Monetização — LineBR Legacy

> Documento permanente. Registra a filosofia oficial aprovada pelo Owner.

---

## 1. Base imutável

- **Retail First** — Interlude 2007 é a referência.
- **Sem Pay To Win.**
- **Todo poder do personagem deve ser conquistado exclusivamente jogando.**

Nunca serão vendidos: poder, equipamentos, Adena, XP, SP, Hero, Noble, Buffs, Boss, itens criados. Lista completa e permanente em [FORBIDDEN_FEATURES.md](FORBIDDEN_FEATURES.md).

## 2. Regra Mestra

> ### "Todo benefício pago deve economizar tempo, nunca substituir esforço."

Todo recurso futuro deverá obedecer esta regra. Ela é o **teste** de qualquer proposta de monetização.

## 3. Princípio Final

> ### "Se um jogador chegar ao topo do servidor, isso deve acontecer porque ele jogou melhor, organizou melhor seu clã e dedicou mais tempo ao jogo — nunca porque gastou mais dinheiro."

## 4. Economia — regras oficiais

| # | Regra |
|:-:|-------|
| E-1 | A economia do servidor utiliza **exclusivamente Adena** |
| E-2 | **Nenhuma moeda premium circula dentro do jogo** |
| E-3 | **Nenhuma moeda substitui Adena** |
| E-4 | **Nenhum NPC venderá itens próprios** |
| E-5 | O **Marketplace apenas conecta jogadores** |
| E-6 | **Todo item existente veio de algum jogador** |
| E-7 | **O servidor nunca cria itens** |
| E-8 | **O servidor nunca cria Adena** |

> **Consequência:** não há injeção externa de valor na economia. Tudo o que circula foi produzido dentro do mundo, por jogadores, jogando. Esta é a defesa estrutural mais forte contra inflação artificial.

## 5. O que a monetização pode tocar

| Categoria | Permitido? | Observação |
|-----------|:----------:|------------|
| Identidade visual (nick, título, cores, sexo) | ✅ | não afeta poder |
| Conveniência de logística (warehouse/inventário) | ✅ (por decisão do Owner) | ver ⚠️ em [DECISION_LOG M-003](DECISION_LOG.md) |
| Offline Shop | ✅ (por decisão do Owner) | custom — não existe na aCis |
| Marketplace (vender) | ✅ (por decisão do Owner) | custom — não existe na aCis |
| Auto Loot (farm comum) | ✅ (por decisão do Owner) | **exclusivo VIP Gold** — ver [DECISION_LOG M-004](DECISION_LOG.md) |
| Serviços administrativos | ✅ | ver [SERVICE_POLICY.md](SERVICE_POLICY.md) |
| **Qualquer coisa que dê poder** | ❌ | [FORBIDDEN_FEATURES.md](FORBIDDEN_FEATURES.md) |

## 6. Auto Loot — decisão oficial

**Aprovada pelo Owner. Registrada como decidida. Não está em discussão.**

- **Auto Loot EXISTE** e é **exclusivo do VIP Gold**.
- **Coleta:** Adena · Drops comuns · Materiais · Recipes · Parts · Equipamentos comuns · Itens normais de farm.
- **NÃO funciona em:** Raid Boss · Boss · Eventos · Drops de Boss.

**Fato técnico (EV-001):** na aCis 409 o Auto Loot é uma **config global** (`AutoLoot = False` por padrão), com `AutoLootRaid` separado (também `False`). A separação "farm comum sim / raid boss não" **coincide** com a arquitetura nativa. Porém, torná-lo **por jogador (VIP)** exige **código custom** — não é apenas ligar uma config. Registrado em [DECISION_LOG M-004](DECISION_LOG.md).

## 7. Relação com o Retail First

Esta política **decide o que o retail não dita**: o Interlude era assinatura (todos pagavam igual, ninguém comprava poder). Esse modelo não é replicável num servidor privado, então o projeto precisa de uma política própria — e ela está aqui.

⚠️ **Registro honesto e permanente:** VIP, Offline Shop, Marketplace e Auto Loot por jogador **não existem no Interlude retail**. São **customizações**. Pelo [ADR-003](../ADR/ADR-003-retail-first.md), customizações exigem enquadramento (opcional / problema comprovado / infra) e ADR próprio. As tensões estão registradas no [DECISION_LOG](DECISION_LOG.md) — não para reabrir a decisão do Owner, mas porque **um projeto que registra só o que deu certo não tem memória, tem propaganda**.

## 8. Sustentabilidade
Ver [BUSINESS_MODEL.md](BUSINESS_MODEL.md).
