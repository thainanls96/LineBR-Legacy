# Política Oficial de Aceitação de Alterações — LineBR Legacy

> Os **6 critérios inegociáveis**. Uma alteração só entra se cumprir **todos**. Falhou um? **NÃO IMPLEMENTAR.**

---

## Os 6 critérios

### ✔ 1. Evidência suficiente
Nível **≥ ★★★★☆** para afirmações sobre o retail — ou **★★★☆☆ que não altere gameplay**.
Declarar: nível, fonte (categoria de [RESEARCH_SOURCES.md](RESEARCH_SOURCES.md)), e se a afirmação é *sobre a aCis* ou *sobre o retail*.
❌ Reprova: memória, opinião, outro emulador, "o código da aCis mostra que…" usado como prova de retail.

### ✔ 2. Reproduzível
Existe um **procedimento escrito** que qualquer dev executa para observar o comportamento — antes e depois.
❌ Reprova: "é óbvio", "confia", ou algo que só se manifesta em produção sem receita.

### ✔ 3. Não descaracteriza o Interlude
A mudança **aproxima** do Interlude/L2OFF. Conveniência moderna, "quality of life" e balanceamento pessoal **não** entram — salvo como **opcional desligado por padrão** ([ADR-003](../ADR/ADR-003-retail-first.md)).
❌ Reprova: qualquer coisa que altere economia/progressão/poder sem base retail. Pay-to-Win é vetado pelo [Manifesto](../LINEBR_MANIFESTO.md).

### ✔ 4. Possui rollback
Commit atômico revertível (`git revert`), preferencialmente aditivo/configurável. A [Base Zero](../Base-Zero.md) e as tags permanecem intactas.
❌ Reprova: mudança entrelaçada com outras, ou que altere `runtime-reference/`.

### ✔ 5. Possui documentação
- **ADR** se altera gameplay/arquitetura;
- registro no documento do sistema (auditoria/backlog) com a evidência;
- changelog + atualização do [SYSTEM_INDEX.md](SYSTEM_INDEX.md).
❌ Reprova: "documento depois".

### ✔ 6. Possui validação
Build (JDK 21 + Ant, 0 erros) → Runtime Validation (servidor sobe, cenário exercitado) → Logs (0 ERROR / 0 WARN novos). Ver [VALIDATION_PROCESS.md](VALIDATION_PROCESS.md).
❌ Reprova: "compilou, deve estar bom".

---

## Fluxo de decisão

```
                 ┌─────────────────────────────┐
                 │ Proposta de alteração       │
                 └──────────────┬──────────────┘
                                ▼
                   Evidência ≥ ★★★★ ?
                    │                 │
                   NÃO               SIM
                    │                 │
       ┌────────────▼──────┐          │
       │ ★★★☆☆ e NÃO muda  │          │
       │ gameplay?         │          │
       └──┬─────────────┬──┘          │
        NÃO            SIM            │
          │             └─────────────┤
          ▼                           ▼
  ┌───────────────┐         Passa nos 6 critérios?
  │ ❌ NÃO         │            │            │
  │ IMPLEMENTAR   │           NÃO          SIM
  │ → backlog de  │            │            │
  │   pesquisa    │            ▼            ▼
  └───────────────┘     ❌ NÃO IMPLEMENTAR   ADR (se muda gameplay)
                                                  │
                                                  ▼
                                    Implementar → Build → Runtime
                                          → Logs → Commit → PR
                                                  │
                                                  ▼
                                        Aprovação do dono → Merge
```

## Casos especiais

| Caso | Decisão |
|------|---------|
| Bug **objetivo** (crash, exploit, o autor documenta como bug) | Entra como **problema comprovado** (ADR-003 §2), mesmo sem evidência retail — mas com validação completa |
| Inconsistência **interna** da aCis sem alvo retail conhecido | ❌ **Não corrigir** — escolher um lado sem saber qual é o retail é palpite. Vira backlog de pesquisa |
| Infraestrutura pura (log, performance, segurança) sem tocar gameplay | ✅ Permitido (ADR-003 §3), com validação |
| "Todo servidor privado faz assim" | ❌ Irrelevante — não é evidência |
| Comentário do autor da aCis dizendo "retail like" | ⚠️ **Intenção, não prova.** Não sobe nível |

## Consequência de burlar a política
Uma alteração que entre sem cumprir os 6 critérios é **dívida técnica com juros**: ninguém saberá, depois, se aquele comportamento é retail, palpite ou acidente. Isso destrói a rastreabilidade que é a razão de existir desta base. **Reverter** é a resposta padrão.
