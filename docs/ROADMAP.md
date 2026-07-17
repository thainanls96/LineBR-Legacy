# Roadmap Oficial — LineBR Legacy

> Plano definitivo do projeto. Supera o roadmap original ([archive/ROADMAP.original.md](archive/ROADMAP.original.md)) e absorve o [ROADMAP_BASELINE](knowledge/baseline/ROADMAP_BASELINE.md) (que segue válido como ordem **interna** de auditorias).

---

## Visão geral

| Fase | Nome | Status |
|:----:|------|:------:|
| **1** | Fundação | ✅ **CONCLUÍDA** |
| **2** | Documentação | ✅ **CONCLUÍDA** (Sprint 010 — congelada) |
| **3** | Infraestrutura | 🔜 **PRÓXIMA** |
| **4** | Implementação | ⬜ |
| **5** | Testes | ⬜ |
| **6** | Balanceamento | ⬜ |
| **7** | Beta | ⬜ |
| **8** | Release | ⬜ |

---

## ✅ FASE 1 — Fundação (concluída)
- [x] Base Zero preservada (tag `acis-409-runtime-base`, commit `d7c8881`)
- [x] Source oficial aCis 409 adotada (`Tryskell/acis_public @ 55ff8a4e`)
- [x] Estrutura de repositório profissional (`source/` + `runtime-reference/`)
- [x] **Build validado** — 2.881/2.881 classes byte-idênticas ao runtime
- [x] **Runtime validado** — login + game operacionais, 0 erros
- [x] ADRs 001–005 congelados

## ✅ FASE 2 — Documentação (concluída — Sprint 010)
- [x] Metodologia de evidência (escala ★, política de aceitação)
- [x] Baseline Retail (63 sistemas catalogados, registro de evidências)
- [x] Auditoria de Movement (1º sistema)
- [x] Game Design Bible + Monetização
- [x] **LineBR Legacy Bible** (Constituição — 101 decisões)
- [x] **Consolidação documental** — 73 docs unificados, estrutura por autoridade, 0 links quebrados
- [x] **Documentação CONGELADA** ([DOCUMENTATION_POLICY](DOCUMENTATION_POLICY.md))

## 🔜 FASE 3 — Infraestrutura (próxima)
> Pré-requisitos técnicos. **Nada de gameplay ainda.**

- [ ] **🔴 Geodata Interlude** — obter e habilitar (formato L2OFF, 139 regiões)
      *Bloqueador crítico: sem ela não há pathfinding nem colisão* ([OD-01](specification/OPEN_DECISIONS.md))
- [ ] **Mesclar as branches na `main`** — hoje há 8 branches; PR #1 aberto desde a Sprint 002
- [ ] **ADRs das customs aprovadas** (VIP, Marketplace, Offline Shop, Hero Skin, Auto Loot, rates escalonadas) — exigidos pelo [ADR-003](adr/ADR-003-retail-first.md)
- [ ] CI de build (JDK 21 + Ant) no GitHub Actions
- [ ] Instrumentação de economia (medir faucet/sink) — infra, não gameplay
- [ ] VPS: usuário de app não-root, MariaDB dedicado, porta 9014 em `127.0.0.1`, firewall, backups

## ⬜ FASE 4 — Implementação
> Ordem por dependência ([DEPENDENCY_MAP](knowledge/baseline/DEPENDENCY_MAP.md)). **Uma custom por vez**, cada uma com Build → Runtime → Logs → Commit.

**4.1 — Configuração (zero custom)**
- [ ] Economia 1x (já é o nativo — apenas confirmar)
- [ ] `AutoLearnSkills = False` (já é o nativo)
- [ ] NPC Buffer nativo (`SchemeBuffer`) — level 🔴 pendente ([OD-02](specification/OPEN_DECISIONS.md))

**4.2 — Customs aprovadas**
- [ ] Rates escalonadas por faixa (3x/2x/1x/0.75x) — exige custom
- [ ] VIP (Bronze/Silver/Gold)
- [ ] Auto Loot por jogador (VIP Gold)
- [ ] Offline Shop
- [ ] Marketplace + taxas (nascem juntos)
- [ ] Hero Dynasty Skin — 🔴 depende de [OD-09](specification/OPEN_DECISIONS.md) (patch de cliente?)

## ⬜ FASE 5 — Testes
- [ ] Suite de validação por sistema
- [ ] Testes de carga
- [ ] Auditoria anti-dupe (obrigatória antes de abrir Marketplace/Trade)
- [ ] Validação de fluxo completo com cliente Interlude real

## ⬜ FASE 6 — Balanceamento
- [ ] Medir economia real (faucet × sink, adena em circulação, concentração)
- [ ] Validar a curva de rates na prática
- [ ] Ajustes **com dados**, nunca por opinião

## ⬜ FASE 7 — Beta
- [ ] Beta fechado (grupo restrito)
- [ ] Observabilidade (logs/métricas)
- [ ] Correções de estabilidade
- [ ] Definir política de punição, denúncia e moderação

## ⬜ FASE 8 — Release
- [ ] Hardening final (segurança/performance)
- [ ] Site, comunicação, políticas públicas
- [ ] Go-live e monitoramento

---

## Trilha paralela — Baseline (contínua, não bloqueia)
As auditorias dos 62 sistemas restantes seguem pela ordem do [ROADMAP_BASELINE](knowledge/baseline/ROADMAP_BASELINE.md): GeoData → Combat → Skills → AI → Economia → Conteúdo. **Não bloqueiam a Fase 3/4**, mas alimentam a qualidade de tudo.

## O gargalo real
> **A documentação não é mais o gargalo.** As três coisas que travam o projeto hoje são:
> 1. **Geodata** (dado — barato, impacto máximo)
> 2. **Merge das branches** (organização)
> 3. **Decisões pendentes do Owner** ([OPEN_DECISIONS](specification/OPEN_DECISIONS.md) — 16 itens)
