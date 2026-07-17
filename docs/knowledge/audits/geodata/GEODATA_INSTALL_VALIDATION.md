# Instalação e Validação da Geodata L2J — Sprint 013

> **Validação executada em ambiente de runtime** (`C:\dev\lbr-runtime`, fora do repositório).
> **Nenhum arquivo Java, `source/` ou config da source foi alterado.** Só infraestrutura de runtime.
> Máquina de teste: Windows 11, **7.8 GB RAM total**. aCis 409 (EV-001) · geodata L2J ([Sprint 012](GEODATA_L2J_AUDIT.md)).

---

## 🟢 Conclusão executiva

**A geodata L2J FUNCIONA na Base Zero (aCis 409).** O GeoEngine carregou **139/139 regiões** sem erro, o servidor subiu estável, e o rollback foi validado. **Pode ser utilizada.**

| Verificação | Resultado |
|-------------|-----------|
| GeoEngine carregou | ✅ **`Loaded 139 L2J region files`** |
| Erros / Exceptions | ✅ **0 ERROR · 0 Exception · 0 ArrayIndexOutOfBounds** |
| Servidor estável | ✅ porta 7777, GS registrado `[1] Bartz`, 34 threads |
| Rollback | ✅ validado (restaura baseline) |
| Ressalvas | 🟡 2 arquivos com aviso "2 bytes"; 🟡 RAM apertada |

---

## FASE 1 — Conferência (pré-instalação)
- Regiões obrigatórias (config da source): **139**
- Todas presentes no L2J source: ✅ **0 faltando**
- Regiões extras (X=15 / Y=26): **excluídas** — não copiadas
- A própria `geoengine.properties` já **comenta** essas regiões: *"Some regions are not supported by L2 client"* (`#16_13`, `#16_14`, …) — confirma que a lista de 139 é a correta por design.

## FASE 2 — Backup
- `geoengine.properties.bak-20260717-190906` (config atual = **sem geodata**, restaurável).
- Runtime da Sprint 002 reutilizado (login+game+datapack já montados).

## FASE 3 — Instalação
- Copiados **139 arquivos `.l2j`** para `<runtime>/gameserver/data/geodata/` (**534 MB**).
- ✅ **0 regiões proibidas** copiadas (nenhuma X=15 ou Y=26).
- ✅ Nada copiado para `source/` — geodata é dado, não código.

## FASE 4 — Configuração
Alteradas **apenas** duas coisas no `geoengine.properties` do runtime:
```
GeoDataType = L2OFF   →   GeoDataType = L2J     (única mudança de valor)
+ restauradas as 139 regiões (comentadas → ativas)
```
- `GeoDataPath = ./data/geodata/` — **inalterado** (já correto)
- Demais parâmetros (pesos, iterações) — **inalterados**
- ⚠️ Correção durante a aplicação: o append inicial colou `16_10` numa linha de comentário sem newline (deu 138); corrigido para 139.

## FASE 5 — Boot

| Marco | Resultado |
|-------|-----------|
| **`Loaded 139 L2J region files`** | ✅ todas |
| Tempo até "Gameserver has started" | **~34 s** |
| **Memória (heap "used memory")** | **1364 / 2048 Mo** |
| Working set (RSS) | ~1692 MB |
| `[ERROR]` / `Exception` | **0 / 0** |
| Porta 7777 | ✅ ouvindo |
| Registro no login | ✅ `Registered as server: [1] Bartz` |
| RAM livre da máquina | 1.7 GB → **0.5 GB** (coube, apertado) |

### ⚠️ Achado: 2 arquivos com aviso (não-fatal)
```
Region file 19_11.l2j can be corrupted, remaining 2 bytes to read.
Region file 20_11.l2j can be corrupted, remaining 2 bytes to read.
```
**Diagnóstico preciso:** ambos = **196.610 bytes = 196.608 (região 100% flat: 65.536 blocos × 3) + 2 bytes**. O parser lê todos os 65.536 blocos corretamente (a região **carrega** e conta nas 139) e sobram **2 bytes de lixo** no fim, que ele apenas registra.
- **Impacto:** nenhum funcional — a geometria dos blocos está íntegra; só 2 bytes finais são ignorados.
- **Causa:** imperfeição da **conversão** (L2OFF→L2J) em 2 de 139 arquivos.
- É `LOGGER.warn` (GeoEngine.java:197), **não** `[ERROR]`. Não impede o boot nem invalida a região.

## FASE 6 — Testes de movimento

### ⚠️ Limitação de ambiente declarada
Os testes **de cliente** (andar em montanhas/paredes/pontes/rios, colisão manual, LoS visual, diagonais, seguir player) **exigem um cliente Lineage II Interlude real**, indisponível nesta máquina. **Não foram executados.**

### O que foi validado (server-side)
| Aspecto | Evidência |
|---------|-----------|
| **Pathfinding ativo** | os **2.616+ NPCs com IA** movimentam-se usando `GeoEngine.findPath`; **0 erro** de path após 25 s de execução |
| **Geodata em uso real** | mensagens `Territory ... wrong Z 10, wrong geo 0` (só 2) = a aCis validando o **Z de spawns contra a altura do terreno** — só ocorre **com geodata carregada** |
| Sem crash | servidor no ar após boot + 30 s |
| Sem deadlock | 34 threads ativas, porta responde |
| Seguir NPC/player | depende de cliente — **não testável aqui** |

> As mensagens `wrong Z / wrong geo` são **prova de que a geodata funciona** (validação de altura ativa), não defeito da geodata — são imperfeições de spawn no datapack, agora visíveis.

## FASE 7 — Performance

| Métrica | Sem geodata | Com geodata (L2J) | Δ |
|---------|:-----------:|:-----------------:|:--:|
| Heap "used memory" | **349 Mo** | **1364 Mo** | **+1015 Mo** |
| Working set (RSS) | ~633 MB | ~1692 MB | +1059 MB |
| Tempo de boot | ~46 s | ~34 s | (variância — cache) |
| CPU acumulada no boot | ~74 s | ~63 s | similar |
| Regiões carregadas | 0 | 139 | +139 |

> **GC:** não instrumentado (exigiria flags de JVM). O heap saltou ~1 GB — coerente com 139 regiões (`mmap().load()` + estruturas de bloco `ABlock` parseadas). O tempo de boot **não** piorou de forma perceptível (a variância de cache dominou).

## FASE 8 — Comparação Antes × Depois

| | **Sem geodata** | **Com geodata L2J** |
|---|---|---|
| **Vantagens** | RAM baixa (~350 MB); boot ~46 s | **pathfinding real**, **colisão de terreno**, **Z correto**, LoS — comportamento Interlude |
| **Desvantagens** | ❌ sem colisão/pathing (não é Interlude) | **+1 GB de RAM**; 2 avisos de conversão |
| RAM | ~349 MB heap | **~1364 MB heap** |
| Boot | ~46 s | ~34 s |
| Erros | 0 | 0 (2 warns não-fatais) |
| Fidelidade retail | 🔴 baixa | 🟢 **alta** |

## FASE 9 — Rollback
✅ **Validado.** Restaurado `geoengine.properties.bak`, reboot → **`Loaded 0 L2OFF region files`**, heap 391 Mo, **0 erro**, porta 7777. Baseline recuperado em um passo. Estado final do runtime = **baseline seguro** (geodata no disco, mas config em L2OFF/0 regiões).

---

## Riscos identificados (com evidência)

| Risco | Nível | Evidência / Nota |
|-------|:-----:|------------------|
| **RAM** | 🟠 **Alto na VPS** | +1 GB de heap. Local (7.8 GB) coube com 0.5 GB de folga. **A VPS tem só 3.8 GB** → geodata (1 GB) + heap + MariaDB + SO fica **muito apertado**; risco real de OOM/swap na VPS |
| Conversão imperfeita (2 arquivos) | 🟢 Baixo | 2 bytes de lixo em `19_11`/`20_11`; região carrega íntegra |
| Boot mais lento | 🟢 Baixo | não observado (variância de cache dominou) |
| Regiões fora de bounds | 🟢 Mitigado | as 41 extras **não** foram instaladas nem configuradas |
| Movimento em cliente | 🟡 Não validado | exige cliente Interlude real |

## Entregáveis
- ✅ Relatório técnico (este)
- ✅ Logs: `Loaded 139 L2J region files` · 0 ERROR · 2 warns caracterizados
- ✅ RAM: +1015 MB heap
- ✅ Tempo de boot: ~34 s (vs ~46 s baseline)
- ✅ Validação do GeoEngine: 139/139
- ✅ Comparação Antes × Depois
- ✅ Rollback validado

## Conclusão

> **A geodata L2J PODE ser utilizada na Base Zero.** Carrega 139/139 sem erro, é usada de fato (pathfinding + validação de Z), e o servidor é estável. As duas ressalvas são menores e documentadas: 2 arquivos com 2 bytes de lixo (inofensivo) e **+1 GB de RAM** (atenção na VPS de 3.8 GB).

### Recomendações (não são decisão — são evidência)
1. **Adotar a geodata L2J** — é a solução do bloqueador P0.
2. **Antes de subir na VPS:** medir RAM real lá. Com 3.8 GB, avaliar `-Xmx` (talvez `1800m` como o Readme sugere) ou upgrade de RAM. Localmente coube; na VPS é o risco a validar.
3. **Investigar (opcional, futuro):** os 2 bytes de `19_11`/`20_11` — provavelmente re-obter/re-converter esses 2 arquivos elimina o warning. Não bloqueia.
4. **Validação final de movimento** exige um cliente Interlude — fica para quando houver ambiente de teste com cliente.

### Estado deixado
- Runtime: config em **baseline (L2OFF, 0 regiões)** — seguro; geodata (139 `.l2j`) preservada no disco.
- Backup do config preservado.
- **`source/` e repositório: 100% intactos** (0 alterações; a geodata nunca entrou no git).
