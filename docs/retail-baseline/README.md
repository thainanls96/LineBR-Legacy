# Retail Baseline — Interlude Bible

> **O documento definitivo que responde: "Como o Lineage II Interlude Retail realmente funcionava?"**
> Toda alteração futura do LineBR Legacy será comparada contra esta baseline.

---

## O que é a Baseline Retail

É o **corpo de conhecimento** do projeto: para cada sistema do jogo, registra-se lado a lado
1. **como a aCis 409 funciona hoje** (fato, com `arquivo:linha`), e
2. **como o Interlude Retail funcionava** (com nível de evidência e fonte),
3. **as divergências**, **as dúvidas** e **os riscos**.

## O que a Baseline **não** é
- ❌ Não é opinião, memória, nem "como deveria ser".
- ❌ Não é um plano de implementação (isso é o roadmap/backlog de cada sistema).
- ❌ Não é lista de melhorias — o projeto **não** busca ser melhor que o Interlude.

## Objetivo
Ter uma **régua**. Sem baseline, "Retail First" é slogan: não há contra o que comparar. Com ela, qualquer proposta futura é medida contra um registro versionado, datado e com evidência.

## Relação com a Knowledge Base (sem sobreposição)

| Base | Responde | Natureza |
|------|----------|----------|
| [`retail-knowledge-base/`](../retail-knowledge-base/) | **COMO** pesquisar, classificar e aceitar mudanças | Metodologia (processo) |
| **`retail-baseline/`** (esta) | **O QUE** sabemos sobre cada sistema | Conhecimento (conteúdo) |

A Baseline **consome** a metodologia: usa a escala ★ de [EVIDENCE_LEVELS](../retail-knowledge-base/EVIDENCE_LEVELS.md), as fontes de [RESEARCH_SOURCES](../retail-knowledge-base/RESEARCH_SOURCES.md) e é filtrada pela [CHANGE_ACCEPTANCE_POLICY](../retail-knowledge-base/CHANGE_ACCEPTANCE_POLICY.md).

> ⚠️ **Consolidação pendente:** este pacote traz [SYSTEM_CATALOG.md](SYSTEM_CATALOG.md) e [SYSTEM_TEMPLATE.md](SYSTEM_TEMPLATE.md), que **superam** o `SYSTEM_INDEX.md` e o `AUDIT_TEMPLATE.md` da knowledge-base (mesmo propósito, granularidade maior). Ao mesclar as branches, os dois antigos devem ser **removidos** para não haver duas fontes de verdade.

## Documentos

| Arquivo | Papel |
|---------|-------|
| [SYSTEM_CATALOG.md](SYSTEM_CATALOG.md) | **Catálogo canônico** de todos os sistemas + status |
| [SYSTEM_TEMPLATE.md](SYSTEM_TEMPLATE.md) | Template obrigatório do documento de baseline de cada sistema |
| [EVIDENCE_REGISTER.md](EVIDENCE_REGISTER.md) | Banco de evidências (ID, fonte, hash, nível, sistemas) |
| [UNKNOWN_BEHAVIORS.md](UNKNOWN_BEHAVIORS.md) | **O que não sabemos** — incertezas nunca são escondidas |
| [RETAIL_ASSUMPTIONS.md](RETAIL_ASSUMPTIONS.md) | Hipóteses separadas em PROVADO / PROVÁVEL / DESCONHECIDO |
| [DEPENDENCY_MAP.md](DEPENDENCY_MAP.md) | Quem depende de quem → define a ordem de auditoria |
| [ROADMAP_BASELINE.md](ROADMAP_BASELINE.md) | Fases ordenadas de construção da baseline |

## Como será utilizada
1. **Antes de qualquer proposta:** consultar o documento de baseline do sistema. Se o sistema não tem baseline → a proposta **não existe** (não há régua).
2. **Ao propor uma mudança:** citar o item da baseline + a evidência (ID do [EVIDENCE_REGISTER](EVIDENCE_REGISTER.md)).
3. **Ao auditar um sistema novo:** copiar o [SYSTEM_TEMPLATE](SYSTEM_TEMPLATE.md), seguir a ordem do [ROADMAP_BASELINE](ROADMAP_BASELINE.md) e o [DEPENDENCY_MAP](DEPENDENCY_MAP.md).
4. **Ao revisar um PR:** o revisor confere se a mudança bate com a baseline; divergir da baseline sem novo ADR = reprovado.

## Quem pode alterar
| Ação | Quem |
|------|------|
| Criar/atualizar baseline de um sistema | Qualquer dev, via PR, seguindo o template |
| **Elevar o nível ★ de um item** | Só com nova evidência registrada no [EVIDENCE_REGISTER](EVIDENCE_REGISTER.md) |
| Mover item de PROVÁVEL → PROVADO | **Somente** com evidência ≥ ★★★★ + revisão do dono |
| Remover/rebaixar um item | Via PR, justificando (evidência refutada) |
| Aprovar merge | **Dono do projeto** (Thainan) |

> **Regra de imutabilidade do registro:** evidências **nunca** são apagadas. Se uma evidência for refutada, marca-se como `REFUTADA` com a justificativa — o histórico do que se acreditou (e por quê) é parte do valor da baseline.

## Como novas evidências entram
```
1. Coletar artefato (RESEARCH_SOURCES.md)
2. Arquivar (Wayback + hash + data de acesso)
3. Registrar no EVIDENCE_REGISTER.md  → recebe ID (EV-NNN)
4. Classificar ★ (EVIDENCE_LEVELS.md) — declarar: sobre aCis ou sobre retail?
5. Vincular aos sistemas afetados (SYSTEM_CATALOG.md)
6. Atualizar RETAIL_ASSUMPTIONS.md (PROVADO/PROVÁVEL/DESCONHECIDO)
7. Se resolver uma incógnita → remover de UNKNOWN_BEHAVIORS.md (com link p/ a evidência)
8. PR → revisão → merge
```

## Estado atual (2026-07-15) — leitura honesta
O projeto possui **zero fontes retail de nível ★★★★+**. Em consequência:
- **nenhum** sistema pode ser marcado 🔵 *Retail validado* hoje;
- a Baseline nasce documentando, sobretudo, **o que a aCis faz** e **o que não sabemos do retail**.

Isso não é fracasso — é o diagnóstico correto, tornado explícito. A Baseline existe justamente para transformar essas lacunas em trabalho rastreável. Ver [UNKNOWN_BEHAVIORS.md](UNKNOWN_BEHAVIORS.md).
