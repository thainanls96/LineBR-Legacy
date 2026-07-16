# Retail Knowledge Base — LineBR Legacy

> Base de conhecimento e **metodologia oficial de pesquisa histórica** do projeto.
> Criada na Sprint 005, após a Sprint 004 revelar que **o maior obstáculo do projeto não é código — é a ausência de uma referência histórica confiável do Interlude/L2OFF**.

---

## 📜 Filosofia oficial

> **O objetivo do LineBR Legacy NÃO é criar um servidor melhor que o Interlude.**
>
> **O objetivo é reconstruir o Interlude com o maior nível de fidelidade tecnicamente comprovável.**
>
> **Na ausência de evidência suficiente, nenhuma alteração será implementada.**

Complementa (não substitui) o [PROJECT_PHILOSOPHY.md](../PROJECT_PHILOSOPHY.md), o [LINEBR_MANIFESTO.md](../LINEBR_MANIFESTO.md) e o [ADR-003 — Retail First](../ADR/ADR-003-retail-first.md).

---

## A descoberta que originou esta base

A auditoria de movimentação (Sprint 004) demonstrou, na prática, dois fatos incômodos:

1. **Não existe especificação pública do L2OFF Interlude.** As fontes históricas mais citadas estão mortas (o fórum do L2J não resolve mais). O que circula é, em larga medida, memória coletiva.
2. **O código da aCis prova o que a aCis faz — e nada sobre o retail.** É evidência de altíssima qualidade para uma pergunta ("o que o servidor faz hoje?") e evidência **nula** para outra ("o que o L2OFF fazia em 2007?"). Confundir as duas é o erro mais fácil e mais caro deste projeto.

Daí a regra que passa a valer: **toda afirmação sobre o retail carrega um nível de evidência explícito**, e só certos níveis autorizam mudança.

## Documentos

| Documento | O que define |
|-----------|--------------|
| [METHODOLOGY.md](METHODOLOGY.md) | O fluxo obrigatório: Descoberta → … → Commit. Nenhuma etapa pode ser pulada. |
| [EVIDENCE_LEVELS.md](EVIDENCE_LEVELS.md) | Escala ★☆ de confiança e **quais níveis autorizam alteração**. |
| [RESEARCH_SOURCES.md](RESEARCH_SOURCES.md) | Catálogo de fontes e sua confiabilidade. |
| [VALIDATION_PROCESS.md](VALIDATION_PROCESS.md) | Como provar que a mudança faz o que diz — e não quebra o resto. |
| [CHANGE_ACCEPTANCE_POLICY.md](CHANGE_ACCEPTANCE_POLICY.md) | Os 6 critérios inegociáveis de aceitação. |
| [SYSTEM_INDEX.md](SYSTEM_INDEX.md) | Todos os sistemas do servidor e seu status de auditoria. |
| [AUDIT_TEMPLATE.md](AUDIT_TEMPLATE.md) | Template obrigatório de toda auditoria futura. |

## Como usar (fluxo rápido)

1. Vai auditar um sistema? → copie o [AUDIT_TEMPLATE.md](AUDIT_TEMPLATE.md) e atualize o [SYSTEM_INDEX.md](SYSTEM_INDEX.md) para *Em auditoria*.
2. Encontrou uma possível divergência do retail? → classifique com [EVIDENCE_LEVELS.md](EVIDENCE_LEVELS.md) usando [RESEARCH_SOURCES.md](RESEARCH_SOURCES.md).
3. Quer implementar? → passe pela [CHANGE_ACCEPTANCE_POLICY.md](CHANGE_ACCEPTANCE_POLICY.md). Se não passar: **não implemente** (registre no backlog do sistema).
4. Passou? → siga a [METHODOLOGY.md](METHODOLOGY.md) até o fim, com [VALIDATION_PROCESS.md](VALIDATION_PROCESS.md).

## Relação com os ADRs
Esta base **operacionaliza** decisões já congeladas:
- [ADR-003](../ADR/ADR-003-retail-first.md) diz *o que* pode mudar (Retail First; custom só se opcional/problema comprovado/infra).
- Esta base diz *como provar* que algo é retail — e **veta** o que não se prova.
- [ADR-005](../ADR/ADR-005-politica-desenvolvimento.md) diz *como* implementar (commits atômicos, revisão, reversibilidade).
