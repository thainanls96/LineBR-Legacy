# Template Oficial de Auditoria — LineBR Legacy

> Copie este arquivo para `docs/retail-audit/<SISTEMA>_*.md` ao iniciar a auditoria de um sistema.
> **Toda auditoria deve responder a todas as seções.** Seção sem resposta = auditoria incompleta.
> Ao iniciar: marque o sistema como 🔵 *Em auditoria* no [SYSTEM_INDEX.md](SYSTEM_INDEX.md). Ao terminar: 🟡 *Auditado*.

---

## 1. Objetivo
O que esta auditoria pretende conhecer e **até onde vai** (escopo e não-escopo).
Regras da sprint (o que é proibido tocar).

## 2. Arquitetura
- Pacotes e classes que compõem o sistema (com caminho).
- Hierarquia/herança e responsabilidade de cada peça.
- Enums, interfaces, managers, configs relacionados.
- Tabela: `Classe | Pacote | Linhas | Refs | Papel`.

## 3. Fluxo
- Ciclo completo, do gatilho ao efeito observável.
- Diagrama em texto com `arquivo:linha` em cada etapa.
- Ramificações relevantes (casos especiais).

## 4. Classes
Tabela das classes centrais: papel, estado interno, API pública principal.

## 5. Pacotes (packets)
- Cliente → Servidor: quais, quando, campos.
- Servidor → Cliente: quais, quando, gatilho.
- ⚠️ Marcar o que é **protocolo** (área sensível).

## 6. Dependências
- **Quem chama quem** (grafo).
- **Quem depende de quem** (tabela de acoplamento).
- Pontos de acoplamento notáveis / armadilhas.

## 7. Riscos
Classificar cada componente: 🟢 Baixo · 🟡 Médio · 🟠 Alto · 🔴 Crítico — **com motivo**.
Listar **métodos que jamais devem ser alterados sem extremo cuidado** e por quê.

## 8. Diferenças (aCis × Retail)
Para **cada** divergência suspeita:
```
### D-NN · <título curto>
Fato (aCis):        <arquivo:linha + trecho>
Indício (retail):   <o que se suspeita>
Evidência:          ★☆☆☆☆ … ★★★★★
Fonte:              <categoria de RESEARCH_SOURCES.md + link arquivado + data>
Afirmação sobre:    [ ] aCis   [ ] retail
Reprodução:         <receita ou "não realizada">
Impacto p/ jogador: baixo / médio / alto
Natureza:           retail / anti-cheat / decisão de design da aCis / bug
```

## 9. Evidências
Consolidação: o que foi pesquisado, **o que foi encontrado** e **o que falhou** (buscas sem resultado são dado — registre).
Todas as fontes **arquivadas** (Wayback + data de acesso).

## 10. Nível de confiança
Tabela-resumo por item (★). Declarar explicitamente quantos itens atingem **≥ ★★★★** (isto é, quantos autorizam alteração).

## 11. Recomendação
Veredito técnico honesto:
- O que **pode** ser implementado agora (≥★★★★ ou ★★★☆☆ sem gameplay)?
- O que **não pode** e por quê?
- O que precisa de **mais evidência** — e qual evidência exatamente?

## 12. Backlog
| # | Item | Ref (D-NN) | Impacto | Complexidade | Risco | Dependências | Prioridade |
|---|------|-----------|---------|--------------|-------|--------------|:---------:|

Prioridade = (impacto × confiança) ÷ (risco + complexidade). **P0 = pré-requisito, não melhoria.**

---

## Checklist de encerramento
- [ ] Todas as 12 seções respondidas
- [ ] Todo `arquivo:linha` conferido no commit auditado
- [ ] Toda fonte externa arquivada (Wayback + data)
- [ ] Nível ★ declarado em **cada** diferença, com "sobre aCis" vs "sobre retail"
- [ ] Nenhuma recomendação sem evidência suficiente
- [ ] [SYSTEM_INDEX.md](SYSTEM_INDEX.md) atualizado
- [ ] **Zero** arquivos fora de `/docs` alterados
- [ ] Commit `docs(retail-audit): …` atômico
