# ADR-002 — Estrutura do Repositório

- **Status:** Aceito
- **Data:** 2026-07-15
- **Decisores:** Thainan Lima

## Contexto

Um projeto de emulador de longo prazo mistura naturalmente código-fonte, dados de jogo (datapack), banco de dados, documentação e ferramentas. Sem uma organização explícita, tudo isso vira um monólito confuso — dificultando build, revisão e onboarding. É preciso definir, de forma oficial, o papel de cada diretório de topo.

## Decisão

A estrutura de topo do repositório é a seguinte, e cada diretório tem responsabilidade única:

```
LineBR-Legacy/
├── source/              # Base de DESENVOLVIMENTO (aCis 409 oficial)
├── runtime-reference/   # Runtime original PRESERVADO (referência histórica)
├── database/            # Documentação e artefatos de banco
├── docs/                # Documentação técnica e decisões (ADR)
└── tools/               # Utilitários de desenvolvimento do projeto
```

### `source/`
Código-fonte oficial da aCis 409. **É o único lugar onde se desenvolve.**
- `aCis_gameserver/` — game + login + commons (Java) + `build.xml` + `config/` + `lib/`.
- `aCis_datapack/` — datapack (html, xml, sql, tools) + `build.xml`.

### `runtime-reference/`
O runtime pack compilado original, **imutável**. Byte-a-byte idêntico à Base Zero (ver [ADR-001](ADR-001-base-oficial.md)). Protegido por `.gitattributes` (`-text`) para nunca sofrer normalização de EOL.
- Papéis: (1) preservar a Base Zero; (2) permitir comparar builds futuros contra o binário original; (3) permitir subir o servidor sem compilar, se necessário.
- **Regra:** nunca editar.

### `database/`
Documentação do banco e artefatos **de desenvolvimento** (migrações incrementais, dumps de teste, diagramas ER). O schema canônico permanece em `source/aCis_datapack/sql/` — este diretório **não duplica** a fonte da verdade.

### `docs/`
Toda a documentação técnica: arquitetura, build, workflow, filosofia, manifesto, roadmap e os **ADRs** (`docs/ADR/`).

### `tools/`
Utilitários **do projeto** (scripts de build/deploy, verificadores de integridade, automações). Não confundir com `source/aCis_datapack/tools/` (instaladores da aCis) nem `runtime-reference/tools/` (do pack original).

## Consequências

**Positivas**
- Fronteiras claras: código, dados, docs e tooling não se misturam.
- `runtime-reference/` isolado protege a Base Zero de qualquer edição acidental.
- Facilita CI, revisão e onboarding.

**Negativas / custos**
- Coexistência de dois `tools/` e dois conjuntos de `sql/` (source vs runtime) exige atenção — mitigado por documentação explícita.

## Alternativas consideradas

- **Manter só a source, descartando o runtime** — rejeitada: perderia a prova de equivalência e a Base Zero.
- **Colocar datapack e database fora de `source/`** — rejeitada: o datapack e o SQL fazem parte da aCis e devem versionar junto da source que os consome.
