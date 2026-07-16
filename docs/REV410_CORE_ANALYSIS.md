# Revisão 410 — Análise da Categoria CORE

> **Sprint 003.** Análise técnica **read-only** da source oficial aCis 409 para a categoria Core da revisão 410.
> **Regra soberana desta sprint (do dono):** *"Se existir qualquer dúvida, NÃO implementar. Nada da imaginação. Somente alterações comprováveis tecnicamente."*

---

## Conclusão executiva (leia primeiro)

Sem o **diff oficial 409→410**, **nenhuma** alteração de código pode ser *comprovada* como pertencente à revisão 410. O changelog fornece **temas**, não mudanças arquivo/método. A auditoria abaixo demonstra, com evidência da própria source, que **cada candidato Core cai em pelo menos uma** destas situações: (a) não existe no 409 → seria adição inventada; (b) já está limpo/sem defeito → nada a "corrigir"; (c) exigiria criar código novo; (d) tocaria áreas proibidas desta sprint; ou (e) é reorganização/renome (proibido).

➡️ **Resultado: 0 alterações implementáveis-com-prova nesta sprint.** Recomendação: obter o diff oficial 410 antes de implementar (ver [REVISION_410_PLAN.md](REVISION_410_PLAN.md) — bloqueio).

---

## 1. Auditoria das classes (localização · uso · referências · impacto)

| Classe | Pacote | Linhas | Refs | Quem usa | Impacto de mexer |
|--------|--------|-------:|-----:|----------|------------------|
| **WorldObject** | `gameserver.model` | 838 | ~121 | raiz da hierarquia de objetos do mundo | **ALTO** |
| **Location** | `gameserver.model.location` | 194 | ~132 | posições em todo o servidor (extends Point2D) | **ALTO** |
| **Point2D** | `gameserver.model.location` | 264 | ~21 | classe-base de Location | **ALTO** (base) |
| **MathUtil** | `commons.math` | 280 | ~22 | cálculos diversos (distância, ângulos) | **MÉDIO** |
| **ItemContainer** | `gameserver.model.itemcontainer` | 549 | ~12 | Inventory/Warehouse/PetInventory | **MÉDIO** |
| **Territory** | `gameserver.model.spawn` | 226 | ~7 | zonas de spawn | **MÉDIO** |
| **Pagination** | `commons.data` | 135 | ~11 | Community Board / listagens HTML | **BAIXO** |
| **SchemeBuffer** | `gameserver.model.actor.instance` | 353 | ~1 | NPC buffer (scheme) | **BAIXO** |
| **FrequentSkill** | inner enum de `SkillTable` | — | ~17 | Seven Signs, skills fixas | (extrair = reorg **proibido**) |
| **QuestVars** | — | — | **0** | **não existe no 409** | N/A |
| **Geometry** | — | — | **0** | **não existe no 409** | N/A |

## 2. Implementabilidade por item

### Classes ausentes no 409 → adição 410+ (NÃO implementável)
- **QuestVars** — `grep` = 0 menções. No 409, variáveis de quest vivem em `scripting/QuestState.java` (armazenamento interno). `QuestVars` como classe/conceito **não existe** → recriá-la seria **imaginação** (proibido). **Implementável? NÃO.**
- **Geometry** — `grep` = 0 menções. Utilidades geométricas hoje estão em `commons.math.MathUtil`. Criar `Geometry` = adição inventada. **Implementável? NÃO.**

### FrequentSkill (reorganização proibida)
- Existe como **`SkillTable.FrequentSkill`** (enum interno, linha 187 de `SkillTable.java`, 17 usos). Uma eventual "extração para classe própria" é **reorganização/renome de pacote** — **explicitamente proibida** nesta sprint. **Implementável? NÃO.**

### Candidatos citados no exemplo do dono — verificados na source
| Candidato | Evidência no 409 | Veredito |
|-----------|------------------|----------|
| "Remove clone desnecessário de Location" | `Location.clone()` usado **58×**; a maioria em `CreatureMove`/`NpcAI`/`Creature`/`Intention` (**Movement/NpcAI = PROIBIDO**). Remover clone arrisca **aliasing** (mutação compartilhada). | **NÃO** (proibido + risco) |
| `ItemContainer::forEachItem` | Método **não existe**; 409 expõe `getItems()` (Set) e itera com `for`. Adicioná-lo = **código novo** sem prova de ser 410. | **NÃO** (código novo) |
| "Pagination >1000" | `Pagination` já usa `Math.clamp`, `stream.toList()`, `subList`; **não há limite/bug `>1000`** no 409. | **NÃO** (nada a corrigir) |
| "WorldObject radius" | `isIn3DRadius(...)` e `forEachKnownTypeInRadius(...)` já presentes e limpos; sem defeito identificável. | **NÃO** (sem defeito) |
| "Point2D" | Estrutura moderna e coesa; nenhuma mudança identificável/atribuível à 410. | **NÃO** (não comprovável) |

### Temas do changelog 410 pertencentes a OUTRAS sprints (fora do escopo Core)
- **Makers, NpcAi/Desires, Cursed Weapon, Movement, Task Managers (MultiSpawn/respawn/despawn)** → **PROIBIDOS** nesta sprint (regra do dono). **Implementável agora? NÃO.**
- **Admincommands, Organization, Bugfixes (ghost corpses)** → só implementáveis **com o diff** que mostre o quê exatamente mudou. **Implementável? PARCIAL — bloqueado pelo diff.**

## 3. Alterações realmente possíveis nesta sprint
**Nenhuma.** Não por falta de análise, mas porque nenhuma satisfaz simultaneamente: (1) comprovável como 410, (2) fora das áreas proibidas, (3) sem criar código novo, (4) sem reorganizar/renomear, (5) sem dúvida. A regra "na dúvida, não implementar" resolve todos os casos para **NÃO**.

## 4. Ordem recomendada (quando o diff 410 estiver disponível)
Mantida a estratégia do [REVISION_410_PLAN.md](REVISION_410_PLAN.md): `Core/Org → Admincommands → Misc → Task/Spawn → Cursed Weapon → Makers → NpcAi/Desires → Movement → Network`, uma categoria por vez com Build + Runtime Validation entre cada.

## 5. "Primeira alteração pronta para revisão"
**Não há alteração pronta.** Entregar uma alteração aqui exigiria inventá-la — o oposto do que esta sprint exige. A "primeira alteração" ficará pronta assim que o **diff oficial 409→410** for fornecido; então a auditoria por-arquivo/método será preenchida e a menor/mais segura correção Core comprovada será a primeira a entrar (Modificar → Compilar → Runtime Validation → Logs → Testes → Relatório → Commit).

---

### Método da auditoria (rastreabilidade)
Todas as afirmações acima foram obtidas por `find`/`grep` sobre `source/aCis_gameserver/java` (aCis 409, commit `55ff8a4e`), sem alterar nenhum arquivo. Nenhum commit de código foi feito nesta sprint.
