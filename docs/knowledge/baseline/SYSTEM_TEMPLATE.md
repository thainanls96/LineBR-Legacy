# Template de Baseline de Sistema — LineBR Legacy

> **Obrigatório.** Copie para `docs/retail-baseline/systems/<SISTEMA>.md` ao construir a baseline de um sistema.
> Supera o `retail-knowledge-base/AUDIT_TEMPLATE.md` (a remover na consolidação).
> **Seção sem resposta = baseline incompleta.** Se não sabe, escreva **"DESCONHECIDO"** e abra item em [UNKNOWN_BEHAVIORS.md](UNKNOWN_BEHAVIORS.md). **Nunca deixe em branco nem invente.**

---

## Nome
`<Sistema>` — ID do catálogo (ex.: `B03`)

## Descrição
O que este sistema é, em 2–3 linhas, na linguagem do jogo (não do código).

## Objetivo
Por que ele existe do ponto de vista da experiência do jogador.

## Fluxo
Ciclo completo do gatilho ao efeito observável, com `arquivo:linha` em cada etapa.
```
<gatilho> → <validação> → <processamento> → <persistência> → <broadcast> → <efeito>
```

## Arquitetura
Pacotes, camadas e responsabilidades. Como as peças se encaixam.

## Classes
| Classe | Pacote | Linhas | Refs | Papel |
|--------|--------|-------:|-----:|-------|

## Pacotes (packets)
| Direção | Packet | Quando | Campos relevantes |
|---------|--------|--------|-------------------|
| C→S | | | |
| S→C | | | |
⚠️ Marcar o que é **protocolo** (área sensível).

## Configs
| Arquivo | Chave | Valor default | Efeito |
|---------|-------|---------------|--------|

## XML (datapack)
| Arquivo | Conteúdo | Volume |
|---------|----------|-------:|

## SQL
| Tabela | Colunas-chave | Papel |
|--------|---------------|-------|

## Dependências
- **Depende de:** (sistemas que precisam existir antes)
- **É usado por:** (sistemas que quebram se este mudar)
- Ver [DEPENDENCY_MAP.md](DEPENDENCY_MAP.md).

## Fluxograma
Diagrama em texto (ASCII) do caminho principal + ramificações relevantes.

## Diferenças da aCis
O que a aCis faz **de fato**, incluindo peculiaridades, heurísticas e decisões próprias.
Cada item: `arquivo:linha` + trecho. Isto é **★★★★★ sobre a aCis**.

## Diferenças Retail
Para **cada** divergência suspeita:
```
### D-NN · <título>
Fato (aCis):        <arquivo:linha>
Retail:             <o que a evidência indica>
Evidência:          ★☆☆☆☆ … ★★★★★   (EVIDENCE_LEVELS.md)
Evidence ID:        EV-NNN            (EVIDENCE_REGISTER.md)
Afirmação sobre:    [ ] aCis  [ ] retail
Reprodução:         <receita ou "não realizada">
Impacto p/ jogador: baixo / médio / alto
Natureza:           retail / anti-cheat / design aCis / bug
```

## Nível de evidência
Tabela-resumo. Declarar **quantos itens atingem ≥ ★★★★** (isto é, quantos autorizam alteração).
Se zero → dizer explicitamente: *"Nenhuma alteração autorizada neste sistema."*

## Fontes
Todas arquivadas (Wayback + data + hash). Referenciar por `EV-NNN`.
Registrar também as buscas que **falharam** — ausência de fonte é dado.

## Riscos
Por componente: 🟢 Baixo · 🟡 Médio · 🟠 Alto · 🔴 Crítico — **com motivo**.
Listar métodos que **jamais** devem ser alterados sem extremo cuidado.

## Observações
Achados relevantes que não se encaixam acima (armadilhas, code smells, notas do autor).

## Pendências
| # | Pendência | Como resolver | Prioridade |
|---|-----------|---------------|:----------:|
Itens de incerteza → espelhar em [UNKNOWN_BEHAVIORS.md](UNKNOWN_BEHAVIORS.md).

---

## Checklist de encerramento
- [ ] Todas as seções respondidas (ou marcadas `DESCONHECIDO` + item em UNKNOWN_BEHAVIORS)
- [ ] Todo `arquivo:linha` conferido no commit auditado (`55ff8a4e`)
- [ ] Toda evidência com `EV-NNN` no [EVIDENCE_REGISTER](EVIDENCE_REGISTER.md)
- [ ] Cada diferença declara ★ e "sobre aCis" vs "sobre retail"
- [ ] Hipóteses espelhadas em [RETAIL_ASSUMPTIONS](RETAIL_ASSUMPTIONS.md) (PROVADO/PROVÁVEL/DESCONHECIDO)
- [ ] [SYSTEM_CATALOG](SYSTEM_CATALOG.md) atualizado (🟢 Baseline criada)
- [ ] **Zero** arquivos fora de `/docs`
- [ ] Commit `docs(baseline): <sistema>` atômico
