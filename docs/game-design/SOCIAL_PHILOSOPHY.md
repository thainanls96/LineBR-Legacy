# Filosofia Social — LineBR Legacy

> **A tese central deste documento:** o Lineage II é um **jogo social disfarçado de RPG**. O conteúdo acaba; as pessoas não.
> O end game do L2 não é um boss — são **outros jogadores**. Um servidor tecnicamente perfeito e socialmente morto **é um servidor morto**.

---

## 1. Como incentivar Party?

**Não incentivando — apenas não sabotando.**

O Interlude já é desenhado para grupo: classes incompletas por design (o healer não mata, o mago não aguenta), mobs duros, bônus de XP em party, dungeons de grupo. **Isso basta** — se não estragarmos.

O que **sabota** party (e por isso recusamos):
- ❌ Rates altas → solo fica viável → ninguém precisa de ninguém.
- ❌ Buffer NPC gratuito → o Buffer humano perde função social.
- ❌ Auto-farm → o jogador não está lá para conversar.
- ❌ Itens que compensem a falta de grupo → party vira ineficiência.

> **Insight desconfortável:** todo "quality of life" que torna o solo viável é uma facada no jogo social. A conveniência individual é inimiga da dependência mútua — e a dependência mútua **é** o L2.

## 2. Como incentivar Clan?
O clã existe porque **coisas grandes exigem gente**: raids, sieges, castelo, Seven Signs.
- **Manter caro:** clan skills, reputação, nível de clã — custam e por isso valem.
- **Manter necessário:** se dá para fazer end game sem clã, o clã vira chat.
- **Manter político:** castelo/siege dão ao clã um **objetivo territorial**, não só social.

## 3. Como incentivar Ally?
Aliança existe para o que é grande demais até para um clã: sieges, epics, guerra política.
- Não forçar; deixar a **escassez de castelos** criar naturalmente a necessidade de coalizão.
- Aliança é consequência da geopolítica — não uma feature a ser "estimulada".

## 4. Como incentivar Siege?
- **Escassez de castelos** → concorrência real.
- **Benefício econômico concreto** (taxas) → motivo material, não só troféu.
- **Agenda pública** → cria evento do servidor, o dia que todos esperam.
- ❌ Nunca: vantagem comprável em siege ([P-11](DESIGN_PRINCIPLES.md)).

## 5. Como incentivar Olympiad?
- É o único sistema de **mérito puro** — proteja-o como tal.
- Noblesse como barreira mantém a elite.
- **A única regra que importa:** nada comprável pode influenciar o resultado. No dia em que influenciar, o Olympiad vira teatro.

## 6. Como incentivar Hero?
- **Escassez** ([P-07](DESIGN_PRINCIPLES.md)): poucos, cíclicos, visíveis.
- **Visibilidade:** aura, skills, canal próprio — o Hero precisa ser **visto**.
- Hero funciona por inveja saudável: o jogador de 20 vê um Hero em Giran e decide ficar.

## 7. Como incentivar amizade?
Amizade nasce de **dependência mútua + tempo + risco compartilhado**:
- dependência: classes incompletas, party obrigatória na prática;
- tempo: jornada longa (x1 cria vínculo; x100 cria turnover);
- risco: morrer junto, perder junto, conquistar junto.
> Não se cria amizade com uma feature. Cria-se **não removendo** as condições que a produzem.

## 8. Como incentivar rivalidade?
Rivalidade é o combustível de longo prazo — e o L2 é feito dela:
- **PvP com consequência** (karma, drop, XP) → conflito tem peso;
- **Recursos disputados** (bosses, spots, castelos) → motivo real de briga;
- **Nomes memoráveis** → reputação persistente (por isso troca de nome é problemática — [MONETIZATION §3.2](MONETIZATION_PHILOSOPHY.md));
- **Rankings visíveis** → placar público.
> Rivalidade saudável exige **fair play absoluto**. Quando existe P2W, a rivalidade morre e vira ressentimento — as pessoas não odeiam perder; odeiam perder para quem pagou.

## 9. O que mata o social (lista de vetos)
| Feature | O que ela mata |
|---------|----------------|
| Auto-farm | presença humana |
| Buffer NPC completo/grátis | classe de suporte + interdependência |
| Rates muito altas | necessidade do outro |
| Teleporte grátis/instantâneo | encontros casuais no mundo |
| Loja de equipamento | economia entre jogadores |
| P2W | confiança (e o servidor junto) |
| Wipes | história e vínculo ([P-13](DESIGN_PRINCIPLES.md)) |

## 10. O risco social que ninguém quer admitir
🔴 **População mínima viável.** O Interlude foi desenhado para **milhares** de jogadores. Com 30–50 pessoas:
- não há party, não há mercado, não há siege, não há Olympiad;
- Giran fica vazia — e Giran vazia é o atestado de óbito ([WORLD_IMPORTANCE](WORLD_IMPORTANCE.md)).

**Esta é a maior ameaça ao projeto** — maior que qualquer bug ou decisão de rate. E é ela que cria a pressão para mid-rate e para P2W: *"precisamos de gente, então vamos facilitar"*. É assim que servidores morrem duas vezes: primeiro a alma, depois o resto.

**Nossa posição:** a resposta para população baixa **não pode ser** quebrar o design ([P-11](DESIGN_PRINCIPLES.md), [ADR-003](../ADR/ADR-003-retail-first.md)). Tem que ser comunidade, divulgação e paciência — ou o projeto assume conscientemente que será pequeno ([D-003](DECISION_LOG.md)).
