# Filosofia do Projeto — LineBR Legacy

## A visão em uma frase

> Reconstruir a experiência clássica do **Lineage II Interlude (2007)** sobre uma base de código **moderna, organizada e sustentável** — não construir mais um servidor cheio de customizações.

## O que o LineBR Legacy É

Um servidor **Retail First**: fiel ao comportamento oficial do Interlude/L2OFF, onde o mundo, as mecânicas, a progressão e a economia funcionam como os jogadores de 2007 conheceram. A modernidade está na **engenharia** — código limpo, versionado, documentado e performático — e não em distorcer o jogo.

A base é a **aCis 409 oficial**, escolhida por ser enxuta, fiel e evolutiva (ver [ADR-001](ADR/ADR-001-base-oficial.md)). Sobre ela aplicamos as correções oficiais (410, 411) e, só então, ajustes próprios cuidadosamente justificados.

## O que o LineBR Legacy NÃO é

- **Não** é um servidor "custom" que acumula sistemas desconexos (auto-farm, painéis, itens mágicos de loja) que descaracterizam o Interlude.
- **Não** é Pay-to-Win: nenhuma vantagem competitiva é vendida.
- **Não** é um fork que abandona o upstream — acompanhamos as revisões oficiais da aCis.
- **Não** trata "quanto mais features, melhor" como verdade. Aqui, **menos e fiel** vence **muito e distorcido**.

## Princípios que guiam decisões

1. **Fidelidade primeiro.** Na dúvida entre "retail" e "conveniente", escolhemos retail (ver [ADR-003](ADR/ADR-003-retail-first.md)).
2. **A conquista tem valor.** O prazer do Interlude vem do esforço: evoluir, farmar, cooperar e competir têm peso. Nada de atalhos que anulem a jornada.
3. **Economia saudável.** Adena, drops e craft mantêm significado; inflação e itens "grátis" são inimigos.
4. **Base antes de enfeite.** Primeiro uma fundação estável e correta; customizações só depois, opcionais e reversíveis.
5. **Engenharia de verdade.** Git disciplinado, documentação obrigatória, decisões registradas em ADR, performance e segurança como requisitos — não como "depois a gente vê".
6. **Longo prazo.** Cada escolha é feita pensando em anos de manutenção, não na próxima semana.

## Por que essa filosofia importa

Servidores privados costumam morrer por dois motivos: **descaracterização** (viram um jogo irreconhecível) e **caos técnico** (código impossível de manter). O LineBR Legacy ataca os dois de frente — preservando a alma do Interlude e tratando o projeto como software profissional.

Esta filosofia é **permanente**. Qualquer proposta que a contrarie deve ser recusada ou exige um ADR que a supere explicitamente.
