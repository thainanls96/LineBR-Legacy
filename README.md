# LineBR Legacy

Servidor **Lineage II Interlude** baseado na **aCis revisão 409**, em transformação para um ambiente de desenvolvimento profissional: **source + datapack + database + documentação**.

> **Status:** migração de estrutura em andamento na branch `development/source-migration`.
> A `main` continua com o runtime original preservado. A tag **`acis-409-runtime-base`** é a Base Zero imutável.

## Estrutura

```
LineBR-Legacy/
├── source/               ← código-fonte oficial da aCis 409 (base de desenvolvimento)
│   ├── aCis_gameserver/  ← gameserver + loginserver + commons (Java, Ant)
│   └── aCis_datapack/    ← datapack (html, xml, sql, tools)
├── runtime-reference/    ← runtime compilado original (REFERÊNCIA HISTÓRICA — não editar)
├── database/             ← documentação e artefatos de banco
├── docs/                 ← documentação técnica do projeto
└── tools/                ← utilitários de desenvolvimento (build, deploy, etc.)
```

## Documentação

| Documento | Conteúdo |
|-----------|----------|
| [docs/Base-Zero.md](docs/Base-Zero.md) | O que é a Base Zero, a tag imutável e a origem de tudo |
| [docs/Architecture.md](docs/Architecture.md) | Arquitetura da aCis (gameserver/login/commons/datapack) |
| [docs/Repository-Structure.md](docs/Repository-Structure.md) | Explicação de cada pasta do repositório |
| [docs/Build.md](docs/Build.md) | Como compilar (JDK 21 + Apache Ant), passo a passo |
| [docs/Development-Workflow.md](docs/Development-Workflow.md) | Branches, commits, fluxo de revisões e customizações |

## Origem

- **Source:** [gitlab.com/Tryskell/acis_public](https://gitlab.com/Tryskell/acis_public) — commit `55ff8a4e` ("aCis 409").
- **Runtime:** pack compilado da mesma revisão 409 (auditado como byte-idêntico em datapack e SQL).
- **Build:** Apache Ant · **JDK 21**.

## Objetivo

1. Estabelecer a aCis 409 limpa como fundação versionada.
2. Aplicar as revisões oficiais **410** e **411** (etapa futura, ainda não iniciada).
3. Reintroduzir customizações do LineBR (VIP, Skins, Coins, etc.) de forma isolada e rastreável.
