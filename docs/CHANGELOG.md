# Changelog Documental — LineBR Legacy

> Histórico de todas as mudanças **estruturais** da documentação.
> (O changelog das decisões da Bíblia vive em [specification/CHANGELOG.md](specification/CHANGELOG.md).)

---

## [2.0.0] — 2026-07-15 · Sprint 010 — Congelamento e Consolidação

### Consolidado
- **73 documentos** unificados numa única branch (antes espalhados por **8 branches**, com links cruzados quebrados entre si). Merge de `retail-audit-movement` — **0 conflitos**.
- **Estrutura reorganizada por AUTORIDADE** (não por assunto). A pasta agora responde "quem manda":
  ```
  constitution/ 🔒 · adr/ 🔒 · specification/ 📗 · design/ 💭
  monetization/ 📗 · knowledge/{methodology,baseline,audits} 🔬
  engineering/ 🔧 · archive/ 📦
  ```
- **88 links relativos** reescritos e verificados — **0 quebrados**.

### Adicionado
- `DOCUMENT_MAP.md` — índice oficial (onde fica cada assunto, ordem de leitura, dependências)
- `DOCUMENTATION_POLICY.md` — os 5 níveis de autoridade e as regras permanentes
- `ROADMAP.md` — roadmap definitivo em 8 fases (substitui o original)
- `CHANGELOG.md` — este arquivo
- `archive/README.md` — índice do que foi arquivado e por quê

### Movido para `constitution/` (passam a ser Constituição 🔒)
`PROJECT_PHILOSOPHY.md` · `LINEBR_MANIFESTO.md` · `GAME_PHILOSOPHY.md` (de game-design) · `DESIGN_PRINCIPLES.md` (de game-design) · `OWNER_DECISIONS.md` (de linebr-bible) · `FORBIDDEN_FEATURES.md` (de monetization) · `BASE_ZERO.md`

### Renomeado / reorganizado
| Antes | Depois |
|-------|--------|
| `ADR/` | `adr/` |
| `linebr-bible/` | `specification/` |
| `game-design/` | `design/` |
| `retail-knowledge-base/` | `knowledge/methodology/` |
| `retail-baseline/` | `knowledge/baseline/` |
| `retail-audit/` | `knowledge/audits/movement/` |
| 8 arquivos técnicos soltos na raiz | `engineering/` |

### Arquivado (nada apagado — rastreabilidade preservada)
| Documento | Motivo |
|-----------|--------|
| `REVISION_410_PLAN.md` | **Obsoleto** — estratégia de perseguir a revisão 410 abandonada na Sprint 004 (o projeto passou a mirar o L2OFF retail, não revisões da aCis) |
| `REV410_CORE_ANALYSIS.md` | **Obsoleto** — idem |
| `SYSTEM_INDEX.superseded.md` | **Duplicado** — superado por `knowledge/baseline/SYSTEM_CATALOG.md` (63 sistemas vs 30, com existência verificada no código) |
| `AUDIT_TEMPLATE.superseded.md` | **Duplicado** — superado por `knowledge/baseline/SYSTEM_TEMPLATE.md` (superset, 12 seções) |
| `MONETIZATION_PHILOSOPHY.game-design.superseded.md` | **Superado** — era exploratório; a pasta `monetization/` traz as decisões do Owner |
| `ROADMAP.original.md` | **Superado** — substituído pelo `ROADMAP.md` definitivo |

### Virou referência oficial
| Documento | Papel |
|-----------|-------|
| `constitution/OWNER_DECISIONS.md` | **fonte normativa única** das decisões (101) |
| `constitution/DESIGN_PRINCIPLES.md` | **o teste** de toda proposta (P-01..P-15) |
| `knowledge/baseline/SYSTEM_CATALOG.md` | catálogo canônico (63 sistemas) |
| `knowledge/baseline/SYSTEM_TEMPLATE.md` | template único de auditoria |
| `knowledge/baseline/EVIDENCE_REGISTER.md` | banco único de evidências (EV-NNN) |
| `DOCUMENT_MAP.md` | índice oficial |
| `ROADMAP.md` | plano oficial |

### Mantido sem alteração
Todo o conteúdo de decisões: ADRs, Bíblia, monetização, game design, baseline, metodologia e auditoria de Movement. **Nenhuma decisão do Owner foi alterada.** **Nenhuma mecânica, rate, economia, VIP, Marketplace ou Auto Loot foi tocada.**

### Estado
📌 **Documentação oficialmente CONGELADA.** Novos documentos apenas por auditoria de sistema, evidência nova, decisão nova do Owner, ou necessidade de implementação ([DOCUMENTATION_POLICY](DOCUMENTATION_POLICY.md)).

---

## [1.x] — Sprints 001–009 (histórico resumido)
| Sprint | Entrega |
|:------:|---------|
| 001 | Build & Validation (2.881/2.881 classes byte-idênticas) |
| 002 | Runtime Validation (login+game operacionais, 0 erros) |
| — | Fundação: ADRs 001–005, filosofia, manifesto, contributing, roadmap |
| 004 | Auditoria de Movement + descoberta: **não existe spec pública do L2OFF** |
| 005 | Retail Knowledge Base (metodologia, escala ★, política de aceitação) |
| 006 | Retail Baseline (63 sistemas, evidências, incógnitas, dependências) |
| 007 | Game Design Bible (10 docs, princípios P-01..P-15) |
| 008 | Monetização (VIP, Marketplace, FORBIDDEN_FEATURES) |
| 009 | **LineBR Legacy Bible** (Constituição, 101 decisões, rates aprovadas) |
| 010 | **Congelamento + Consolidação** (este) |
