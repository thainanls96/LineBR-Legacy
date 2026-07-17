# Fluxo de Desenvolvimento — LineBR Legacy

## Princípios

1. **`main` é sagrada** — contém a Base Zero (runtime original, tag `acis-409-runtime-base`). Só recebe merges revisados e aprovados.
2. **Nunca trabalhar direto na `main`.**
3. **Uma mudança lógica por branch/commit** — rastreabilidade total.
4. **Preservar a filosofia da aCis** — sem customs até a base 409→410→411 estar consolidada.
5. **Tudo documentado** em `docs/`.

## Branches

| Branch | Propósito |
|--------|-----------|
| `main` | Base Zero (runtime). Protegida. |
| `development/source-migration` | Migração para estrutura de dev + source oficial 409 (**atual**). |
| `development/rev-410` | Aplicação da revisão oficial 410 (futuro). |
| `development/rev-411` | Aplicação da revisão oficial 411 (futuro). |
| `feature/<nome>` | Customizações do LineBR (VIP, Skins, Coins…), uma por branch (futuro). |

## Roadmap de revisões (ainda NÃO iniciado)

```
source aCis 409 (limpa)
      │
      ├─▶ development/rev-410   ← aplicar diff oficial 409→410 + recompilar
      │
      ├─▶ development/rev-411   ← aplicar diff oficial 410→411 + recompilar
      │
      └─▶ feature/*             ← reintroduzir customs LineBR sobre a 411
```

> As revisões 410/411 exigem os **diffs oficiais** da aCis, aplicados sobre `source/` e recompilados a cada passo. Nada disso é feito nesta fase.

## Convenção de commits

Formato: `tipo(escopo): descrição`

- `chore(structure): ...` — mudanças de estrutura/tooling
- `docs(...): ...` — documentação
- `feat(...): ...` — feature (só na fase de customs)
- `fix(...): ...` — correção
- `build(...): ...` — build/dependências

## Regras de merge

- Merge para `main` **somente com aprovação explícita do dono**.
- Preferir merges revisáveis (pull/merge request no GitHub) a push direto.
- **Nunca** apagar/mover a tag `acis-409-runtime-base`.

## Ambiente

- Working copy em caminho curto **fora do OneDrive** (`C:\dev\LineBR-Legacy`).
- `git config core.longpaths true` + `core.autocrlf false`.
- JDK 21 + Apache Ant para build (ver [Build.md](BUILD.md)).
