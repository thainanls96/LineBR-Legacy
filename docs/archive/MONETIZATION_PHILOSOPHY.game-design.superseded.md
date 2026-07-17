> 📦 **DOCUMENTO ARQUIVADO — NÃO VIGENTE.**
> Superado pela pasta `monetization/` (Sprint 008), que traz as decisões do Owner.
> Preservado para rastreabilidade. Ver [archive/README.md](README.md) e [CHANGELOG](../CHANGELOG.md).

---

# Filosofia de Monetização — LineBR Legacy

> **Documento crítico.** Aqui é onde a maioria dos servidores privados morre — não por falta de dinheiro, mas por vender a alma para consegui-lo.
> **Este documento NÃO decide nada.** Apresenta opções com vantagens, riscos e impacto no jogador. A decisão é do dono e vira entrada no [DECISION_LOG](../design/DECISION_LOG.md).

---

## Nota de honestidade

Não há, nesta conversa, discussões prévias de monetização do LineBR Legacy para eu referenciar. (Houve documentos de monetização do **CAPTA IMOB** — projeto de SaaS imobiliário, cancelado e sem relação alguma com este.) Portanto, este documento parte **dos princípios do projeto**, não de ideias anteriores. Se você tem ideias já discutidas em outro contexto, traga-as: eu as analiso criticamente aqui.

---

## 1. O problema estrutural (que ninguém gosta de encarar)

O Interlude retail era **assinatura**: todos pagavam igual, e o pagamento **não comprava poder**. Esse modelo é o único historicamente compatível com o design do jogo — e é justamente o que servidores privados **não conseguem** replicar, porque:
- cobrar assinatura para jogar afasta a massa que sustenta a população;
- população baixa mata o jogo social — que **é** o jogo;
- então vende-se "coisinhas"; as coisinhas viram poder; o servidor vira P2W; os jogadores sérios saem; o servidor morre.

**Todo servidor privado enfrenta este trilema:**
```
        Sustentabilidade financeira
                  /\
                 /  \
                /    \
   População   /______\   Integridade (sem P2W)
```
**Só se escolhe dois.** Quem promete os três está mentindo ou ainda não percebeu. Nosso Manifesto já escolheu **Integridade** como inegociável ([P-11](../constitution/DESIGN_PRINCIPLES.md)) — logo, a escolha real é entre **População** e **Sustentabilidade**.

## 2. Princípios que nunca serão quebrados
1. **Dinheiro nunca compra poder** — nem stat, nem XP, nem item, nem tempo competitivo.
2. **Dinheiro nunca compra vantagem competitiva indireta** (fila, buff, slot, warehouse maior, mais tempo offline).
3. **Nada exclusivo que afete gameplay** — se afeta, tem que ser obtível jogando.
4. **Transparência total** — toda receita e todo item vendido são públicos.
5. **O dono não joga com vantagem.** GM não acumula, não vende, não interfere.
6. **Sem "só desta vez".** A primeira exceção é o fim da política.

## 3. O que **pode** ser vendido (análise crítica)

### 3.1 Cosméticos sem efeito ✅ (o mais seguro)
Skins de armadura/arma, cores de nome/título, acessórios visuais, animações.
- **Vantagem:** zero impacto em poder; apelo real (status social é motivador legítimo).
- **Risco:** ⚠️ **fere Retail First** — o Interlude não tinha loja de skins. Skins *inexistentes no retail* são customs visuais → exigem ADR e ferem a estética do mundo.
- **Impacto no jogador:** baixo, **se** discreto. Alto e negativo se a cidade virar carnaval — a atmosfera é parte do produto.
- **Veredito:** viável, mas **menos "retail"** do que parece. Requer ADR.

### 3.2 Serviços de conta ✅/⚠️
Troca de nome, troca de aparência, transferência de personagem, slot extra de personagem.
- **Vantagem:** não afeta poder; demanda real; barato de operar.
- **Risco:** slot extra = mais bots/dualbox potencial; troca de nome pode atrapalhar reputação social (o nome **é** reputação no L2).
- **Veredito:** viável com cautela. **Troca de nome** merece debate — reputação é mecânica social real.

### 3.3 Apoio voluntário / doação ✅
Doação sem contrapartida, ou com contrapartida só simbólica (nome nos créditos, Discord role).
- **Vantagem:** **zero risco de P2W**; alinha quem paga com quem ama o projeto.
- **Risco:** 🔴 **receita imprevisível e insuficiente** — é a opção mais honesta e a menos sustentável.
- **Veredito:** deve existir sempre. **Não sustenta sozinho.**

### 3.4 Assinatura cosmética / "clube" ⚠️
Mensalidade que dá só cosmético/QoL não-competitivo (ex.: cor de nome, título especial).
- **Vantagem:** **receita recorrente** — a única coisa que dá previsibilidade.
- **Risco:** a pressão para "adicionar valor" ao clube é constante e **sempre** empurra para P2W. Começa cosmético, termina com "+1 slot de buff".
- **Veredito:** possível, **se** o escopo for congelado em ADR e nunca ampliado.

### 3.5 Publicidade / parcerias ⚠️
- **Vantagem:** não toca no jogo.
- **Risco:** receita baixa em nicho pequeno; pode poluir a experiência.
- **Veredito:** marginal.

## 4. O que **nunca** será vendido
| Item | Por quê |
|------|---------|
| Adena, XP, SP, drop boost | destrói a economia ([P-04](../constitution/DESIGN_PRINCIPLES.md), [P-09](../constitution/DESIGN_PRINCIPLES.md)) |
| Equipamento, enchant, scrolls, materiais | destrói craft, spoil e o Dwarf ([P-05](../constitution/DESIGN_PRINCIPLES.md)) |
| Buffs, soulshots, consumíveis | vantagem competitiva disfarçada de conveniência |
| Vantagem em Olympiad/Siege/Hero | destrói o topo ([P-07](../constitution/DESIGN_PRINCIPLES.md)) |
| Ressurreição, redução de penalidade de morte | remove o risco ([P-14](../constitution/DESIGN_PRINCIPLES.md)) |
| Warehouse/inventário maior | logística é poder no L2 |
| Qualquer coisa exclusiva que afete gameplay | P2W por definição |
| VIP com prioridade de fila | vende tempo = vende poder |

## 5. Como manter sustentabilidade financeira (a conta real)

**Custos reais** (a serem estimados): VPS, domínio, backups, proteção DDoS, tempo do dono.
Hoje: um servidor de porte pequeno/médio cabe numa VPS modesta — a barreira é **tempo**, não dinheiro.

**Cenários honestos:**
| Cenário | Receita | Integridade | Viabilidade |
|---------|---------|-------------|-------------|
| Só doação | 🔴 baixa/instável | 🟢 total | ok se o dono banca a diferença |
| Doação + cosmético | 🟡 média | 🟡 boa (com ADR) | mais realista |
| Doação + clube cosmético recorrente | 🟢 previsível | 🟠 sob pressão constante | precisa de disciplina de ferro |
| Qualquer coisa com poder | 🟢 alta | 🔴 zero | **proibido** |

> **A pergunta honesta que o dono precisa responder:** *o LineBR Legacy precisa se pagar, ou é um projeto que você banca porque quer que ele exista?* As duas respostas são legítimas — mas levam a servidores diferentes, e fingir que não é escolher errado por omissão.

## 6. Como evitar que dinheiro compre poder (mecanismos concretos)
1. **Lista branca fechada em ADR**: só o que está explicitamente listado pode ser vendido. Novidade = novo ADR + revisão pública.
2. **Teste do competidor:** *"dois jogadores idênticos, um pagou e o outro não — algum ganha vantagem em PvE, PvP, economia ou tempo?"* Se sim → não vende.
3. **Auditoria pública** de itens vendidos e receita.
4. **Separação de contas:** GM/dono não têm personagens competitivos com privilégio.
5. **Sem loja in-game que afete o mercado** — cosmético não entra na economia de adena.

## 7. Como gerar receita recorrente sem P2W
- **Clube cosmético** com escopo congelado (§3.4) — o único caminho recorrente compatível.
- **Doação recorrente** (apoio) com reconhecimento simbólico.
- **Merch/comunidade** (marginal, mas zero risco).
> Recorrência **honesta** vem de pessoas que querem que o projeto exista — não de pessoas que querem ganhar do vizinho.

## 8. Riscos declarados
| Risco | Gravidade | Nota |
|-------|:---------:|------|
| Pressão financeira levar a "só uma exceção" | 🔴 | é assim que **todo** servidor cai. A política existe para o dia em que doer |
| Cosmético ferir Retail First / atmosfera | 🟠 | requer ADR; manter discrição |
| Receita insuficiente → abandono | 🟠 | abandonar fere [P-13](../constitution/DESIGN_PRINCIPLES.md) mais do que não monetizar |
| Vender "conveniência" | 🔴 | conveniência competitiva **é** poder |

## 9. Recomendação (não é decisão)
Minha leitura técnica: **doação + cosmético discreto com lista branca em ADR** é o único ponto do trilema compatível com o Manifesto. E, ainda assim, **provavelmente não paga o projeto** — o que torna a pergunta da §5 (banca ou se paga?) a decisão mais importante deste documento.

**Nada decidido.** → [DECISION_LOG D-002](../design/DECISION_LOG.md).
