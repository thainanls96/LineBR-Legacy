# Filosofia de Progressão — LineBR Legacy

> Por que cada mecanismo de progressão existe e o que ele deve custar.
> ⚠️ **Tudo aqui depende de [D-001 (rates)](DECISION_LOG.md).** **Fato (EV-001/EV-002):** base atual = **x1** em XP, SP, Adena, Drop, Spoil.

---

## Princípio regente
**Progressão é a moeda do tempo do jogador.** Cada mecanismo abaixo troca *tempo/risco/cooperação* por *poder*. Quando um mecanismo dá poder sem cobrar nada, ele não "ajuda o jogador" — ele **desvaloriza o que os outros pagaram**.

---

## XP
- **Papel:** medir tempo investido; controlar o ritmo do mundo.
- **Design retail:** curva cruel, especialmente 52–61 e 75+.
- **Por que preservar a dureza:** a lentidão é o que dá **peso** ao nível. Level 80 num servidor x1 é biografia; num x100 é terça-feira.
- **Perda de XP na morte:** é o que faz o risco existir ([P-14](DESIGN_PRINCIPLES.md)). Remover = remover a tensão do jogo inteiro.

## SP
- **Papel:** segunda moeda de progressão; força escolhas (quais skills subir primeiro).
- **Por que importa:** SP escasso cria **build**, não checklist. Com SP abundante, todo mundo tem tudo — e classes deixam de ter identidade.

## Drop
- **Papel:** motor da economia + recompensa de exploração.
- **Tensão fundamental:** drop generoso = economia inflada + regiões desertas ([P-02](DESIGN_PRINCIPLES.md), [P-04](DESIGN_PRINCIPLES.md)).
- **Regra:** drop é *faucet*. Cada ponto de rate é multiplicado por milhares de mobs/dia.

## Spoil
- **Papel:** razão de existir de uma classe inteira (Dwarf Scavenger).
- **Regra de ouro:** materiais relevantes devem vir **preferencialmente** de spoil. Se drop normal ou loja fornecerem o mesmo, o Dwarf morre e a economia perde o seu banco central ([P-05](DESIGN_PRINCIPLES.md)).

## Craft
- **Papel:** transformar material em poder; conectar jogadores.
- **Por que existe:** é o que torna a economia **interdependente**. Sem craft, cada jogador é uma ilha.
- **Requisito:** craft precisa ser a via **principal** de equipamento — não a loja, não o drop pronto.

## Enchant
- **Papel duplo:** progressão vertical **e** o maior **dreno** da economia.
- **Por que a quebra importa:** o item destruído é o que impede o acúmulo infinito. É o único mecanismo que **remove** riqueza do mundo em escala.
- **Emoção:** medo + cobiça ([GAME_PHILOSOPHY §3](GAME_PHILOSOPHY.md)). Enchant sem risco é só um botão.

## Economia
- Ver [ECONOMY_PHILOSOPHY](ECONOMY_PHILOSOPHY.md). Resumo: **faucets ≤ sinks**, sempre; medir antes de mexer.

## Raid Boss
- **Papel:** progressão em grupo + cobiça + agenda social (o boss cria compromisso entre pessoas).
- **Por que preservar a escassez:** boss trivial = item trivial = economia trivial ([P-03](DESIGN_PRINCIPLES.md)).

## Seven Signs
- **Papel:** o mecanismo que transforma progressão **individual** em **política coletiva**.
- **Por que é especial:** é um dos designs mais originais do L2 — e um dos primeiros a ser desligado/quebrado em servidores privados, por ser "complicado".
- **Nossa posição:** manter, mesmo que dê trabalho. É pilar de identidade do Interlude.

## Olympiad
- **Papel:** o único sistema de **mérito puro** (sem farm, sem sorte, sem clã).
- **Requisito:** noblesse — a barreira que torna o Olympiad de elite.
- **Ameaça:** qualquer vantagem comprável aqui destrói o sistema inteiro ([P-11](DESIGN_PRINCIPLES.md)).

## Hero
- **Papel:** o **topo visível** do servidor. Status social encarnado (aura, skills, canal).
- **Regra:** escassez absoluta ([P-07](DESIGN_PRINCIPLES.md)). Hero é o que o jogador de level 20 vê passar em Giran e pensa "um dia".
- **Se muitos são Hero, ninguém é.**

---

## O encadeamento (por que a ordem importa)
```
XP/SP  →  chegar aos níveis      (tempo)
Drop/Spoil  →  alimentar economia (mundo)
Craft  →  transformar em poder    (interdependência)
Enchant  →  arriscar por mais     (dreno + emoção)
Raid/Seven Signs  →  progressão coletiva (social)
Olympiad → Hero  →  mérito e status   (topo)
```
Cada elo depende do anterior. **Acelerar um elo quebra os seguintes**: rate de XP alta → pula-se drop/craft → economia sem base → equipamento sem valor → Olympiad decidido por quem farmou adena, não por skill.

> É por isso que **D-001 não é "uma configuração"** — é a decisão que define se este encadeamento existe ou não.

## Riscos declarados
| Risco | Gravidade |
|-------|:---------:|
| 🔴 Decidir rates sem entender o encadeamento acima | destrói craft/spoil/economia em cascata |
| 🔴 Reduzir penalidade de morte "para ser amigável" | remove o risco → remove a tensão → remove o jogo |
| 🟠 Enchant sem quebra | acúmulo infinito → inflação de itens |
| 🟠 Hero acessível demais | mata o topo aspiracional |
| 🟠 Seven Signs desligado "por simplicidade" | perde-se um pilar de identidade |
