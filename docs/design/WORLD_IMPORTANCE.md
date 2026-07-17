# Importância do Mundo — LineBR Legacy

> Por que cada região existe e o que ela deve significar na vida do jogador.
> ⚠️ **Evidência ★☆☆☆☆–★★☆☆☆** — descrições de conhecimento geral do Interlude, **não validadas**. Intenção de design, não referência técnica.
> **Princípio regente:** [P-02](../constitution/DESIGN_PRINCIPLES.md) — *todo mapa deve importar*. Região morta = sintoma de erro nosso (rates/economia), não do mapa.

---

## Vilas iniciais (Talking Island · Elven · Dark Elven · Orc · Dwarven)
| | |
|---|---|
| **Por que ir** | Nascimento; identidade de raça; primeiras quests |
| **Quando** | 1–20 |
| **Recompensa** | Equipamento inicial, aprendizado, 1ª profissão |
| **Economia** | Nenhuma (consumo puro) |
| **Progressão** | Fundamental — é o funil de entrada |
| **Risco de morrer** | Se o novato não for guiado, ele sai. Retenção começa aqui |

## Gludio / Gludin
**Por que ir:** primeira cidade "de verdade"; hub de saída do berço · **Quando:** 15–30 · **Economia:** primeiro mercado real, primeiro contato com Dwarf · **Progressão:** transição do tutorial para o mundo.

## Dion
**Por que ir:** faixa 25–40; Cruma nas redondezas · **Economia:** materiais de C-grade · **Progressão:** rumo à 2ª profissão.

## **Giran** ⭐ (o coração)
| | |
|---|---|
| **Por que ir** | **É o mercado.** O ponto de encontro social do servidor |
| **Quando** | do 40 até sempre |
| **Recompensa** | comércio, clã, vida social |
| **Economia** | 🔴 **Máxima.** Giran vazia = servidor morto. É o termômetro nº 1 |
| **Progressão** | indireta, mas essencial |
> **Se Giran não estiver cheia, algo está errado** — não com Giran, mas com a economia ou a população.

## Cruma Tower
**Por que ir:** XP de 40–52; materiais · **Recompensa:** progressão no "muro" · **Economia:** materiais de craft.

## Oren
**Por que ir:** faixa 50–60; acesso a regiões de elite · **Economia:** média-alta.

## **Dragon Valley**
**Por que ir:** XP e drop da faixa 55–65; um dos lugares mais lembrados do Interlude · **Recompensa:** alta, com risco alto · **Economia:** materiais e itens cobiçados · **Progressão:** atravessar o muro.

## Aden
**Por que ir:** capital; castelo; hub de end game · **Economia:** alta · **Progressão:** política de clãs.

## Rune / Goddard
**Por que ir:** end game (75+); castelos · **Economia:** elite.

## Hot Springs
**Por que ir:** XP de topo com mecânica própria (debuffs característicos) · **Quando:** 75+.

## Imperial Tomb / Forge of the Gods (FOG) / Wall of Argos
**Por que ir:** XP/drop de elite 75+ · **Economia:** itens de topo · **Progressão:** A/S-grade.

## Tower of Insolence (TOI)
**Por que ir:** XP 60+; raids · **Economia:** alta.

## Pagan Temple
**Por que ir:** conteúdo 70+, acesso restrito · **Recompensa:** itens específicos.

## **Catacombs / Necropolis** ⚠️
| | |
|---|---|
| **Por que ir** | Seven Signs — progressão **e** política de servidor |
| **Quando** | ~55+ |
| **Economia** | ligada ao ciclo de Seven Signs (buffs, acesso, benefícios coletivos) |
| **Nota técnica** | ⚠️ **não são um "sistema" na aCis** — vivem no datapack + `SevenSignsManager` + `DungeonGatekeeper`/`DungeonTeleporter` ([SYSTEM_CATALOG F06](../knowledge/baseline/SYSTEM_CATALOG.md)) |
> Seven Signs é o mecanismo que transforma farm individual em **política coletiva** — é design brilhante e frequentemente quebrado em servidores privados.

## Ilhas / regiões de boat (Talking Island ↔ Giran ↔ Gludin)
**Por que ir:** deslocamento; imersão · **Risco:** se teleporte for barato demais, o boat (e o mundo) somem → fere [P-10](../constitution/DESIGN_PRINCIPLES.md).

---

## O teste de saúde do mundo
Um mapa está saudável se **alguém está lá agora**, por vontade própria, sem ser forçado.

| Sintoma | Diagnóstico provável |
|---------|----------------------|
| Só a cidade tem gente | rates altas demais (não precisa caçar) ou população baixa |
| **Giran vazia** | economia quebrada ou servidor morrendo |
| Regiões de 40–60 desertas | jogadores pulam a faixa (rates) ou não chegam lá (retenção) |
| Todos no mesmo spot | um lugar é bom demais → desequilíbrio de drop/XP |
| Ninguém em Catacombs | Seven Signs sem relevância → perda de um pilar |

> **Nenhum destes se resolve mexendo no mapa.** Resolvem-se na economia, nas rates e na população. Mapa é sintoma; economia é causa.

## Riscos declarados
- 🔴 **Teleporte barato encolhe o mundo** — o custo de deslocamento é o que dá **tamanho** ao mundo ([P-10](../constitution/DESIGN_PRINCIPLES.md)).
- 🔴 **Rates altas matam regiões inteiras** — o jogador nunca precisa ir a metade do mapa. Depende de [D-001](DECISION_LOG.md).
- 🟠 **População baixa mata mapas antes da economia** — 30 jogadores não preenchem o Interlude. É um mundo desenhado para milhares.
