# Níveis de Evidência — LineBR Legacy

> Escala oficial de confiança. **Toda afirmação sobre o comportamento retail deve carregar um nível.** Sem nível declarado, a afirmação não existe para efeito de decisão.

---

## ⚠️ A regra que evita o erro mais caro do projeto

Estes níveis medem **afirmações sobre o Interlude/L2OFF retail** — não sobre a aCis.

> **O código da aCis é prova ★★★★★ de "o que a aCis faz" e prova ☆ (nenhuma) de "o que o retail fazia".**

Ler o código responde *"como está implementado hoje?"*. **Nunca** responde *"como era no retail?"*. Confundir as duas perguntas transforma opinião em falso-fato — e foi exatamente o risco identificado na Sprint 004.

---

## A escala

### ★★★★★ — Comprovado por múltiplas fontes oficiais independentes
Duas ou mais fontes de **origem NCSoft/L2OFF** que concordam. Ex.: comportamento observável no **cliente oficial Interlude** + confirmado por **patch note NCSoft** + reproduzido em **captura de pacotes**.
**Autoriza alteração:** ✅ **SIM.**

### ★★★★☆ — Fonte oficial + reprodução prática
Uma fonte oficial (cliente, binário/PTS L2OFF, patch note) **e** reprodução empírica que confirma (captura de pacotes própria, teste em servidor de referência).
**Autoriza alteração:** ✅ **SIM.**

### ★★★☆☆ — Fonte oficial apenas (sem reprodução)
Uma fonte oficial credível, porém **não reproduzida** por nós. Ex.: patch note descrevendo a mecânica, sem termos medido.
**Autoriza alteração:** ⚠️ **CONDICIONAL.**
- ✅ Sim, se a mudança **não altera gameplay** (infra, logging, performance, correção de bug interno comprovado).
- ⚠️ Se **altera gameplay**: só como **opcional (desligado por padrão)** e com **ADR** — ou aguarda subir para ★★★★.

### ★★☆☆☆ — Comunidade especializada
Relato técnico e coerente de fonte respeitada (dev experiente, wiki de comunidade, fórum técnico), **sem** artefato oficial nem reprodução.
**Autoriza alteração:** ❌ **NÃO.** Vira **hipótese de pesquisa** no backlog do sistema — nunca implementação.

### ★☆☆☆☆ — Memória, opinião ou hipótese
"Eu lembro que era assim", "faz sentido que fosse", "todo servidor faz assim".
**Autoriza alteração:** ❌ **NUNCA.** Nem como opcional.

---

## Tabela de decisão

| Nível | Origem típica | Altera gameplay? | Decisão |
|:-----:|---------------|------------------|---------|
| ★★★★★ | ≥2 fontes oficiais concordantes | sim ou não | ✅ implementar (ADR se mudar gameplay) |
| ★★★★☆ | oficial + reprodução própria | sim ou não | ✅ implementar (ADR se mudar gameplay) |
| ★★★☆☆ | oficial, sem reprodução | **não** | ✅ implementar |
| ★★★☆☆ | oficial, sem reprodução | **sim** | ⚠️ só opcional + ADR, ou pesquisar mais |
| ★★☆☆☆ | comunidade especializada | — | ❌ backlog de pesquisa |
| ★☆☆☆☆ | memória/opinião | — | ❌ nunca |

## Caso especial: divergências **internas** da aCis
Quando a evidência é o próprio código e a afirmação é sobre a **aCis** (ex.: *"`PlayerMove` e `CreatureMove` usam matemáticas diferentes"* — Sprint 004, D-11), então:
- a afirmação é **★★★★★ sobre a aCis** (arquivo:linha comprova);
- mas a decisão de **mudar** ainda depende de o alvo ser conhecido: corrigir uma inconsistência interna **sem saber qual lado é o retail** é escolher um palpite. Nesse caso, trate como **problema comprovado** (ADR-003, critério 2) **apenas** se houver defeito objetivo (crash, exploit, inconsistência que o próprio autor documenta como bug) — caso contrário, é ★★☆☆☆ disfarçado.

## Mapeamento com a Sprint 004
A auditoria de movimentação usou uma escala provisória de 3 níveis. Equivalência oficial:

| Sprint 004 | Escala oficial |
|------------|----------------|
| 🟢 ALTO (fato no código aCis) | ★★★★★ **sobre a aCis** · ☆ sobre o retail |
| 🟡 MÉDIO (plausível/derivável) | ★★☆☆☆ |
| 🔴 BAIXO (comunidade/lore) | ★☆☆☆☆ – ★★☆☆☆ |

> Consequência: **nenhum** dos 14 itens de [MOVEMENT_L2OFF_DIFFERENCES](../audits/movement/MOVEMENT_L2OFF_DIFFERENCES.md) atinge hoje ★★★★☆ **como afirmação sobre o retail**. Por isso o backlog daquele sistema começa por *obter evidência* (geodata + referência medível), não por implementar.

## Como declarar
Todo item de auditoria/backlog declara assim:
```
Evidência: ★★★☆☆
Fonte: patch note NCSoft (Interlude, 2007-xx-xx) — RESEARCH_SOURCES.md#patch-notes
Reprodução: não realizada
Afirmação: sobre o RETAIL
```
