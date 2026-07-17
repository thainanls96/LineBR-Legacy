# ADR-005 — Política de Desenvolvimento

- **Status:** Aceito
- **Data:** 2026-07-15
- **Decisores:** Thainan Lima

## Contexto

Mesmo sendo (hoje) um projeto de um único desenvolvedor, o LineBR Legacy é planejado para durar anos. Práticas de engenharia disciplinadas desde o início evitam dívida técnica, tornam o histórico útil e permitem que colaboradores entrem no futuro sem atrito. É preciso oficializar a forma de trabalhar.

## Decisão

Ficam definidas as seguintes políticas obrigatórias:

### 1. Commits pequenos e atômicos
Cada commit representa **uma** mudança lógica coerente. Nada de "commitão" com dez assuntos. Isso torna revisão, `revert` e `bisect` viáveis.

### 2. Commits descritivos (Conventional Commits)
Formato `tipo(escopo): descrição`, com corpo quando necessário:
- `feat` · `fix` · `chore` · `docs` · `build` · `refactor` · `perf` · `test`
- Exemplos: `docs(adr): add retail-first`, `chore(structure): move runtime to runtime-reference`.

### 3. Feature branches
Nunca trabalhar direto na `main`. Cada frente em sua branch:
- `development/*` para revisões oficiais e migrações;
- `feature/*` para customizações LineBR;
- `fix/*` para correções.

### 4. Revisão obrigatória
Toda integração à `main` passa por **Pull Request** revisável — mesmo sendo um só desenvolvedor, o PR serve de checkpoint consciente e registro. **Nenhum push direto na `main`.**

### 5. Documentação obrigatória
Nenhuma mudança arquitetural sem ADR. Nenhuma revisão/patch sem changelog e atualização de roadmap. Código não trivial recebe comentários no padrão da aCis.

### 6. Alterações reversíveis
Toda mudança deve poder ser desfeita: preferir alterações aditivas e configuráveis; customizações opcionais e desligáveis (ver [ADR-003](ADR-003-retail-first.md)); nunca reescrever a Base Zero.

### 7. Testes e validação
Antes de integrar mudanças de código (nas sprints futuras): compilar (JDK 21 + Ant), validar que o servidor sobe, e comparar builds contra `runtime-reference/` quando aplicável. Nesta fase (documentação) não há código a testar.

## Consequências

**Positivas**
- Histórico limpo e navegável; regressões fáceis de isolar.
- Base pronta para receber colaboradores sem retrabalho de processo.
- Segurança: mudanças sempre reversíveis e revisadas.

**Negativas / custos**
- Mais cerimônia por mudança (PR, changelog, ADR) — aceitável e compensado pela sustentabilidade.

## Alternativas consideradas

- **"Commitar direto na main, é só um dev"** — rejeitada: cria hábito ruim, histórico inútil e risco à Base Zero.
