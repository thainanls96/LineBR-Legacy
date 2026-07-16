# Comportamentos Desconhecidos — LineBR Legacy

> **Jamais esconder incertezas.** Este documento é o inventário honesto do que **não sabemos** sobre o Interlude Retail.
> Um item só sai daqui quando uma evidência (`EV-NNN`) o resolve — nunca por opinião ou cansaço.

---

## Como ler
Cada item tem **Sistema · Descrição · Impacto · Prioridade · Como provar**.
**Prioridade** = quanto o desconhecimento **bloqueia** o projeto (não quanto incomoda).

---

## 🚧 Incógnitas estruturais (bloqueiam o projeto inteiro)

### U-001 · Não temos nenhuma referência retail medível
- **Sistema:** todos
- **Descrição:** o projeto não possui cliente oficial, servidor L2OFF/PTS, nem capturas. Logo, **nenhuma** afirmação sobre o retail pode chegar a ★★★★.
- **Impacto:** 🔴 **Máximo** — trava toda alteração de gameplay (por política).
- **Prioridade:** **P0**
- **Como provar:** obter cliente oficial Interlude e/ou servidor L2OFF/PTS de referência; montar captura de pacotes. Ver [EVIDENCE_REGISTER](EVIDENCE_REGISTER.md#evidências-desejadas-lacunas-prioritárias).

### U-002 · Geodata Interlude ausente
- **Sistema:** B01 GeoData, B02 Pathfinding, B03 Movement, B04 Collision
- **Descrição:** a aCis lê geodata no formato **L2OFF** (`GeoDataType = L2OFF`), mas o LineBR **não possui os arquivos** — pathfinding e colisão de terreno não operam.
- **Impacto:** 🔴 **Máximo** — o servidor não se comporta nem como a aCis pretende, quanto mais como retail.
- **Prioridade:** **P0**
- **Como provar:** obter os arquivos de geodata Interlude (formato L2OFF), habilitar as 139 regiões e revalidar o runtime.

### U-003 · Quais sistemas da aCis existiam no retail?
- **Sistema:** todos (ex.: H07 Wedding/Couple, D05 Enchant Skill, F07 Derby Track)
- **Descrição:** o catálogo prova o que **a aCis tem**. Não sabemos, sistema a sistema, o que era **retail Interlude**, o que era de outra chronicle, e o que a aCis adicionou.
- **Impacto:** 🟠 Alto — "Retail First" exige saber o que é retail.
- **Prioridade:** **P1**
- **Como provar:** patch notes NCSoft da época (Wayback) + cliente oficial (existência de UI/strings).

---

## Movement (B03) — derivadas da Sprint 004

### U-010 · O retail aceitava movimento por teclado?
- **Descrição:** a aCis **bloqueia** (`_moveMovement == 0` → `ActionFailed`). O cliente Interlude **envia** o pacote com `0` ao usar setas — logo o modo existe no protocolo. O que o servidor retail fazia com ele é desconhecido.
- **Impacto:** 🟠 Alto — jogadores de teclado simplesmente não andam.
- **Prioridade:** **P1**
- **Como provar:** captura de pacotes contra servidor L2OFF usando as setas; ou vídeo verificável de 2007 com movimento por teclado.

### U-011 · Qual era a granularidade do tick de movimento no retail?
- **Descrição:** aCis usa 100 ms fixo. Retail desconhecido.
- **Impacto:** 🟡 Médio — afeta suavidade e precisão percebidas.
- **Prioridade:** P3
- **Como provar:** captura de pacotes (frequência de `MoveToLocation`/`ValidatePosition`).

### U-012 · O retail tinha o "arranque andando" (walk antes de run)?
- **Descrição:** aCis usa velocidade de caminhada nos **5 primeiros ticks**. Parece emular o retail, mas o valor (5) não tem fonte.
- **Impacto:** 🟡 Médio — micro-posicionamento em PvP.
- **Prioridade:** P3
- **Como provar:** medir a curva de deslocamento inicial em referência retail.

### U-013 · Qual a autoridade de posição no retail (cliente × servidor)?
- **Descrição:** aCis é 100% server-authoritative (só corrige o cliente se `desync > moveSpeed`). Relatos dizem que o retail "parecia" mais responsivo — sem prova.
- **Impacto:** 🟠 Alto — define a sensação do jogo e a superfície anti-cheat.
- **Prioridade:** P2
- **Como provar:** captura de pacotes: observar se o servidor retail adota a posição do cliente.

### U-014 · O limite de 9900 por clique é retail?
- **Descrição:** cap na aCis (`MoveBackwardToLocation:110`). Provável anti-cheat próprio.
- **Impacto:** 🟢 Baixo
- **Prioridade:** P4
- **Como provar:** clicar além de 9900 em referência retail e observar.

### U-015 · O "+50 de raio para NPC vs alvo em movimento" é retail?
- **Descrição:** heurística da aCis (`CreatureMove:400-401`), aparentemente anti-kiting.
- **Impacto:** 🟡 Médio — PvE (mobs alcançam quem foge).
- **Prioridade:** P3
- **Como provar:** medir alcance efetivo de mobs contra alvo em fuga em referência retail.

### U-016 · Qual o comportamento retail em terreno íngreme (bug de Z)?
- **Descrição:** o próprio autor da aCis registra *"Falling/Climb bug found"* quando `|ΔZ| > 100`. Não sabemos como o retail se comportava.
- **Impacto:** 🟠 Alto — personagem "escala"/"cai" indevidamente.
- **Prioridade:** P2 (depende de U-002 para reproduzir)
- **Como provar:** com geodata habilitada, comparar deslocamento em encosta contra referência retail.

---

## Combate / Skills / Economia (ainda não auditados)

### U-020 · Fórmulas de dano físico/mágico do retail
- **Sistema:** C03, C04 · **Impacto:** 🔴 Máximo (é o coração do jogo) · **Prioridade:** **P1**
- **Como provar:** patch notes + medição controlada (dano com stats fixos) em referência retail.

### U-021 · Taxas retail (XP/SP/Adena/Drop/Spoil) do Interlude
- **Sistema:** G05, G06, G13 · **Impacto:** 🔴 Máximo (economia = pilar do Manifesto) · **Prioridade:** **P1**
- **Como provar:** patch notes NCSoft + tabelas oficiais arquivadas.
- **Nota:** o runtime original do LineBR usava rates **mid** (XP/SP x20, Adena x10, Drop x5) — isso é **decisão do servidor anterior**, não retail.

### U-022 · Regras de stacking de buffs/debuffs no retail
- **Sistema:** D03, D04 · **Impacto:** 🟠 Alto · **Prioridade:** P2

### U-023 · Comportamento de aggro/hate no retail
- **Sistema:** E03 · **Impacto:** 🟠 Alto · **Prioridade:** P2

---

## Resumo
| Prioridade | Itens |
|:----------:|------:|
| **P0** (bloqueiam tudo) | 2 — U-001, U-002 |
| **P1** | 4 — U-003, U-010, U-020, U-021 |
| **P2** | 4 |
| **P3–P4** | 4 |
| **Total** | **14** |

> **Leitura honesta:** os dois itens P0 **não são de código** — são de **aquisição de evidência e de dados**. Enquanto não forem resolvidos, o projeto pode auditar e documentar (o que gera valor real), mas **não pode implementar** nada de gameplay sem violar a própria política.
