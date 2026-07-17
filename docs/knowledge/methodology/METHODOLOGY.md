# Metodologia Oficial de Pesquisa e Alteração — LineBR Legacy

> Fluxo obrigatório para **toda** mudança que se pretenda "retail". **Nenhuma etapa pode ser pulada.**
> Vale para todas as auditorias e sprints futuras.

---

## O fluxo

```
1  DESCOBERTA          → algo parece divergir do Interlude
        ↓
2  PESQUISA            → buscar artefatos (RESEARCH_SOURCES.md)
        ↓
3  COMPARAÇÃO          → confrontar aCis × retail, com arquivo:linha de um lado e artefato do outro
        ↓
4  VALIDAÇÃO           → reproduzir empiricamente (captura/teste). Falhou? volta p/ 2
        ↓
5  CLASSIFICAÇÃO       → atribuir ★ (EVIDENCE_LEVELS.md)  ── < ★★★★? ⇒ PARA. Vira backlog de pesquisa.
        ↓
6  ADR                 → obrigatório se altera gameplay/arquitetura (ADR-003/005)
        ↓
7  IMPLEMENTAÇÃO       → 1 mudança atômica, no estilo do autor da aCis
        ↓
8  BUILD               → JDK 21 + Ant, 0 erros (Build.md)
        ↓
9  RUNTIME VALIDATION  → login+game sobem, cenário exercitado (VALIDATION_PROCESS.md)
        ↓
10 LOGS                → 0 ERROR / 0 WARN novos; evidência anexada
        ↓
11 COMMIT              → atômico, rastreável, com referência à evidência
```

## Detalhamento

### 1. Descoberta
Origem: auditoria de sistema, relato, ou observação em runtime. **Registrar sem julgar**: o que se observa na aCis (com `arquivo:linha`) e o que se suspeita do retail.
❌ Proibido: já propor a "correção" nesta etapa.

### 2. Pesquisa
Buscar artefatos conforme [RESEARCH_SOURCES.md](RESEARCH_SOURCES.md), do mais forte para o mais fraco: cliente oficial → binários/PTS L2OFF → patch notes NCSoft → capturas → arquivos históricos → fóruns técnicos → relatos.
Registrar **tudo**, inclusive as buscas que **falharam** (isso é dado: a Sprint 004 provou que o fórum do L2J está morto — informação valiosa).

### 3. Comparação
Tabela com três colunas: **o que a aCis faz** (`arquivo:linha`) · **o que a evidência retail indica** (fonte) · **delta**.
❌ Proibido: comparar código da aCis com *outra* implementação (L2J/Mobius/fork) e chamar isso de "retail" — emulador não é fonte retail.

### 4. Validação (empírica)
Reproduzir o comportamento: captura de pacotes, teste em servidor de referência, ou observação no cliente oficial. Documentar **como reproduzir** (passo a passo).
Não conseguiu reproduzir? → o item **não sobe** de nível. Volta para a etapa 2 ou vira backlog.

### 5. Classificação da evidência
Atribuir ★ por [EVIDENCE_LEVELS.md](EVIDENCE_LEVELS.md), declarando explicitamente se a afirmação é **sobre a aCis** ou **sobre o retail**.
🚧 **Portão:** abaixo de ★★★★ (ou ★★★☆☆ que não altera gameplay) → **PARA AQUI**. Registra no backlog do sistema como *hipótese de pesquisa*. **Não implementa.**

### 6. ADR
Obrigatório quando a mudança altera gameplay, arquitetura ou uma decisão congelada. O ADR referencia a evidência e o nível ★. Ver [ADR-003](../../adr/ADR-003-retail-first.md) (o que pode mudar) e [ADR-004](../../adr/ADR-004-estrategia-versionamento.md) (versionamento/tags).

### 7. Implementação
- **Uma** mudança lógica por vez (ADR-005).
- **No estilo do autor da aCis** — sem modernizar, renomear, reorganizar, reindentar ou "melhorar" de passagem.
- Branch dedicada (`feature/*` ou `development/*`).

### 8. Build
`JDK 21 + Apache Ant` — **0 erros**. Ver [Build.md](../../engineering/BUILD.md) e [BUILD_VALIDATION.md](../../engineering/BUILD_VALIDATION.md).

### 9. Runtime Validation
Servidor sobe (login + game) e o **cenário específico** da mudança é exercitado. Ver [VALIDATION_PROCESS.md](VALIDATION_PROCESS.md) e [RUNTIME_VALIDATION.md](../../engineering/RUNTIME_VALIDATION.md).

### 10. Logs
**0 `[ERROR]` e 0 `[ WARN]` novos** em relação à baseline. Anexar o trecho relevante ao relatório da mudança.

### 11. Commit
Atômico, Conventional Commits, corpo citando: evidência, nível ★, fonte, ADR (se houver) e como reverter.

## Portões (gates) — resumo
| Portão | Onde | Critério |
|--------|------|----------|
| **G1 — Evidência** | etapa 5 | ≥ ★★★★ (ou ★★★☆☆ sem impacto em gameplay). Senão: backlog. |
| **G2 — Política** | antes da 7 | Os 6 critérios de [CHANGE_ACCEPTANCE_POLICY.md](CHANGE_ACCEPTANCE_POLICY.md). |
| **G3 — Técnico** | 8–10 | Build 0 erros · runtime OK · logs limpos. |
| **G4 — Revisão** | 11 | PR revisado; merge só com aprovação do dono. |

## O que esta metodologia proíbe explicitamente
- Implementar por memória, opinião, "faz sentido" ou "todo servidor faz assim".
- Usar outro emulador como prova de retail.
- Usar o código da aCis como prova de retail.
- Agrupar duas mudanças num commit "porque são parecidas".
- Pular a validação empírica "porque é óbvio".
