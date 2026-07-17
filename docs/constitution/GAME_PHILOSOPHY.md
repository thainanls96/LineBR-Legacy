# Filosofia de Game Design — LineBR Legacy

> **Autoridade máxima de design.** Toda alteração futura deve respeitar este documento.
> Responde *"como queremos que o jogador sinta o servidor?"* — não *"como o código funciona?"*.

---

## ⚠️ Aviso de escopo (leia primeiro)

Existe uma tensão real entre **ter um Game Design Bible** e **ser Retail First**: se reproduzimos o Interlude com fidelidade, **o game design já está decidido — é o da NCSoft, de 2007**. Não somos os designers deste jogo; somos seus **restauradores**.

Portanto, este documento **não desenha o jogo**. Ele faz três coisas legítimas:
1. **Explicita nossa intenção** ao restaurar (o que buscamos, o que recusamos);
2. **Documenta o entendimento** do design original (marcado com nível de evidência);
3. **Decide o que o retail não dita** — monetização, comunidade, operação, política do servidor.

Onde este documento tentar "melhorar o jogo", ele estará **violando o [ADR-003](../adr/ADR-003-retail-first.md)** — e deve ser corrigido, não obedecido.

---

## 1. Qual é o objetivo do LineBR Legacy?

**Reconstruir a experiência do Lineage II Interlude (2007) com a maior fidelidade tecnicamente comprovável, e mantê-la viva de forma sustentável por anos.**

Não é: fazer um Interlude "melhorado", "modernizado" ou "adaptado aos tempos atuais". Se o jogador quisesse um jogo moderno, ele jogaria um jogo moderno. Ele vem aqui porque quer **aquele** jogo.

## 2. Qual sensação queremos transmitir?

**Peso.** Cada coisa neste jogo deve custar algo — tempo, risco, cooperação ou escolha.

O Interlude é um mundo que **não facilita**. É lento, é duro, é injusto às vezes. E é exatamente daí que vem o valor: quando algo custa, ele significa. Um servidor que remove o custo remove o significado junto.

A sensação-alvo é a de **habitar um mundo**, não a de consumir conteúdo. O jogador não deve sentir que "está progredindo numa esteira" — deve sentir que está **vivendo em um lugar hostil e vasto** onde suas conquistas são dele.

## 3. Quais emoções o jogador deve sentir?

| Emoção | Quando | Por que preservá-la |
|--------|--------|---------------------|
| **Tensão** | ao caçar longe da vila, ao ver um nome vermelho | o risco é o que dá sabor à segurança |
| **Orgulho** | ao alcançar 76, ao vestir um set, ao virar Hero | conquistas caras são as únicas que orgulham |
| **Pertencimento** | no clã, na party, na aliança | o L2 é um jogo social disfarçado de RPG |
| **Cobiça** | ao ver um item raro, um boss, um castelo | o desejo move a economia |
| **Medo (saudável)** | ao arriscar enchant, ao entrar em PvP | perder precisa ser possível |
| **Frustração (dosada)** | ao falhar, ao morrer, ao perder XP | sem frustração não há alívio |
| **Admiração** | ao ver um Hero passar | o topo precisa ser visível e raro |

> **Nota honesta:** frustração é parte do design original. Um servidor que elimina toda frustração elimina também o alívio, o orgulho e a admiração — porque são a mesma moeda.

## 4. Por que alguém jogaria o nosso servidor em vez de outro?

Não por termos mais features. **Por termos menos.**

O diferencial pretendido é **confiança**:
- **É o Interlude de verdade** — não uma interpretação com "melhorias" que ninguém pediu.
- **As regras não mudam ao sabor do humor do dono.** Elas estão documentadas, versionadas e auditáveis (ADRs, baseline, evidências).
- **Ninguém compra poder.** O ranking reflete esforço, não cartão.
- **O servidor é técnico de verdade** — build reproduzível, base preservada, decisões rastreáveis. Isso é raro e, com o tempo, os jogadores sentem.

A promessa é simples: **aqui, o que você conquistar é seu, e vale.**

## 5. O que NUNCA aceitaremos

1. **Pay-to-Win** em qualquer disfarce (item, buff, XP, conveniência competitiva).
2. **Customs que descaracterizem o Interlude** (auto-farm, painéis mágicos, itens inventados).
3. **Interferência do dono/GM na economia ou no ranking** — nem "só uma vez".
4. **Rates ou atalhos que anulem a jornada** sem decisão documentada.
5. **Mudança de gameplay sem evidência** (ver [CHANGE_ACCEPTANCE_POLICY](../knowledge/methodology/CHANGE_ACCEPTANCE_POLICY.md)).
6. **Wipe/reset por conveniência** — o tempo do jogador é sagrado.
7. **Promessas que não podemos manter** (servidor "para sempre" sem sustentabilidade real).

## 6. O que significa "Retail First" dentro deste projeto?

**Retail First = o ônus da prova é sempre de quem quer mudar.**

Formalmente ([ADR-003](../adr/ADR-003-retail-first.md)): o comportamento do Interlude/L2OFF é o padrão; divergir é exceção, permitida só quando (a) opcional e desligada por padrão, (b) corrige problema comprovado, ou (c) é infraestrutura sem tocar gameplay.

Na prática, três consequências desconfortáveis que aceitamos:
- **Bugs do retail podem ser parte do retail.** Nem todo comportamento estranho é para "consertar".
- **"Faz sentido melhorar" não é argumento.** Sem evidência, não muda ([EVIDENCE_LEVELS](../knowledge/methodology/EVIDENCE_LEVELS.md)).
- **Hoje não sabemos o suficiente.** O projeto tem **zero evidências retail** ([EVIDENCE_REGISTER](../knowledge/baseline/EVIDENCE_REGISTER.md)) — logo, quase tudo neste documento é **intenção**, não descrição validada.

## 7. O que este documento NÃO decide
- **Rates** (x1 retail vs mid) → decisão em aberto: [DECISION_LOG](../design/DECISION_LOG.md) **D-001**.
- **Monetização** → [MONETIZATION_PHILOSOPHY](../monetization/MONETIZATION_PHILOSOPHY.md) (apresenta opções, não decide).
- **Qualquer número** — números exigem evidência retail que ainda não temos.
