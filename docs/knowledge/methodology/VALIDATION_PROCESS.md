# Processo de Validação — LineBR Legacy

> Como provar que uma mudança faz o que promete **e** não quebra o resto. Etapas 8–10 da [METHODOLOGY.md](METHODOLOGY.md).

---

## 1. Validação de evidência (antes do código)

### 1.1 Reprodução do comportamento
Escrever uma **receita** que qualquer dev siga:
```
Cenário: <o que observar>
Pré-condições: <estado do servidor/personagem/zona>
Passos: 1… 2… 3…
Observado na aCis: <resultado + como medir>
Esperado (retail): <resultado + fonte/evidência ★>
Como medir: <log, captura de pacote, debug GM (ExServerPrimitive), consulta ao banco>
```

### 1.2 Ferramentas de medição disponíveis (aCis 409)
| Ferramenta | Uso |
|------------|-----|
| **Debug GM `ExServerPrimitive`** | desenha linhas/pontos no cliente — ex.: `_isDebugMove`/`_isDebugPath` do movimento |
| **Logs do servidor** | `log/console`, `log/error`, `stdout` |
| **Captura de pacotes** | comparar wire-format entre aCis e referência |
| **Consulta ao MariaDB** | estado persistido (`acis`) |
| **Runtime local** | ambiente validado na Sprint 002 ([ENVIRONMENT_SETUP.md](../../engineering/ENVIRONMENT_SETUP.md)) |

## 2. Validação técnica (depois do código)

### 2.1 Build
```bash
export JAVA_HOME=/c/dev/tools/jdk-21.0.4+7
export ANT_HOME=/c/dev/tools/apache-ant-1.10.14
export PATH="$JAVA_HOME/bin:$ANT_HOME/bin:$PATH"
cd source/aCis_gameserver && ant     # 0 erros obrigatório
cd ../aCis_datapack      && ant
```
**Critério:** `BUILD SUCCESSFUL`, **0 erros**. Warnings novos devem ser justificados. Ver [BUILD_VALIDATION.md](../../engineering/BUILD_VALIDATION.md).

### 2.2 Runtime Validation
```
1. MariaDB no ar (banco acis, usuário linebr_app)
2. LoginServer  → "Loginserver ready on 127.0.0.1:2106."
3. GameServer   → "Gameserver has started" + "Registered as server: [1] …"
4. Exercitar o CENÁRIO da mudança (receita da §1.1)
5. Encerrar
```
Baseline de referência (Sprint 002): login+game sobem com **0 ERROR / 0 WARN**. Ver [RUNTIME_VALIDATION.md](../../engineering/RUNTIME_VALIDATION.md).

### 2.3 Logs
```bash
grep -c '\[ERROR\]'            stdout_game.log   # esperado: 0
grep -c '\[ WARN\]'            stdout_game.log   # esperado: 0
grep -c 'Exception in thread'  stdout_game.log   # esperado: 0
```
**Critério:** nenhuma ocorrência **nova** em relação à baseline. Anexar o diff ao relatório.

### 2.4 Comparação com `runtime-reference/` (quando aplicável)
Para mudanças no core, comparar o `l2jserver.jar` gerado com o preservado — a diferença deve ser **exatamente** a esperada, nada mais:
```bash
diff -rq <jar-extraido-novo> <jar-extraido-runtime-reference>
```
Baseline conhecida: **2.881/2.881 classes byte-idênticas** na rev 409 pura (só o `MANIFEST.MF` difere). Qualquer classe extra alterada = efeito colateral não intencional.

## 3. Relatório obrigatório da mudança
Toda alteração entrega:
| Campo | Conteúdo |
|-------|----------|
| Arquivos alterados | lista |
| Métodos alterados | lista |
| Linhas +/− | contagem |
| Evidência | nível ★ + fonte |
| Risco | baixo/médio/alto/crítico + motivo |
| Compatibilidade | cliente / banco / datapack |
| Muda gameplay? | sim/não (se sim → ADR) |
| Altera protocolo? | sim/não |
| Altera banco? | sim/não (migração?) |
| Altera datapack? | sim/não |
| Build | resultado |
| Runtime | resultado + cenário exercitado |
| Logs | ERROR/WARN antes × depois |
| Rollback | comando exato (`git revert <sha>`) |

## 4. Limitações conhecidas do ambiente atual (declarar sempre)
| Limitação | Efeito na validação |
|-----------|---------------------|
| **Sem geodata** | pathfinding/colisão de terreno **não** são exercitados |
| **Sem cliente Interlude** | fluxo de cliente (login→mundo) não validável ponta a ponta |
| **Sem referência L2OFF** | impossível validar "retail" empiricamente (bloqueia ★★★★) |
| Servidor destacado (sem console) | shutdown limpo via `//shutdown` não testável |

> Enquanto essas limitações existirem, **declare-as** em todo relatório. Omitir limitação é falsear validação.
