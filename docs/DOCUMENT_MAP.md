# Mapa Documental — LineBR Legacy

> **Índice oficial do projeto.** Onde fica cada assunto, quem manda, e em que ordem ler.
> Regido pela [DOCUMENTATION_POLICY.md](DOCUMENTATION_POLICY.md).

---

## A árvore (organizada por AUTORIDADE, não por assunto)

```
docs/
├── DOCUMENT_MAP.md          ← você está aqui (índice oficial)
├── DOCUMENTATION_POLICY.md  ← quem manda, quem explica, o que congela
├── ROADMAP.md               ← plano oficial do projeto (8 fases)
├── CHANGELOG.md             ← histórico documental
│
├── constitution/   🔒 MANDA        — imutável sem ADR do Owner
├── adr/            🔒 MANDA        — decisões de arquitetura (nunca apagadas)
├── specification/  📗 ESPECIFICA   — a Bíblia: o que o servidor SERÁ
├── design/         💭 EXPLICA      — o porquê das decisões de design
├── monetization/   📗 ESPECIFICA   — VIP, Marketplace, serviços, modelo
├── knowledge/      🔬 CONHECIMENTO — o que sabemos (com evidência)
│   ├── methodology/     — COMO pesquisar e aceitar mudanças
│   ├── baseline/        — O QUE sabemos (catálogo, evidências, incógnitas)
│   └── audits/movement/ — auditorias por sistema
├── engineering/    🔧 OPERA        — build, runtime, ambiente, workflow
└── archive/        📦 HISTÓRICO    — superado. Nunca apagado. Somente leitura
```

## Ordem correta de leitura

### 🥇 Para entender o projeto (obrigatório para qualquer dev)
1. [constitution/PROJECT_PHILOSOPHY.md](constitution/PROJECT_PHILOSOPHY.md) — o que é o projeto
2. [constitution/LINEBR_MANIFESTO.md](constitution/LINEBR_MANIFESTO.md) — os 10 princípios permanentes
3. [constitution/GAME_PHILOSOPHY.md](constitution/GAME_PHILOSOPHY.md) — que servidor queremos ser
4. [constitution/DESIGN_PRINCIPLES.md](constitution/DESIGN_PRINCIPLES.md) — P-01..P-15 (o **teste** de toda proposta)
5. [constitution/OWNER_DECISIONS.md](constitution/OWNER_DECISIONS.md) — **as 101 decisões vigentes**
6. [specification/README.md](specification/README.md) — a Bíblia

### 🥈 Antes de tocar em código
7. [adr/README.md](adr/README.md) → **ADR-001..005**
8. [knowledge/methodology/EVIDENCE_LEVELS.md](knowledge/methodology/EVIDENCE_LEVELS.md) — a escala ★
9. [knowledge/methodology/CHANGE_ACCEPTANCE_POLICY.md](knowledge/methodology/CHANGE_ACCEPTANCE_POLICY.md) — os 6 critérios
10. [knowledge/methodology/METHODOLOGY.md](knowledge/methodology/METHODOLOGY.md) — o fluxo obrigatório
11. [engineering/CONTRIBUTING.md](engineering/CONTRIBUTING.md) — commits, branches, PR

### 🥉 Para construir/rodar
12. [engineering/BUILD.md](engineering/BUILD.md) · [engineering/BUILD_VALIDATION.md](engineering/BUILD_VALIDATION.md)
13. [engineering/ENVIRONMENT_SETUP.md](engineering/ENVIRONMENT_SETUP.md) · [engineering/RUNTIME_VALIDATION.md](engineering/RUNTIME_VALIDATION.md)
14. [engineering/REPOSITORY_STRUCTURE.md](engineering/REPOSITORY_STRUCTURE.md) · [engineering/ARCHITECTURE.md](engineering/ARCHITECTURE.md)

## Onde fica cada assunto

| Assunto | Documento |
|---------|-----------|
| **Decisões vigentes do Owner** | [constitution/OWNER_DECISIONS.md](constitution/OWNER_DECISIONS.md) 🔒 |
| **Decisões pendentes** | [specification/OPEN_DECISIONS.md](specification/OPEN_DECISIONS.md) |
| **O que nunca será vendido** | [constitution/FORBIDDEN_FEATURES.md](constitution/FORBIDDEN_FEATURES.md) 🔒 |
| **Base Zero / origem** | [constitution/BASE_ZERO.md](constitution/BASE_ZERO.md) 🔒 |
| **Rates (XP/SP)** | [specification/PROGRESSION.md](specification/PROGRESSION.md) |
| **Economia (Adena/drop/spoil/craft)** | [specification/ECONOMY.md](specification/ECONOMY.md) |
| **Customs aprovadas (5)** | [specification/CUSTOM_SYSTEMS.md](specification/CUSTOM_SYSTEMS.md) |
| **VIP / Auto Loot / Marketplace** | [specification/SERVER_SERVICES.md](specification/SERVER_SERVICES.md) · [monetization/](monetization/) |
| **Regras (bot, RMT, dupe)** | [specification/SERVER_RULES.md](specification/SERVER_RULES.md) |
| **Quests e mundo** | [specification/QUESTS_AND_WORLD.md](specification/QUESTS_AND_WORLD.md) |
| **Por que a economia é assim** | [design/ECONOMY_PHILOSOPHY.md](design/ECONOMY_PHILOSOPHY.md) |
| **Catálogo dos 63 sistemas** | [knowledge/baseline/SYSTEM_CATALOG.md](knowledge/baseline/SYSTEM_CATALOG.md) |
| **Evidências (EV-NNN)** | [knowledge/baseline/EVIDENCE_REGISTER.md](knowledge/baseline/EVIDENCE_REGISTER.md) |
| **O que não sabemos** | [knowledge/baseline/UNKNOWN_BEHAVIORS.md](knowledge/baseline/UNKNOWN_BEHAVIORS.md) |
| **Ordem de auditoria** | [knowledge/baseline/DEPENDENCY_MAP.md](knowledge/baseline/DEPENDENCY_MAP.md) |
| **Auditoria de Movement** | [knowledge/audits/movement/](knowledge/audits/movement/) |
| **Template de auditoria** | [knowledge/baseline/SYSTEM_TEMPLATE.md](knowledge/baseline/SYSTEM_TEMPLATE.md) |

## Quem referencia quem (dependências)

```
constitution/  ──manda em──▶  todo o resto
     ▲
adr/  ──governa──▶  o que pode divergir do retail (ADR-003) e como se desenvolve (ADR-005)
     ▲
specification/ (Bíblia)  ──especifica──▶  o que implementar
     │  consome
     ▼
design/ (o porquê)  ·  monetization/ (VIP/mercado)
     │
knowledge/  ──autoriza (ou veta)──▶  qualquer mudança de gameplay
  methodology (★ + política)  →  baseline (catálogo/evidências)  →  audits (por sistema)
     │
engineering/  ──valida──▶  build · runtime · logs
```

**Regra de precedência:** `constitution` > `adr` > `specification` > `design`/`monetization` > `knowledge` > `engineering`.
Em conflito, **o de cima vence** — e o de baixo deve ser corrigido.

## Documentos obrigatórios (ninguém implementa sem ter lido)
1. [constitution/OWNER_DECISIONS.md](constitution/OWNER_DECISIONS.md)
2. [constitution/DESIGN_PRINCIPLES.md](constitution/DESIGN_PRINCIPLES.md)
3. [adr/ADR-003-retail-first.md](adr/ADR-003-retail-first.md)
4. [knowledge/methodology/CHANGE_ACCEPTANCE_POLICY.md](knowledge/methodology/CHANGE_ACCEPTANCE_POLICY.md)
5. [specification/CUSTOM_SYSTEMS.md](specification/CUSTOM_SYSTEMS.md)
6. [engineering/CONTRIBUTING.md](engineering/CONTRIBUTING.md)
