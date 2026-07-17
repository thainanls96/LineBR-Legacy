# Princípios Permanentes de Design — LineBR Legacy

> Princípios que **não mudam**. Alterá-los exige ADR que os supere explicitamente + aprovação do dono.
> Servem como **teste** para qualquer proposta futura: se a proposta fere um princípio, ela é recusada — mesmo que pareça boa.

---

## Os princípios

### P-01 · Toda quest deve ter propósito
Uma quest existe para dar XP, item, acesso, dinheiro **ou** história. Quest que não entrega nada disso é ruído — mas **não a removemos**: se o retail a tinha, ela fica (Retail First). O propósito pode ser fraco; a existência é do retail, não nossa.

### P-02 · Todo mapa deve importar
Cada região precisa de uma razão para o jogador ir até lá. Se uma região do Interlude estiver morta no nosso servidor, a causa é **nossa** (rates, drops, economia distorcida) — e o problema é essa causa, não o mapa.

### P-03 · Todo boss deve importar
Boss é evento, não conteúdo de rotina. Se matar um boss vira trivial, perdemos um pilar da cobiça e da economia.

### P-04 · Toda Adena deve importar
Adena precisa ser escassa o bastante para que 1 adena a mais seja um motivo para jogar. Adena abundante mata drop, craft, spoil, mercado e o próprio sentido de caçar.

### P-05 · Todo Craft deve importar
Se comprar for sempre melhor que craftar, o Dwarf vira NPC. O craft é o coração da economia do Interlude.

### P-06 · Toda Party deve importar
O L2 foi desenhado para ser jogado em grupo. Se solo for sempre igual ou melhor, o jogo social morre — e com ele o servidor.

### P-07 · Todo Hero deve ser admirado
Hero é escasso por design. Se muitos são Hero, ninguém é. A aura tem que significar algo quando passa na cidade.

### P-08 · Nada deve existir apenas por existir
Nenhuma feature entra "porque é legal". Toda adição responde: que emoção ela serve? que princípio ela fortalece? — Se a resposta é "nenhuma", ela não entra.

### P-09 · Nenhuma feature pode destruir a economia
Economia é o sistema mais frágil e o menos reversível. Um erro de economia leva meses para aparecer e não se conserta sem wipe. Na dúvida sobre impacto econômico: **não implementar**.

### P-10 · Nenhuma feature pode diminuir a importância da exploração
Teleporte fácil, mapas resumidos, atalhos e "conveniências" encolhem o mundo. O mundo grande e perigoso **é** o produto.

### P-11 · Nenhuma feature pode incentivar Pay-to-Win
Dinheiro nunca compra poder, progresso, vantagem competitiva ou tempo de jogo relevante. Sem exceções, sem "só cosmético que dá stat", sem "só um pouquinho".

### P-12 · O ônus da prova é de quem muda
Retail First operacional: sem evidência ≥ ★★★★, não muda ([EVIDENCE_LEVELS](../knowledge/methodology/EVIDENCE_LEVELS.md)).

### P-13 · O tempo do jogador é sagrado
Sem wipes por conveniência, sem mudanças retroativas que anulem esforço, sem "recomeçar porque erramos". Se erramos, **nós** pagamos o custo — não ele.

### P-14 · A frustração faz parte
Não removemos a dureza do Interlude. Morrer, perder XP, falhar enchant e andar longe são **features**. O alívio só existe porque a dureza existe.

### P-15 · Regras não mudam ao sabor do humor
Toda regra é documentada, versionada e auditável. GM não interfere em economia, ranking ou PvP. Nunca.

---

## Como usar (teste de proposta)

Toda proposta futura deve passar por este teste, em ordem:
```
1. Fere algum princípio P-01..P-15?          → SIM: recusada.
2. É Retail First (ADR-003)?                 → NÃO: só se opcional/problema comprovado/infra.
3. Tem evidência ≥ ★★★★ (se muda gameplay)?  → NÃO: vira pesquisa, não implementação.
4. Passa nos 6 critérios da CHANGE_ACCEPTANCE_POLICY? → NÃO: recusada.
5. Qual emoção (GAME_PHILOSOPHY §3) ela serve?       → nenhuma: recusada (P-08).
```

## Conflitos entre princípios
Quando dois princípios colidirem, a ordem de prevalência é:

**P-11 (anti-P2W) > P-13 (tempo do jogador) > P-09 (economia) > P-12 (ônus da prova) > demais**

Motivo: P2W e quebra de confiança **matam o servidor de vez**; erro de economia é grave mas corrigível com tempo; os demais são recuperáveis.

> Toda resolução de conflito vira entrada no [DECISION_LOG](../design/DECISION_LOG.md).
