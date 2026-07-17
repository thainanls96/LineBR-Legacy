# Movement — Diferenças conhecidas aCis 409 × L2OFF Interlude

> **ETAPA 4.** Nada foi implementado. Cada item traz **nível de confiança** e **origem da evidência**.

---

## ⚠️ Aviso metodológico (leia antes de usar este documento)

A pesquisa por documentação técnica pública do **L2OFF Interlude** foi realizada e o resultado é honesto e desconfortável: **não existe especificação pública do comportamento do L2OFF**. Os canais históricos ou estão mortos (ex.: o fórum do L2J — `l2jserver.com/forum` — hoje **não resolve**, o domínio redireciona para fora), ou são fóruns de compartilhamento sem material técnico verificável.

**Consequência prática:** só existe **um tipo de evidência de confiança ALTA** para este projeto — **o próprio código da aCis** (incluindo os comentários dos autores, que declaram intenção retail). Tudo que vier de "lore de comunidade" é **MÉDIO/BAIXO** e **não deve** justificar mudança de gameplay sem validação empírica contra um servidor L2OFF real.

**Legenda de confiança**
- 🟢 **ALTO** — comprovado no código-fonte auditado (arquivo:linha) ou em comentário explícito do autor.
- 🟡 **MÉDIO** — comportamento tecnicamente plausível/derivável, mas sem fonte primária do L2OFF.
- 🔴 **BAIXO** — relato de comunidade / memória coletiva, sem evidência verificável.

---

## D-01 · Movimento por teclado (setas) é bloqueado — 🟢 **ALTO**
**Fato (código):** `MoveBackwardToLocation.java:45,68`
```java
_moveMovement = readD(); // is 0 if cursor keys are used 1 if mouse is used
...
// Deny movement from arrow keys.
if (_moveMovement == 0) { player.sendPacket(ActionFailed.STATIC_PACKET); return; }
```
A aCis **recusa** qualquer movimento originado do teclado; só aceita clique de mouse (`1`).
**L2OFF:** o cliente Interlude **envia** o pacote com `0` ao usar as setas — ou seja, o cliente suporta o modo, e o retail o processa. 🟡 (a existência do campo e o comentário do próprio autor comprovam o modo; o processamento retail é inferência).
**Natureza:** provável decisão **anti-bot/anti-L2Walker** da aCis (o mesmo packet tem `Config.L2WALKER_PROTECTION`), não fidelidade retail.
**Impacto para o jogador:** ALTO e imediatamente perceptível (quem joga de teclado simplesmente não anda).

## D-02 · Posição: servidor 100% autoritativo — 🟢 **ALTO**
**Fato (código):** `ValidatePosition.java:73-80` — no fluxo normal a posição enviada pelo cliente **nunca** é aplicada; serve só para medir desvio. Se `dist > moveSpeed` → `ValidateLocation` (corrige o cliente).
**Comentário do autor** (`CreatureMove.java:284-285`): *"the current server position can differ from the current client position… client send regularly a ValidatePosition packet to eventually correct the gap on the server. But, it's always the server position that is used in range calculation."*
**L2OFF:** 🔴 **BAIXO** — há relato consistente de comunidade de que o retail "sente" mais responsivo, o que sugere maior peso do cliente; **sem fonte verificável**.
**Impacto:** sensação de "borracha"/atraso quando há desvio.

## D-03 · Tick de movimento fixo de 100 ms — 🟢 **ALTO** (aCis)
**Fato:** `CreatureMove.java:221-234` — `ThreadPool.scheduleAtFixedRate(..., 100, 100)`.
**L2OFF:** 🔴 **BAIXO** — granularidade real do retail desconhecida publicamente.
**Nota técnica:** o Player compensa com tempo real (`Instant`), o NPC não (`speed/10` assume tick exato) → sob carga, **NPCs andam "devagar" e jogadores não**. Isso é um desvio **interno** da aCis, mensurável, independentemente do L2OFF. 🟢

## D-04 · Início do movimento anda antes de correr (5 ticks) — 🟢 **ALTO** (aCis)
**Fato:** `PlayerMove.java:246` + `PlayerStatus.java:958-961`
```java
getRealMoveSpeed(type != MoveType.FLY && _moveTimeStamp <= 5)
// isStillWalking → usa getBaseWalkSpeed() em vez de getBaseRunSpeed()
```
Os **5 primeiros ticks (~0,5 s)** usam velocidade de **caminhada** mesmo com "correr" ativo.
**L2OFF:** 🟡 **MÉDIO** — é uma emulação deliberada do "arranque" do retail; o valor exato (5 ticks) não tem fonte primária.
**Impacto:** afeta micro-posicionamento em PvP (kiting, primeiro passo).

## D-05 · Limite de 9900 unidades por clique — 🟢 **ALTO** (aCis)
**Fato:** `MoveBackwardToLocation.java:110` — alvo além de 9900 do ponto de origem → `ActionFailed`.
**L2OFF:** 🔴 **BAIXO** — limite retail desconhecido. Provável proteção anti-cheat da aCis.

## D-06 · Correção de Z pelo `collisionHeight` — 🟢 **ALTO** (aCis)
**Fato:** `MoveBackwardToLocation.java:93` — `_targetZ += player.getCollisionHeight();` ("floor level to head level").
**L2OFF:** 🟡 **MÉDIO** — correção necessária pela semântica do cliente; comportamento retail equivalente é plausível, sem fonte.

## D-07 · Geodata "L2OFF" mas ausente no LineBR — 🟢 **ALTO**
**Fato:** `geoengine.properties` → `GeoDataType = L2OFF`; a aCis lê o **formato de geodata do L2OFF**. Porém o runtime preservado do LineBR **não possui os arquivos** (lista de 139 regiões removida — ver [ENVIRONMENT_SETUP.md](../ENVIRONMENT_SETUP.md)).
**Consequência:** sem geodata → `findPath` inoperante → **sem pathfinding, sem colisão real de terreno**. Isso é, hoje, a **maior divergência prática** do LineBR para o retail — maior que qualquer detalhe de fórmula.
**Impacto:** ALTÍSSIMO (NPCs/jogadores atravessando obstáculos, Z incorreto, mobs "presos").

## D-08 · Follow com granularidade de 1 s — 🟢 **ALTO** (aCis)
**Fato:** `CreatureMove.java:539-543` — follow task a cada **1 s** (vs tick de movimento de 100 ms).
**L2OFF:** 🔴 **BAIXO**.
**Impacto:** MÉDIO — perseguição "aos saltos" e atraso ao reagir a alvo em fuga (perceptível em PvP/kiting).

## D-09 · NPC ganha +50 de raio se o alvo está em movimento — 🟢 **ALTO** (aCis)
**Fato:** `CreatureMove.java:400-401` — `if (_actor instanceof Npc) totalRadius += (target.isMoving() ? 50 : 0);`
**L2OFF:** 🔴 **BAIXO** — parece heurística anti-kiting da aCis; sem correspondência retail conhecida.
**Impacto:** MÉDIO (mobs "alcançam" um pouco mais quem foge).

## D-10 · Validação desligada durante queda — 🟢 **ALTO** (aCis)
**Fato:** `ValidatePosition.java:54-56` — `if (player.isFalling(_z)) return;` ("avoid jumping").
**L2OFF:** 🟡 **MÉDIO** — mitigação de artefato; comportamento retail não documentado.

## D-11 · Precisão divergente Player × NPC — 🟢 **ALTO** (aCis, desvio interno)
**Fato:** `PlayerMove.java:272-273` usa `Math.round(...)`; `CreatureMove.java:340-341` usa cast `(int)` (trunca). Mesma trajetória produz posições ligeiramente diferentes.
**L2OFF:** — (não aplicável; é inconsistência interna).
**Impacto:** BAIXO isolado, mas é *code smell* que dificulta reproduzir bugs.

## D-12 · Água (SWIM) com clamp de -20 — 🟢 **ALTO** (aCis)
**Fato:** `CreatureMove.java:319-324` / `PlayerMove.java:250-255` — se `getHeight(...) - waterZone.getWaterZ() < -20` → `maxZ = waterZone.getWaterZ()`. Player usa `getBaseSwimSpeed()` em água (`PlayerStatus.java:961`).
**L2OFF:** 🔴 **BAIXO** — constante `-20` sem fonte retail.

## D-13 · Boat suspende o movimento real — 🟢 **ALTO** (aCis)
**Fato:** `MoveBackwardToLocation.java:127-128` — comentário do autor: *"we don't want to schedule a real movement until he gets out of it otherwise GeoEngine will be confused"*. Tolerância de desync em barco = **500** (`ValidatePosition.java:66-70`).
**L2OFF:** 🔴 **BAIXO** — arquitetura retail de embarcações desconhecida.

## D-14 · "Falling/Climb bug" reconhecido pelo autor — 🟢 **ALTO**
**Fato:** `CreatureMove.java:380-381` / `PlayerMove.java:316-317` — debug avisa GM: *"Falling/Climb bug found when moving from…"* quando `|ΔZ| > 100` em GROUND.
**Leitura:** o próprio autor reconhece um artefato **conhecido e não resolvido** de Z em movimento. Provável divergência real do retail. 🟡 quanto ao comportamento L2OFF.
**Impacto:** MÉDIO-ALTO (personagem "escala"/"cai" indevidamente em terreno acidentado).

---

## Resumo por confiança
| Confiança | Itens |
|-----------|-------|
| 🟢 **ALTO** (código) | D-01, D-02, D-03, D-04, D-05, D-06, D-07, D-08, D-09, D-10, D-11, D-12, D-13, D-14 (fatos da aCis) |
| 🟡 **MÉDIO** | comportamento **retail** correspondente em D-01, D-04, D-06, D-10, D-14 |
| 🔴 **BAIXO** | comportamento **retail** em D-02, D-03, D-05, D-08, D-09, D-12, D-13 |

> **Conclusão honesta:** sabemos com precisão o que a **aCis faz** (🟢). O que o **L2OFF fazia** é, na maioria dos pontos, 🟡/🔴. Qualquer mudança "para ficar retail" exige **validação empírica** (servidor L2OFF de referência ou captura de pacotes histórica), sob pena de trocar um comportamento conhecido por um palpite.
