# Política de Serviços — LineBR Legacy

> Serviços **administrativos** possíveis. Nenhum altera gameplay. **Nada implementado.**

---

## Princípio

Todos os itens abaixo são **serviços administrativos**: operam sobre a **conta/identidade**, nunca sobre o **poder do personagem**. Nenhum deles dá vantagem em PvE, PvP, economia ou progressão.

Todos obedecem a Regra Mestra: *economizam tempo/resolvem problemas, não substituem esforço.*

## Serviços futuros possíveis

### Identidade
| Serviço | Natureza | Observação |
|---------|----------|------------|
| **Mudança de Nick** | identidade | ⚠️ ver nota sobre reputação abaixo |
| **Mudança de Sexo** | identidade visual | sem efeito em stats |
| **Mudança de Título** | identidade | — |
| **Mudança de Cor do Nick** | identidade visual | — |
| **Mudança de Cor do Título** | identidade visual | — |
| **Clan Rename** | identidade coletiva | ⚠️ reputação de clã |
| **Alliance Rename** | identidade coletiva | ⚠️ reputação de aliança |

### Recuperação
| Serviço | Natureza | Observação |
|---------|----------|------------|
| **Recuperação de personagem deletado** | administrativo | dentro da janela técnica de retenção |
| **Recuperação de conta** | administrativo | verificação de titularidade |
| **Recuperação de PIN** | administrativo | verificação de titularidade |
| **Recuperação administrativa de itens** | administrativo | **somente casos comprovados** |

---

## ⚠️ Notas de risco (registradas, não são objeções)

### Recuperação de itens — o serviço mais delicado
É o único serviço da lista que **toca a economia**. Riscos a controlar:
- **Criação de item** — recuperar item é, tecnicamente, **criar item** ([regra E-7](MONETIZATION_PHILOSOPHY.md)). Só é legítimo se o item comprovadamente existiu e se perdeu por falha **do servidor**, restaurando o estado — nunca compensando erro do jogador.
- **Precedente** — "comprovado" precisa de critério escrito e público, ou vira caso a caso, e caso a caso vira favorecimento.
- **Vetor de fraude** — é o alvo preferido de engenharia social.

**Recomendação:** este serviço deveria ser **gratuito** e raro (correção de falha nossa), **nunca pago**. Cobrar por recuperação cria incentivo perverso: o servidor lucra com os próprios bugs.

### Mudança de Nick / Clan Rename — reputação é mecânica social
No L2, **o nome é a reputação**. Rivalidades, listas de KOS, confiança em comércio — tudo se ancora no nome. Trocar de nome permite **escapar da própria reputação** (o PK que recomeça limpo, o golpista que reabre negócio).

Não é P2W, mas **é** interferência no tecido social ([SOCIAL_PHILOSOPHY §8](../design/SOCIAL_PHILOSOPHY.md)).
**Mitigação sugerida:** histórico público de nomes anteriores, ou *cooldown* longo entre trocas.

## Fato técnico (EV-001)
Nenhum destes serviços existe como sistema automatizado na aCis 409. Todos seriam executados **manualmente por administração** (ou exigiriam ferramentas custom). Isso os torna:
- ✅ baratos de "implementar" (é processo, não código);
- ⚠️ caros de **operar** (tempo do dono) e dependentes de disciplina.

## Pendências
| # | Pendência |
|---|-----------|
| S-1 | Preço de cada serviço (ou gratuidade) |
| S-2 | Critério público e escrito de "caso comprovado" para recuperação de itens |
| S-3 | Janela de retenção para recuperação de personagem deletado |
| S-4 | Processo de verificação de titularidade (anti-fraude) |
| S-5 | Política de histórico de nomes |
