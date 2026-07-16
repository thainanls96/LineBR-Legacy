# Contribuindo com o LineBR Legacy

Mesmo com um único desenvolvedor hoje, seguimos processo profissional desde o dia zero. Estas regras valem para qualquer pessoa que venha a contribuir.

## Antes de tudo, leia
- [PROJECT_PHILOSOPHY.md](PROJECT_PHILOSOPHY.md) e [LINEBR_MANIFESTO.md](LINEBR_MANIFESTO.md) — a alma do projeto.
- [ADR-003 (Retail First)](ADR/ADR-003-retail-first.md) — o filtro de toda mudança.
- [ADR-005 (Política de Desenvolvimento)](ADR/ADR-005-politica-desenvolvimento.md) — as regras abaixo em forma de decisão.

## Padrão de commits (Conventional Commits)
Formato: `tipo(escopo): descrição` (imperativo, curto). Corpo opcional explicando *por quê*.

| Tipo | Uso |
|------|-----|
| `feat` | nova funcionalidade (fase de customs) |
| `fix` | correção de bug |
| `docs` | documentação |
| `chore` | estrutura, tooling, manutenção |
| `build` | build, dependências, Ant |
| `refactor` | refatoração sem mudança de comportamento |
| `perf` | performance |
| `test` | testes |

Exemplos: `docs(adr): add versioning strategy` · `fix(login): restrict hexid port to localhost`.

**Regras:** commits **pequenos e atômicos** (uma mudança lógica cada); mensagens descritivas; nada de "misc/updates".

## Fluxo Git
1. Nunca trabalhar na `main`. Criar branch a partir da branch de trabalho vigente:
   - `development/*` — revisões oficiais/migrações;
   - `feature/*` — customizações LineBR;
   - `fix/*` — correções.
2. Fazer commits pequenos e descritivos.
3. Abrir **Pull Request** para revisão (nunca push direto na `main`).
4. Após aprovação, merge; taggear quando for uma revisão/patch (ver [ADR-004](ADR/ADR-004-estrategia-versionamento.md)).

## Revisão
Todo PR é revisado (mesmo pelo próprio autor, como checkpoint consciente): verifica-se aderência ao Retail First, tamanho/clareza dos commits, documentação presente e reversibilidade.

## Branches — resumo
| Branch | Propósito |
|--------|-----------|
| `main` | Base Zero / releases. Protegida. Só via PR aprovado. |
| `development/source-migration` | Migração de estrutura + source oficial (atual). |
| `development/rev-4XX` | Revisões oficiais da aCis. |
| `feature/<nome>` | Customizações LineBR (fase futura). |
| `fix/<nome>` | Correções pontuais. |

## Documentação
- Mudança arquitetural → **novo ADR** em `docs/ADR/`.
- Revisão/patch aplicado → atualizar `docs/ROADMAP.md` + changelog + tag.
- Mudança estrutural → atualizar `docs/Repository-Structure.md`.
- Código não trivial → comentários no estilo da aCis.

## Testes e validação (fases de código)
Antes de integrar código:
- compilar com **JDK 21 + Apache Ant** (ver [Build.md](Build.md));
- validar que login e gameserver sobem;
- quando aplicável, comparar o `l2jserver.jar` gerado com `runtime-reference/`.

## O que NÃO fazer
- Alterar `runtime-reference/` (é imutável).
- Mover/apagar a tag `acis-409-runtime-base`.
- Introduzir Pay-to-Win ou customs que alterem gameplay sem enquadrar-se no [ADR-003](ADR/ADR-003-retail-first.md).
- Commitar segredos (senhas, tokens, HexID de produção).
