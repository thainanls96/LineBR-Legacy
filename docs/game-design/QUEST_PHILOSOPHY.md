# Filosofia de Quests — LineBR Legacy

> ⚠️ **Evidência ★☆☆☆☆–★★☆☆☆** nas afirmações sobre o Interlude. Intenção de design.
> **Fato (EV-001):** a aCis 409 carrega **857 scripts regulares + 6 agendados**.

---

## 1. As quests devem ser obrigatórias?

**Não — e essa é a resposta do próprio retail.**

No Interlude a maioria das quests é **opcional**; poucas são obrigatórias de fato (profissões, subclass, noblesse). Essa proporção **é** design: quests obrigatórias criam trilho; quests opcionais criam **escolha**, e escolha é o que faz o mundo parecer vivo.

**Nossa posição:** manter exatamente a obrigatoriedade do retail. Não tornar quest opcional em obrigatória (fere Retail First), nem o contrário.

## 2. Quais quests são fundamentais?

| Categoria | Papel | Por que não pode perder importância |
|-----------|-------|-------------------------------------|
| **1ª Profissão (~20)** | Primeiro marco de identidade | define a classe; é o 1º "eu sou alguém" |
| **2ª Profissão (~40)** | **O maior marco da vida média** | é o momento em que a classe vira a classe |
| **Subclass (~75)** | Marco de elite | abre o end game |
| **Noblesse (~75+)** | Porta do Olympiad | sem ela, não há Hero |
| **Newbie quests** | Retenção | guiam e equipam quem ainda não entendeu o jogo |
| **Seven Signs** | Política coletiva | transforma farm em geopolítica |

## 3. Quais quests movimentam economia?

- **Quests de material/craft** — alimentam a cadeia do Dwarf.
- **Quests de adena repetíveis** — renda de early/mid game; **atenção:** são *faucets* — em rate alta, viram fábrica de inflação.
- **Quests de recipe/equipamento** — injetam itens específicos no mercado.
- **Quests de acesso** (que liberam áreas/serviços) — criam demanda indireta.

> ⚠️ Toda quest com recompensa em adena é uma **torneira**. Ao decidir rates ([D-001](DECISION_LOG.md)), `RateQuestReward` e `RateQuestDrop` precisam ser tratados junto com drop — esquecê-los é o erro clássico que infla economias.

## 4. Quais quests não podem perder importância?
Profissões, subclass, noblesse e Seven Signs. Se qualquer uma virar trivial (por rate, por atalho ou por "conveniência"), perde-se um **marco emocional** da jornada — e marcos são o que o jogador lembra anos depois.

## 5. Como impedir que sejam ignoradas?

**A resposta honesta: não fazendo nada de especial — e cuidando das rates.**

Quests são ignoradas por **dois** motivos, e nenhum se resolve mexendo na quest:
1. **Rates altas** → a recompensa da quest vira irrelevante perto do farm. *Causa: rate, não quest.*
2. **Economia inflacionada** → a adena da quest não compra nada. *Causa: economia, não quest.*

**O que NÃO faremos:**
- ❌ Aumentar recompensa de quest para "incentivar" → é custom, fere Retail First, e infla.
- ❌ Tornar quest obrigatória → fere Retail First.
- ❌ Criar quest nova → custom.
- ❌ "Melhorar" a UI de quest → conveniência que descaracteriza.

**O que faremos:** manter as rates coerentes o bastante para que a economia da quest **faça sentido sozinha**, exatamente como fazia em 2007. Se as quests estiverem sendo ignoradas no nosso servidor, o defeito é **nosso**, e está nas rates/economia — não na quest.

## 6. Princípio regente
[P-01](DESIGN_PRINCIPLES.md): *toda quest deve ter propósito.* Mas cuidado com a leitura: **o propósito é do retail, não nosso.** Se uma quest do Interlude parece inútil, ela fica assim mesmo — Retail First significa aceitar também o que não gostamos.

## 7. Pendências
| # | Pendência | Como resolver |
|---|-----------|---------------|
| Q-1 | Quais quests são de fato obrigatórias no Interlude (lista validada) | fonte retail ★★★★ |
| Q-2 | Quais recompensas de quest são *faucets* relevantes | auditoria do Quest Engine (F01) + medição de economia |
| Q-3 | Seven Signs: mecânica e impacto econômico reais | auditoria F04 |
