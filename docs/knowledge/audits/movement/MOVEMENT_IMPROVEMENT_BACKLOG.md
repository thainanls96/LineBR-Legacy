# Movement — Backlog priorizado (aCis 409 → Retail)

> **ETAPA 7. Nenhuma implementação.** Lista priorizada derivada de [MOVEMENT_L2OFF_DIFFERENCES.md](MOVEMENT_L2OFF_DIFFERENCES.md) e [MOVEMENT_RISKS.md](MOVEMENT_RISKS.md).
> Prioridade = (impacto para o jogador) × (confiança na evidência) ÷ (risco + complexidade).

---

## Backlog

| # | Item | Ref | Impacto p/ jogador | Complexidade | Risco | Dependências | Prioridade |
|---|------|-----|--------------------|--------------|-------|--------------|:----------:|
| **B-01** | **Obter e habilitar a geodata (formato L2OFF)** | D-07 | 🔥 **Altíssimo** — sem ela não há pathfinding nem colisão de terreno | Baixa (operacional) | Baixo (é dado, não código) | Arquivos de geodata Interlude; `geoengine.properties` | **P0** |
| **B-02** | **Validar movimento contra um L2OFF de referência** (captura de pacotes / servidor PTS) | metodologia | 🔥 Alto — sem isso, todo "retail fix" é palpite | Média | Baixo (só medir) | Acesso a L2OFF/PTS Interlude | **P0** |
| **B-03** | **Reavaliar o bloqueio de movimento por teclado** | D-01 | 🔥 Alto — jogadores de teclado não andam | **Baixa** (1 `if`) | 🟠 Alto (anti-bot: existe por um motivo) | Decisão de produto + política anti-bot | **P1** |
| **B-04** | Unificar a matemática de tick Player × NPC (tempo real vs `speed/10`) | D-03, D-11 | Médio — NPCs lentos sob carga | Média | 🔴 **Crítico** (hot path) | Nenhuma | **P2** |
| **B-05** | Investigar o "Falling/Climb bug" de Z (`|ΔZ|>100`) | D-14 | Médio-Alto — personagem escala/cai indevidamente | Alta | 🔴 Crítico (GeoEngine) | **B-01** (precisa de geodata p/ reproduzir) | **P2** |
| **B-06** | Revisar granularidade do follow (1 s) | D-08 | Médio — perseguição "aos saltos" no PvP | Média | 🟠 Alto (combate + carga) | **B-02** (validar retail) | **P3** |
| **B-07** | Revisar o `+50` de raio para NPC vs alvo em movimento | D-09 | Médio — mobs alcançam quem foge | Baixa | 🟠 Alto (afeta PvE) | **B-02** | **P3** |
| **B-08** | Revisar o arranque "walk nos 5 primeiros ticks" | D-04 | Médio — micro-posicionamento PvP | Baixa | 🟠 Alto (gameplay) | **B-02** | **P3** |
| **B-09** | Revisar tolerância de desync (`dist > moveSpeed`) | D-02 | Médio — rubber-banding vs anti-cheat | Média | 🟠 Alto (segurança) | **B-02** | **P4** |
| **B-10** | Revisar constantes mágicas (9900, `-20` água, 500 barco) | D-05, D-12, D-13 | Baixo | Baixa | 🟡 Médio | **B-02** | **P4** |
| **B-11** | Padronizar arredondamento (`Math.round` vs `(int)`) | D-11 | Baixo (consistência interna) | Baixa | 🔴 Crítico (hot path) | **B-04** | **P5** |

## Leitura do backlog

**P0 — pré-requisitos, não são "melhorias".** Sem **geodata** (B-01) o sistema de movimento do LineBR não está sequer operando como a aCis pretende; e sem uma **referência L2OFF medível** (B-02) não há como afirmar que qualquer mudança aproxima do retail. **Nenhum item de P2+ deveria ser implementado antes de B-01 e B-02.**

**P1 — decisão de produto, não técnica.** O bloqueio de teclado (B-03) é trivial de remover (um `if`), mas existe como **anti-bot**. É uma escolha entre *fidelidade retail* e *proteção contra L2Walker* — cabe ao dono, e deve virar um **ADR** (ver [ADR-003 Retail First](../../../adr/ADR-003-retail-first.md), critério "opcional").

**P2+ — só com evidência.** Todos dependem de medição contra o retail ou de geodata para reprodução. Implementar por opinião violaria o Manifesto e o ADR-003.

## Regra de ouro para este backlog
Nenhum item entra em implementação sem:
1. **Evidência** (🟢/🟡, nunca só 🔴);
2. **ADR** quando alterar gameplay (ADR-003 exige: opcional **ou** problema comprovado **ou** infra sem tocar gameplay);
3. Fluxo `Modificar → Compilar → Runtime Validation → Logs → Relatório → Commit` (ADR-005), **um item por vez**.
