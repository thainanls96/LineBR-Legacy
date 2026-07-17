# Quests e Mundo — LineBR Legacy

> ✅ Decisões aprovadas pelo Owner.

---

## Quests — regra oficial

> ### **Todas as quests possuem importância. Nada será pulado. Nada será simplificado.**

| Quest | Status |
|-------|--------|
| **Quest inicial** | ✅ **Importante** |
| **Quest de profissão** | ✅ **Obrigatória** |
| **Quest de acesso** | ✅ **Obrigatória** |
| **Quest de Catacomb** | ✅ **Importante** |
| **Quest de Necropolis** | ✅ **Importante** |
| **Quest de Noblesse** | ✅ **Importante** |
| **Quest de Subclass** | ✅ **Importante** |

**Rate de Quest:** **Retail** ([ECONOMY](ECONOMY.md)).

📌 **FATO (EV-001):** a aCis 409 carrega **857 scripts regulares + 6 agendados**. Nenhum será desativado ou simplificado.

> **Consequência:** não haverá atalhos, NPCs "facilitadores", nem quests puladas por conveniência. A jornada é a do Interlude.

---

## Mundo — regra oficial

> ### **O mundo deve permanecer vivo. Nada será descartado.**

| Elemento | Status |
|----------|--------|
| **Giran** | ✅ **Centro econômico** do servidor |
| **Marketplace** | ✅ **Ficará em Giran** |
| **Catacombs** | ✅ **Possuem importância** |
| **Necropolis** | ✅ **Possuem importância** |
| **Raid Boss** | ✅ **Possuem importância** |
| **Grand Boss** | ✅ **Possuem importância** |
| **Castle Siege** | ✅ **Possui importância** |
| **Olympiad** | ✅ **Possui importância** |
| **Seven Signs** | ✅ **Possui importância** |

### Giran e o Marketplace
O Marketplace fica **em Giran** — decisão coerente com Giran ser o coração econômico e social. **Isso é design deliberado:** ancorar o Marketplace fisicamente na cidade preserva o motivo de as pessoas estarem lá.

⚠️ **Registro para acompanhamento:** um Marketplace, por natureza, reduz a necessidade de negociar presencialmente. Ancorá-lo em Giran mitiga, mas não elimina, o risco de esvaziar a cidade. *"Giran vazia = servidor morto"* ([WORLD_IMPORTANCE](../design/WORLD_IMPORTANCE.md)) — vale monitorar a presença em Giran depois que o Marketplace existir.

### 📌 FATO (EV-001) — Catacombs e Necropolis
**Não são um "sistema"** na aCis 409. Vivem no **datapack** (22 arquivos xml/sql + 40 html) + `SevenSignsManager` + `DungeonGatekeeper` / `DungeonTeleporter`.
**Consequência:** "dar importância" a eles = manter **Seven Signs funcionando**, não implementar algo novo. Eles já existem e funcionam nativamente.

---

## Princípio regente
[SERVER_IDENTITY](SERVER_IDENTITY.md): **Tudo deve ter importância. Nada deve ser descartável.**

Se uma quest, mapa ou boss estiver irrelevante no nosso servidor, a causa será **nossa** (rates, economia, população) — nunca do conteúdo. A resposta correta é **corrigir a causa**, jamais "compensar" com custom.
