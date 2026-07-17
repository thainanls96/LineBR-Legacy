> 📦 **DOCUMENTO ARQUIVADO — NÃO VIGENTE.**
> Duplicado: superado por `knowledge/baseline/SYSTEM_CATALOG.md` (63 sistemas, existência verificada no código).
> Preservado para rastreabilidade. Ver [archive/README.md](README.md) e [CHANGELOG](../CHANGELOG.md).

---

# Índice de Sistemas — LineBR Legacy

> Mapa de todos os sistemas do servidor e seu status de auditoria. **Atualizar a cada sprint.**

---

## Legenda de status
| Status | Significado |
|--------|-------------|
| ⚪ **Não auditado** | Nunca analisado |
| 🔵 **Em auditoria** | Análise em andamento |
| 🟡 **Auditado** | Arquitetura/fluxo/riscos documentados; diferenças **hipotéticas** levantadas |
| 🟢 **Retail validado** | Diferenças confirmadas com evidência **≥ ★★★★** |
| 🟠 **Em implementação** | Mudanças aprovadas sendo aplicadas |
| ✅ **Concluído** | Implementado, validado e documentado |

> **Nota:** *Auditado* → *Retail validado* exige uma **fonte retail de nível ★★★★+**, que o projeto ainda **não possui** (ver [RESEARCH_SOURCES.md](../knowledge/methodology/RESEARCH_SOURCES.md#estado-atual-das-fontes-2026-07-15)). Hoje, nenhum sistema pode passar de 🟡.

---

## Sistemas

| # | Sistema | Status | Sprint | Documentação | Observações |
|:-:|---------|:------:|:------:|--------------|-------------|
| 01 | **Movement** | 🟡 Auditado | 004 | [retail-audit/MOVEMENT_*](../retail-audit/) | 14 diferenças levantadas; nenhuma ≥★★★★. Bloqueio P0: geodata + referência L2OFF |
| 02 | **GeoData / Pathfinding** | ⚪ Não auditado | — | — | ⛔ **Bloqueador do projeto**: formato `L2OFF` configurado, **arquivos ausentes** → sem pathfinding/colisão |
| 03 | **Combat** | ⚪ Não auditado | — | — | Fórmulas, hit/miss, crítico, dano |
| 04 | **Skills** | ⚪ Não auditado | — | — | Efeitos, cast, cooldown, stacking |
| 05 | **AI (NpcAi / Desires)** | ⚪ Não auditado | — | — | Acoplado a Movement |
| 06 | **NPC** | ⚪ Não auditado | — | — | Spawn, respawn, comportamento |
| 07 | **Quests** | ⚪ Não auditado | — | — | 857 scripts carregados no runtime |
| 08 | **Items** | ⚪ Não auditado | — | — | Inventário, equip, enchant |
| 09 | **Drops** | ⚪ Não auditado | — | — | Taxas, listas, sweep |
| 10 | **Spoil** | ⚪ Não auditado | — | — | Relacionado a Drops |
| 11 | **Craft** | ⚪ Não auditado | — | — | Recipes, Makers/Manor |
| 12 | **Economy** | ⚪ Não auditado | — | — | Adena, lojas, taxas |
| 13 | **Olympiad** | ⚪ Não auditado | — | — | Ciclos, pontuação, heróis |
| 14 | **Hero** | ⚪ Não auditado | — | — | Depende de Olympiad |
| 15 | **Clan** | ⚪ Não auditado | — | — | Níveis, skills, guerra |
| 16 | **Castle Siege** | ⚪ Não auditado | — | — | Agendamentos vistos no runtime |
| 17 | **Seven Signs** | ⚪ Não auditado | — | — | 2.616 NPCs de evento no runtime |
| 18 | **Manor** | ⚪ Não auditado | — | — | Ligado a Castle/Craft |
| 19 | **Fishing** | ⚪ Não auditado | — | — | Championship ativo no runtime |
| 20 | **Pets** | ⚪ Não auditado | — | — | `PetStatus`, movimento próprio |
| 21 | **Summons** | ⚪ Não auditado | — | — | `SummonMove`, `SummonAI` |
| 22 | **Boat** | ⚪ Não auditado | — | — | `BoatMove`, `BoatDock` (mapeado parcialmente na 004) |
| 23 | **Packets / Protocol** | ⚪ Não auditado | — | — | ⚠️ Área sensível |
| 24 | **Network** | ⚪ Não auditado | — | — | ⚠️ Área sensível |
| 25 | **ThreadPool** | ⚪ Não auditado | — | — | ⚠️ Área sensível; tick de movimento depende |
| 26 | **Admin Commands** | ⚪ Não auditado | — | — | 93 handlers no runtime |
| 27 | **Events** | ⚪ Não auditado | — | — | Derby, casais, fishing champ |
| 28 | **Community Board (BBS)** | ⚪ Não auditado | — | — | Nativo aCis; usa `Pagination` |
| 29 | **Zones** | ⚪ Não auditado | — | — | `ZoneManager`; `revalidateZone` no hot path |
| 30 | **Sieges (outros)** | ⚪ Não auditado | — | — | Fortress, Rainbow Springs, Devastated |

**Resumo:** 1 sistema 🟡 auditado · 29 ⚪ não auditados · **0 🟢 retail validados**.

## Prioridade sugerida das próximas auditorias
1. **GeoData/Pathfinding (#02)** — é pré-requisito do Movement e do combate/AI. Sem ele, várias auditorias ficam sem chão.
2. **Combat (#03)** e **Skills (#04)** — maior impacto percebido pelo jogador.
3. **Drops (#09) / Spoil (#10) / Economy (#12)** — sustentam a "economia saudável" do Manifesto.
4. **AI (#05)** e **NPC (#06)** — acoplados a Movement.

> Ordem final é decisão do dono. Toda auditoria usa o [AUDIT_TEMPLATE.md](../knowledge/baseline/SYSTEM_TEMPLATE.md).
