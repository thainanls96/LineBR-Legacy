# Arquivo — LineBR Legacy

> 📦 **Somente leitura. Nada aqui é vigente. Nada aqui será apagado.**
> Existe para preservar a **rastreabilidade** do projeto: o que se acreditou, o que se decidiu, e por que mudou.

---

## Regra
- ❌ **Nunca citar** um documento daqui como referência vigente.
- ❌ **Nunca apagar.**
- ✅ Consultar para entender **por que** algo mudou.

## Conteúdo

| Documento | Origem | Por que foi arquivado |
|-----------|--------|------------------------|
| [REVISION_410_PLAN.md](REVISION_410_PLAN.md) | Sprint 002 | **Obsoleto.** Plano de aplicar a revisão 410 da aCis. A Sprint 004 mudou a estratégia: o projeto deixou de perseguir revisões da aCis e passou a mirar o **L2OFF Interlude retail**. Além disso, as revisões 410/411 são de doador e nunca foram obtidas |
| [REV410_CORE_ANALYSIS.md](REV410_CORE_ANALYSIS.md) | Sprint 003 | **Obsoleto.** Auditoria das classes Core para a 410. Conclusão registrada na época: **0 alterações implementáveis-com-prova** sem o diff oficial. Continua sendo um bom registro de *por que* a estratégia 410 foi abandonada |
| [SYSTEM_INDEX.superseded.md](SYSTEM_INDEX.superseded.md) | Sprint 005 | **Duplicado.** Índice de 30 sistemas. Superado por `knowledge/baseline/SYSTEM_CATALOG.md`, que cataloga **63 sistemas com existência verificada no código** |
| [AUDIT_TEMPLATE.superseded.md](AUDIT_TEMPLATE.superseded.md) | Sprint 005 | **Duplicado.** Template de auditoria. Superado por `knowledge/baseline/SYSTEM_TEMPLATE.md` (superset, 12 seções obrigatórias) |
| [MONETIZATION_PHILOSOPHY.game-design.superseded.md](MONETIZATION_PHILOSOPHY.game-design.superseded.md) | Sprint 007 | **Superado.** Documento exploratório que apresentava opções de monetização sem decidir. A pasta `monetization/` (Sprint 008) traz as **decisões do Owner**. ⚠️ Nota histórica: este documento listava "warehouse/inventário maior" como *nunca vender* — decisão posteriormente superada (ver `monetization/DECISION_LOG.md` M-003) |
| [ROADMAP.original.md](ROADMAP.original.md) | Sprint 002 | **Superado** pelo `ROADMAP.md` definitivo (Sprint 010) |

## Como restaurar algo daqui
Não se "restaura". Se um documento arquivado voltar a ser relevante, seu **conteúdo** é reincorporado ao documento vigente correspondente, via PR, com registro no [CHANGELOG](../CHANGELOG.md). O arquivo permanece aqui, intocado.
