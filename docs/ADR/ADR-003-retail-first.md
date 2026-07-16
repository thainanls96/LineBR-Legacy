# ADR-003 — Retail First

- **Status:** Aceito
- **Data:** 2026-07-15
- **Decisores:** Thainan Lima

## Contexto

A maioria dos servidores privados de Lineage II fracassa ao acumular customizações desconexas que distorcem o balanceamento, quebram a economia e afastam quem busca a experiência clássica. O LineBR Legacy nasce com a proposta oposta: **reconstruir fielmente o Interlude de 2007** sobre uma base moderna e organizada. Isso exige um princípio arquitetural que sirva de filtro para toda decisão futura.

## Decisão

Adota-se oficialmente o princípio **Retail First**:

> **Toda alteração deve priorizar a fidelidade ao Lineage II Interlude / L2OFF.** O comportamento *retail* é o padrão e o alvo. Divergir do retail é a exceção, não a regra.

Uma customização (desvio do retail) **só é permitida** quando satisfizer **ao menos uma** das condições abaixo, e for aprovada via ADR próprio:

1. **É opcional** — pode ser ligada/desligada por configuração, sem alterar o comportamento padrão (retail) de quem não a ativa; **ou**
2. **Resolve um problema comprovado** — corrige um bug, exploit ou inconsistência real, documentado com evidência; **ou**
3. **Melhora infraestrutura sem alterar gameplay** — performance, segurança, logging, observabilidade, ferramentas — sem mudar mecânicas de jogo, rates ou economia percebidas pelo jogador.

Qualquer alteração que **mude gameplay, rates ou economia** e **não** se enquadre nas condições acima é **rejeitada por padrão**.

## Consequências

**Positivas**
- Preserva a identidade clássica do Interlude — o principal atrativo do projeto.
- Cria um critério objetivo para aceitar/rejeitar mudanças (menos discussão subjetiva).
- Mantém a base próxima do upstream aCis, facilitando aplicar revisões oficiais.

**Negativas / custos**
- Algumas "conveniências" populares em servidores custom serão recusadas ou terão de ser opcionais.
- Exige disciplina: toda exceção precisa de justificativa documentada (ADR).

## Aplicação prática

- Correções oficiais da aCis (revisões 410/411) **são Retail First por natureza** — aproximam do comportamento correto.
- Customizações de conveniência (ex.: buffer, auto-learn) só entram como **opcionais e desligadas por padrão**.
- Nada de **Pay-to-Win**: itens/vantagens que alterem o equilíbrio competitivo por pagamento violam este ADR e o [LINEBR_MANIFESTO](../LINEBR_MANIFESTO.md).
