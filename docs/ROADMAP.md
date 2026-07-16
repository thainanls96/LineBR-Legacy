# Roadmap — LineBR Legacy

Plano de evolução em fases. Cada fase concluída é registrada aqui (data + tag/commit) e, quando houver decisão arquitetural, um ADR.

> **Estado atual:** FASE 1 (Fundação) em conclusão — arquitetura e documentação sendo congeladas. Nenhuma revisão aplicada, nenhum código alterado.

---

## FASE 1 — Fundação  🟡 em andamento
Estabelecer a base profissional do projeto.
- [x] Importar runtime original (Base Zero) → tag `acis-409-runtime-base`.
- [x] Confirmar source oficial (Tryskell/aCis 409) e auditar correspondência com o runtime.
- [x] Migrar para estrutura de desenvolvimento (`source/`, `runtime-reference/`, `database/`, `docs/`, `tools/`).
- [x] Congelar arquitetura e padrões (ADR-001..005, Filosofia, Manifesto, Contributing, este Roadmap).
- [ ] Aprovação e merge da migração para `main` (aguarda o dono).

## FASE 2 — Correções oficiais
Aplicar as revisões oficiais da aCis, uma de cada vez, sobre `source/`.
- [ ] **409 → 410**: obter diff oficial, aplicar em `development/rev-410`, documentar changelog, tag `acis-410`.
- [ ] **410 → 411**: aplicar em `development/rev-411`, changelog, tag `acis-411`.
- Regra: nada de customs nesta fase (Retail First puro).

## FASE 3 — Build validado
Provar que a source compila e roda.
- [ ] Ambiente de build: **JDK 21 + Apache Ant**.
- [ ] Compilar gameserver + loginserver + datapack.
- [ ] Servidor sobe (login + game) contra MariaDB local.

## FASE 4 — Comparação com o runtime
Garantir equivalência com o binário original.
- [ ] Comparar o `l2jserver.jar` compilado (rev 409) com `runtime-reference/` (classes/estrutura).
- [ ] Documentar quaisquer diferenças esperadas (timestamps/ordem) vs. inesperadas.

## FASE 5 — Infraestrutura
Preparar hospedagem profissional.
- [ ] VPS: usuário de app não-root, MariaDB dedicado, HexID/porta 9014 em `127.0.0.1`, firewall (2106/7777 públicas).
- [ ] CI (build automático), backups automatizados do `l2jdb`/datapack, deploy reproduzível.

## FASE 6 — Servidor de testes
Ambiente interno para validar comportamento.
- [ ] Deploy de staging; testes de gameplay retail (spawns, quests, sieges, economia).
- [ ] Correções de bugs encontrados (documentadas).

## FASE 7 — Beta fechado
Validação com jogadores convidados.
- [ ] Grupo restrito; coleta de feedback; observabilidade (logs/métricas).
- [ ] Ajustes de estabilidade e balanceamento retail.

## FASE 8 — Lançamento
Abertura pública.
- [ ] Hardening final de segurança e performance.
- [ ] Site, comunicação, políticas.
- [ ] Go-live e monitoramento contínuo.

---

### Camada de customizações (pós-fundação)
As customizações do LineBR (opcionais, Retail First) entram **somente após** a base 411 estar validada, como `LineBR Patch 001, 002, …` (ver [ADR-004](ADR/ADR-004-estrategia-versionamento.md)) — cada uma opcional, justificada e reversível.
