# Hipóteses sobre o Retail — LineBR Legacy

> Todas as afirmações que o projeto sustenta sobre o Interlude Retail, **separadas por status**.
> **JAMAIS misturar as três seções.** Um item só sobe de status com evidência registrada (`EV-NNN`).

---

## Definição dos status

| Status | Critério | Autoriza alteração? |
|--------|----------|:-------------------:|
| ✅ **PROVADO** | Evidência **≥ ★★★★** sobre o **retail**, registrada e reproduzível | ✅ Sim |
| 🟨 **PROVÁVEL** | Indício coerente (★★☆☆☆–★★★☆☆) sem prova; ou intenção declarada do autor da aCis | ❌ Não (vira pesquisa) |
| ⬜ **DESCONHECIDO** | Sem evidência de nenhum lado | ❌ Nunca |

> ⚠️ **Fatos sobre a aCis não entram aqui.** Este documento é só sobre o **retail**. O que a aCis faz é ★★★★★ e vive nos documentos de baseline de cada sistema.

---

## ✅ PROVADO (evidência ≥ ★★★★ sobre o retail)

> **NENHUM ITEM.**

O projeto **não possui nenhuma evidência retail** ([EVIDENCE_REGISTER](EVIDENCE_REGISTER.md)). Esta seção permanecerá vazia até que uma fonte oficial ★★★★+ seja obtida e registrada.

Isto é declarado sem rodeios de propósito: **hoje, o LineBR Legacy não tem uma única afirmação provada sobre o Interlude retail.** Tudo o que "sabemos" é sobre a aCis.

---

## 🟨 PROVÁVEL (indício, sem prova — NÃO autoriza alteração)

| # | Hipótese | Base do indício | ★ | Sistema |
|:-:|----------|-----------------|:-:|---------|
| A-01 | O cliente Interlude **suporta** movimento por teclado (o protocolo carrega o flag `0 = cursor keys`) | Campo existe no packet + comentário do autor (`MoveBackwardToLocation:45`) | ★★★☆☆ **(sobre o protocolo/cliente)** | B03 |
| A-02 | O retail tinha um "arranque" (andar antes de correr) ao iniciar o movimento | aCis o emula deliberadamente (`_moveTimeStamp <= 5`); comportamento é lembrado pela comunidade | ★★☆☆☆ | B03 |
| A-03 | O retail corrigia o Z do clique do piso para a altura da cabeça | Necessário pela semântica do cliente; aCis o faz (`+= collisionHeight`) | ★★☆☆☆ | B03 |
| A-04 | O retail usava geodata no formato hoje chamado "L2OFF" | A aCis implementa um leitor desse formato e o nomeia assim | ★★☆☆☆ | B01 |
| A-05 | O retail tinha desync/correção de posição (algum equivalente a `ValidateLocation`) | O packet existe no protocolo Interlude | ★★★☆☆ **(sobre o protocolo)** | B03 |
| A-06 | Bugs de terreno (escalar/cair) existiam também no retail | O autor da aCis registra o artefato como "bug" conhecido | ★☆☆☆☆ | B03 |

> **Nota importante sobre A-01 e A-05:** a existência de um **campo/packet no protocolo** é evidência sobre o **cliente** (★★★☆☆), não sobre **o que o servidor retail fazia** com ele. São coisas diferentes — não promover sem captura.

---

## ⬜ DESCONHECIDO (sem evidência)

| # | Questão | Sistema | Ref |
|:-:|---------|---------|-----|
| — | O servidor retail aceitava/processava movimento por teclado? | B03 | [U-010](UNKNOWN_BEHAVIORS.md#u-010--o-retail-aceitava-movimento-por-teclado) |
| — | Granularidade do tick de movimento no retail | B03 | U-011 |
| — | Autoridade de posição (cliente × servidor) no retail | B03 | U-013 |
| — | Limite de distância por clique no retail | B03 | U-014 |
| — | Alcance de NPC contra alvo em fuga no retail | E03 | U-015 |
| — | Comportamento retail em terreno íngreme | B03/B01 | U-016 |
| — | Fórmulas de dano físico/mágico do retail | C03/C04 | U-020 |
| — | Taxas retail do Interlude (XP/SP/Adena/Drop/Spoil) | G05/G06/G13 | U-021 |
| — | Regras de stacking de buffs/debuffs | D03/D04 | U-022 |
| — | Regras de aggro/hate | E03 | U-023 |
| — | Quais sistemas da aCis existiam de fato no Interlude retail | todos | U-003 |
| — | **Todo o restante dos 63 sistemas** (62 não auditados) | — | — |

---

## Armadilhas que este documento existe para evitar

1. **"O código da aCis faz X, logo o retail fazia X."** ❌ Falso. Código da aCis = evidência sobre a aCis.
2. **"O autor escreveu 'retail like'."** ❌ Isso é **intenção**, não prova. Não sobe status.
3. **"Todos os emuladores fazem assim."** ❌ Emuladores copiam-se entre si (inclusive os erros) → falso consenso.
4. **"Eu jogava em 2007 e lembro."** ❌ ★☆☆☆☆. Gera hipótese, nunca decisão.
5. **"É óbvio / faz sentido."** ❌ Não é evidência.

## Como promover um item
```
DESCONHECIDO → PROVÁVEL : indício documentado + fonte arquivada (★★☆☆☆+)
PROVÁVEL → PROVADO      : evidência ≥ ★★★★ sobre o RETAIL, registrada (EV-NNN),
                          reproduzível, + revisão do dono
qualquer → REFUTADO     : evidência contrária (o item NÃO é apagado — é marcado)
```

## Estado
| Status | Itens |
|--------|------:|
| ✅ PROVADO | **0** |
| 🟨 PROVÁVEL | 6 |
| ⬜ DESCONHECIDO | 11 + (62 sistemas não auditados) |
