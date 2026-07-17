# Filosofia de Economia — LineBR Legacy

> A economia é o sistema **mais frágil e menos reversível** do servidor. Um erro aqui aparece em meses e não se conserta sem wipe (que é proibido por [P-13](../constitution/DESIGN_PRINCIPLES.md)).
> **Nível de evidência:** este documento expressa **intenção de design**. As afirmações sobre o funcionamento retail estão marcadas ★ conforme [EVIDENCE_LEVELS](../knowledge/methodology/EVIDENCE_LEVELS.md).

---

## ⚠️ A decisão que precede tudo: RATES

Toda esta filosofia depende de uma decisão **ainda em aberto** ([DECISION_LOG D-001](DECISION_LOG.md)):

**Fato verificado (EV-001/EV-002):** a source oficial aCis 409 **e** o runtime Base Zero estão em **x1** (`RateXp=1.`, `RateSp=1.`, `RateDropCurrency=1.`, `RateDropItems=1.`, `RateDropSpoil=1.`).
*(As rates mid — x20/x10/x5 — eram do **antigo LineBR customizado** da VPS, uma base diferente. Não são a nossa base.)*

Sem resolver x1-vs-mid, **nenhum número deste documento pode ser fixado** — porque a rate multiplica ou destrói cada mecanismo abaixo.

---

## 1. Como a Adena entra (fontes / *faucets*)
| Fonte | Papel no Interlude | Observação |
|-------|--------------------|------------|
| **Drop de mobs** | principal | escalonado por nível/região |
| **Spoil** | secundária, exclusiva do Dwarf | sustenta o craft |
| **Quests** | pontual, dirigida | algumas são a renda de early game |
| **Venda a NPC** | escoadouro de lixo → vira renda | preço fixo = piso de valor |
| **Raid/Boss** | eventual, alta | cobiça |
| **Manor / Castelo** | coletiva | economia de clã |

## 2. Como a Adena sai (drenos / *sinks*)
| Dreno | Papel | Risco se fraco |
|-------|-------|----------------|
| **Compra em NPC** (soulshots, potions, flechas) | dreno **contínuo** — o mais importante | sem ele, adena só acumula |
| **Craft** (materiais, recipes, taxa do Dwarf) | dreno + circulação | craft morre |
| **Enchant** (scrolls) | dreno **agressivo** (queima item + adena) | itens viram commodity |
| **Teleporte** | dreno pequeno e constante | mundo encolhe (fere [P-10](../constitution/DESIGN_PRINCIPLES.md)) |
| **Taxas de castelo / lojas** | dreno coletivo | economia de clã esvazia |
| **Morte / perda de XP** | dreno indireto (tempo) | risco some |
| **Clan hall / auction** | dreno de topo | adena de elite acumula |

> **Princípio central:** uma economia saudável é **um cano, não um balde**. Se entra mais do que sai, infla — sempre. A pergunta certa nunca é "quanta adena entra?", e sim **"a que taxa ela sai?"**.

## 3. Quais itens movimentam o mercado
- **Consumíveis** (soulshot/spiritshot, potions, flechas) — volume constante, base do fluxo diário.
- **Materiais de craft** — a "matéria-prima" da economia; ligam mob → Dwarf → jogador.
- **Recipes** — escassez controlada, dão poder ao crafter.
- **Equipamentos B/A/S** — os grandes objetos de desejo; sustentam o topo.
- **Enchant scrolls** — o cassino que queima riqueza e cria raridade.
- **Itens de boss** — raridade máxima, definem status.

## 4. Como manter o Craft vivo
1. **Comprar pronto tem que ser caro** — se NPC vende o que o Dwarf faz, o Dwarf morre.
2. **Materiais só vêm do mundo** (drop/spoil) — nunca de loja.
3. **Craft precisa de risco/custo** (falha, taxa) — sem custo, não há valor.
4. **Rates altas matam o craft**: com muito drop de item pronto, ninguém craft. ⚠️ *impacto direto de D-001.*

## 5. Como manter o Spoil vivo
- Spoil é a **razão de existir** de uma classe inteira (Dwarf Scavenger). Se material vier fácil de drop normal ou de loja, o spoil vira hobby.
- **Manter:** materiais relevantes **exclusivos ou muito melhores** via spoil.
- ⚠️ **Ameaça direta:** `RateDropSpoil` desbalanceada em relação a `RateDropItems` — inverte o equilíbrio silenciosamente.

## 6. Como manter os Dwarfs importantes
O Dwarf é o **banco central** do Interlude. Ele importa se, e só se:
- craft for a via principal de equipamento (não a loja, não o drop);
- spoil for a via principal de material;
- **peso/warehouse** importarem (logística é poder);
- ninguém puder "pular" a cadeia com dinheiro real ([P-11](../constitution/DESIGN_PRINCIPLES.md)).

> Um servidor onde o Dwarf é dispensável **não é Interlude** — é outro jogo com o mesmo mapa.

## 7. Como evitar inflação
1. **Drenos ≥ fontes**, sempre. Medir, não supor.
2. **Preços de NPC fixos** funcionam como âncora de valor.
3. **Nada de adena "de graça"** (evento, compensação, presente de GM). Cada adena criada fora do mundo é imposto sobre todos.
4. **Vigiar o topo:** riqueza concentrada infla o mercado de itens raros primeiro — é o sinal precoce.
5. **Monitorar, não reagir tarde:** ver §9.

## 8. Como evitar excesso de Adena
- Rates conservadoras (⚠️ D-001).
- Enchant como dreno voluntário (o jogador **quer** queimar adena).
- Consumíveis obrigatórios em PvE/PvP de alto nível.
- **Nunca** vender adena, nem indiretamente ([MONETIZATION_PHILOSOPHY](../monetization/MONETIZATION_PHILOSOPHY.md)).

## 9. Como manter equipamentos com valor
- **Escassez**: A/S-grade têm que ser raros e caros.
- **Destruição**: enchant que quebra item é o que impede o acúmulo infinito. É o dreno mais poderoso do jogo.
- **Sem duplicação**: bug de dupe é evento de **extinção** para a economia — mais grave que qualquer exploit de combate.
- **Sem loja de itens** ([P-11](../constitution/DESIGN_PRINCIPLES.md)).

## 10. Instrumentação (obrigatória antes de qualquer ajuste)
Não se pilota economia no escuro. Antes de tocar em qualquer rate, é preciso medir:
| Métrica | Por quê |
|---------|---------|
| Adena total em circulação (por semana) | detecta inflação cedo |
| Adena criada × destruída (faucet/sink ratio) | o número mais importante |
| Distribuição de riqueza (top 1% × mediana) | detecta concentração |
| Volume de craft/spoil por semana | saúde do Dwarf |
| Preço médio de itens-chave no mercado | inflação percebida |

> Isso é **infraestrutura sem tocar gameplay** → permitido pelo [ADR-003 §3](../adr/ADR-003-retail-first.md). É o primeiro trabalho de economia que deveria existir.

## 11. Riscos declarados
| Risco | Gravidade | Mitigação |
|-------|:---------:|-----------|
| Decidir rates sem dados | 🔴 | resolver D-001 com evidência retail |
| Inflação silenciosa | 🔴 | instrumentação (§10) desde o dia 1 |
| Dupe / exploit | 🔴 | auditoria de Items/Trade antes de abrir |
| Adena de evento/GM | 🟠 | proibição explícita ([P-15](../constitution/DESIGN_PRINCIPLES.md)) |
| Loja quebrar o craft | 🟠 | nada que o Dwarf faça pode vir de loja |
