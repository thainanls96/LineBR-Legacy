# LineBR Legacy Bible — Constituição Oficial

> **O documento mais importante do projeto.** Responde: *"Como funciona exatamente o LineBR Legacy?"*
> Toda implementação futura deve seguir obrigatoriamente esta documentação.

---

## Autoridade

Esta Bíblia é a **fonte única de verdade** sobre o funcionamento do servidor. Em caso de conflito com qualquer outro documento, **a Bíblia prevalece** — exceto sobre:
- [ADR/](../ADR/) — decisões de arquitetura (técnicas)
- [retail-knowledge-base/](../retail-knowledge-base/) — metodologia de evidência

**Regra de ouro desta Bíblia:** nada aqui é inventado. Toda linha é (a) decisão aprovada pelo Owner, (b) fato verificado no código (EV-001), ou (c) explicitamente marcada **PENDENTE DE DECISÃO DO OWNER**.

## Documentos

| Arquivo | Conteúdo |
|---------|----------|
| [SERVER_IDENTITY.md](SERVER_IDENTITY.md) | Missão, visão, público, filosofia |
| [GAMEPLAY_RULES.md](GAMEPLAY_RULES.md) | Regras de jogo (skills, teleport, buffer) |
| [PROGRESSION.md](PROGRESSION.md) | **Rates aprovadas** (XP/SP) |
| [ECONOMY.md](ECONOMY.md) | Adena, drop, spoil, craft, marketplace |
| [PVP_AND_PVE.md](PVP_AND_PVE.md) | PvP, PK, bosses, sieges, Olympiad |
| [SOCIAL_SYSTEMS.md](SOCIAL_SYSTEMS.md) | Clã, aliança, Hero, comunidade |
| [QUESTS_AND_WORLD.md](QUESTS_AND_WORLD.md) | Quests e importância do mundo |
| [SERVER_SERVICES.md](SERVER_SERVICES.md) | VIP e serviços administrativos |
| [CUSTOM_SYSTEMS.md](CUSTOM_SYSTEMS.md) | **As 5 customs aprovadas** — todas as demais proibidas |
| [SERVER_RULES.md](SERVER_RULES.md) | Regras de conduta (bot, RMT, exploit) |
| [OWNER_DECISIONS.md](../constitution/OWNER_DECISIONS.md) | **Somente fatos decididos** — sem opinião |
| [OPEN_DECISIONS.md](OPEN_DECISIONS.md) | **Pendências de decisão do Owner** |
| [CHANGELOG.md](CHANGELOG.md) | Histórico de mudanças da Bíblia |

## Estado do servidor

**Nada implementado.** O servidor hoje é a **aCis 409 pura** (Base Zero, tag `acis-409-runtime-base`), build e runtime validados, **rates nativas x1**, sem nenhuma custom.

Esta Bíblia especifica **o que o LineBR Legacy será** — não o que ele já é.

## Como usar

| Situação | O que fazer |
|----------|-------------|
| Vai implementar algo | Confira aqui primeiro. Não está na Bíblia? **Não implementa** |
| A Bíblia diz "PENDENTE" | **Não assuma.** Pergunte ao Owner |
| Conflito com outro doc | A Bíblia prevalece (exceto ADRs e metodologia) |
| Mudar uma decisão | Owner aprova → atualiza a Bíblia → registra no [CHANGELOG](CHANGELOG.md) |

## Legenda
- ✅ **APROVADO** — decisão do Owner, vigente
- 🔴 **PENDENTE DE DECISÃO DO OWNER** — não assumir, não implementar
- 📌 **FATO (EV-001)** — verificado no código da aCis 409 (commit `55ff8a4e`)
- ⚠️ **CUSTOM** — diverge do Interlude retail; exige ADR ([ADR-003](../adr/ADR-003-retail-first.md))
