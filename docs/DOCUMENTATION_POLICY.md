# Política de Documentação — LineBR Legacy

> Define **qual documento manda**, qual apenas explica, qual nunca muda e qual é só histórico.
> Vigente a partir da Sprint 010 (congelamento documental).

---

## Os cinco níveis de autoridade

### 🔒 1. CONSTITUIÇÃO — *manda*
**Pastas:** `constitution/` · `adr/`

Estes documentos **governam todos os outros**. Uma proposta que os contrarie é **recusada**, não debatida.

| Documento | Natureza |
|-----------|----------|
| `constitution/PROJECT_PHILOSOPHY.md` | identidade do projeto |
| `constitution/LINEBR_MANIFESTO.md` | os 10 princípios permanentes |
| `constitution/GAME_PHILOSOPHY.md` | que servidor queremos ser |
| `constitution/DESIGN_PRINCIPLES.md` | P-01..P-15 — o **teste** de toda proposta |
| `constitution/OWNER_DECISIONS.md` | **as decisões vigentes do Owner** (normativo) |
| `constitution/FORBIDDEN_FEATURES.md` | o que nunca será vendido |
| `constitution/BASE_ZERO.md` | a origem imutável |
| `adr/ADR-001..005` | decisões de arquitetura |

**Como alterar:** somente o **Owner**, via ADR novo que supere o anterior explicitamente. **Nunca por edição silenciosa.**

### 📗 2. ESPECIFICAÇÃO — *define o que será construído*
**Pastas:** `specification/` (a Bíblia) · `monetization/`

Dizem **o que** o servidor será. Evoluem com aprovação do Owner + entrada no [CHANGELOG](CHANGELOG.md).

### 💭 3. DESIGN — *explica o porquê*
**Pasta:** `design/`

**Não manda.** Explica o raciocínio por trás das decisões. Se contradisser a Constituição ou a Especificação, **o documento de design é que está errado**.

### 🔬 4. CONHECIMENTO — *o que sabemos, com evidência*
**Pasta:** `knowledge/`

- `methodology/` — como pesquisar, classificar (★) e aceitar mudanças. **Tem poder de veto**: uma mudança sem evidência suficiente não entra, mesmo que todos queiram.
- `baseline/` — o catálogo, o registro de evidências, as incógnitas.
- `audits/` — auditorias por sistema.

Evolui **com evidência nova**, nunca com opinião.

### 🔧 5. ENGENHARIA — *como se constrói e se roda*
**Pasta:** `engineering/`

Documentação operacional. Evolui livremente conforme a realidade técnica (build, ambiente, ferramentas).

### 📦 6. ARQUIVO — *histórico*
**Pasta:** `archive/`

**Somente leitura. Nunca apagado. Nunca citado como vigente.** Preserva o que foi superado, para que a rastreabilidade do projeto sobreviva.

---

## Respostas diretas

| Pergunta | Resposta |
|----------|----------|
| **Qual documento manda?** | `constitution/` e `adr/`. Acima de todos: **`OWNER_DECISIONS.md`** (o que o Owner decidiu) e **`DESIGN_PRINCIPLES.md`** (o teste). |
| **Qual documento apenas explica?** | Tudo em `design/`. Também as seções de análise em `monetization/` e `knowledge/`. |
| **Qual nunca poderá ser alterado?** | `constitution/BASE_ZERO.md` (a origem é um fato histórico), a tag `acis-409-runtime-base`, e todo `archive/`. ADRs **nunca são apagados** — só marcados `Superseded`. `FORBIDDEN_FEATURES` só **cresce**. |
| **Qual pode evoluir?** | `specification/`, `monetization/`, `knowledge/`, `engineering/` — cada um por sua regra (Owner / evidência / realidade técnica). |
| **Qual serve só como histórico?** | `archive/` inteiro + o `CHANGELOG`. |

## Regra de precedência (em conflito)
```
constitution  >  adr  >  specification  >  design | monetization  >  knowledge  >  engineering
```
> **Exceção que vale ouro:** `knowledge/methodology` tem **poder de veto** sobre mudanças de gameplay — mesmo contra a vontade de todos. Sem evidência ≥ ★★★★, não se implementa. É a única regra que protege o projeto de si mesmo.

## Regras permanentes

1. **Nada é apagado.** Superado vai para `archive/` com sufixo `.superseded.md` e um aviso no topo.
2. **Uma fonte de verdade por assunto.** Duplicou? Um vira canônico, o outro vai para `archive/`.
3. **Toda decisão do Owner** entra em `constitution/OWNER_DECISIONS.md`. Pendências em `specification/OPEN_DECISIONS.md`. **Nunca assumir.**
4. **Todo documento novo** entra no [DOCUMENT_MAP.md](DOCUMENT_MAP.md).
5. **Toda mudança documental** entra no [CHANGELOG.md](CHANGELOG.md).
6. **Links relativos e válidos.** Nenhum link para branch, nenhum link quebrado.
7. **Não produzir documento por produzir.** Documento sem leitor e sem decisão é dívida, não ativo.

## Estado: CONGELADO
A partir da Sprint 010 a documentação está **oficialmente congelada** para fins de estrutura. As próximas sprints são de **implementação**.

Novos documentos só devem nascer quando:
- uma **auditoria de sistema** for realizada (usa o `SYSTEM_TEMPLATE`), **ou**
- uma **evidência nova** for registrada, **ou**
- o **Owner tomar uma decisão nova**, **ou**
- a **implementação** exigir documentação técnica.

**Não** se cria documento novo para reexplicar o que já está escrito.
