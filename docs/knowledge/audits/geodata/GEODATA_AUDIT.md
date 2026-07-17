# Auditoria de Geodata — Sistema B01

> **Sprint 011 — auditoria READ-ONLY.** Nenhum arquivo copiado, nenhuma config alterada, GeoEngine não habilitada.
> **Material auditado:** `C:\Users\thain\Downloads\geodata` (766 MB, 142 arquivos)
> **Base de comparação:** aCis 409 (EV-001, commit `55ff8a4e`)

---

## Veredito executivo

| | |
|---|---|
| **Origem** | ✅ **Oficial aCis** — Readme é o *"GEODATA COMPENDIUM, by Tryskell and Hasha"* (Tryskell = autor da aCis) |
| **Formato** | **L2D** — formato **próprio da aCis**, posterior à revisão 409 |
| **Integridade** | ✅ **Boa** — 139 arquivos, 0 vazios, tamanhos coerentes |
| **Cobertura** | ✅ **Perfeita** — **139/139 regiões** batem exatamente com a `geoengine.properties` |
| **Compatibilidade com aCis 409** | 🔴 **INCOMPATÍVEL** — a 409 só suporta **L2J** e **L2OFF** |
| **Pode ser usada hoje?** | ❌ **Não, como está** |

> **Resumo honesto:** a geodata é **legítima, íntegra e tem exatamente a cobertura certa** — mas está no formato **errado para a nossa base**. Não é um problema de qualidade; é um problema de versão.

---

## 1. Estrutura (ETAPA 1)

```
Downloads/geodata/
└── geodata/
    ├── 139 × *.l2d          (16_10.l2d … 26_16.l2d)
    ├── Readme.txt           (GEODATA COMPENDIUM — by Tryskell and Hasha)
    ├── geo_bugs.txt
    └── Interlude-real-geodata.jpg
```
| Métrica | Valor |
|---------|-------|
| Total | **766 MB** · 142 arquivos · 2 diretórios |
| Geodata | **139 × `.l2d`** |
| Tamanhos | 0.2 MB – 22.6 MB (**média 5.5 MB**, total 764.7 MB) |
| Nomenclatura | `{regiãoX}_{regiãoY}.l2d` |

**Ligação com o pack original:** `geo_bugs.txt` e `Interlude-real-geodata.jpg` são **byte-idênticos (md5)** aos que já existem em `runtime-reference/gameserver/data/geodata/`. Ou seja: **o pack original do LineBR foi distribuído com a "documentação" desta geodata, mas sem os arquivos de dados.** Este download é o complemento que faltava — da mesma linhagem.

## 2. Formato (ETAPA 2)

**É L2D — formato próprio da aCis.** Evidência direta do Readme (autor da aCis):

> *"aCis introduces a new geodata file format, named **L2D**. It holds diagonal movement informations, in addition to regular NSWE flags."*

| Formato | É este? | Por quê |
|---------|:-------:|---------|
| **L2D (aCis)** | ✅ **SIM** | extensão `.l2d` + Readme oficial do autor |
| L2OFF | ❌ | L2OFF usa `{x}_{y}_conv.dat` com header de 18 bytes |
| L2J | ❌ | L2J usa `{x}_{y}.l2j`, tipo de bloco em 1 byte (0/1/2) |
| Mobius | ❌ | Mobius usa `.l2j`/derivados; o Readme é da aCis |

## 3. Integridade (ETAPA 3)

| Verificação | Resultado |
|-------------|-----------|
| Arquivos corrompidos | ❌ nenhum indício |
| Arquivos vazios (0 bytes) | **0** |
| Arquivos suspeitos (<100 KB) | 0 |
| Sequência incompleta | ❌ não — 139/139 |
| Regiões faltando | **0** |

**Variação de tamanho (0.2 – 22.6 MB) é esperada e saudável:** regiões planas (mar/deserto) usam blocos *flat* compactos; regiões densas (cidades, torres, multicamada) usam blocos *complex*/*multilayer*. `16_10.l2d` = 22.6 MB (maior) é coerente com uma região de alta complexidade.

## 4. Compatibilidade com a aCis 409 (ETAPA 4)

### 🔴 INCOMPATÍVEL — evidência tripla no código

**(a) O enum `GeoType` só tem dois valores** (`enums/GeoType.java`):
```java
L2J  ("%d_%d.l2j"),
L2OFF("%d_%d_conv.dat");
```
Não existe `L2D`. `Config.GEODATA_TYPE = Enum.valueOf(GeoType.class, ...)` → **`GeoDataType = L2D` lançaria exceção no boot**.

**(b) A própria `geoengine.properties` documenta só dois formatos:**
```
# L2J:   Using L2J geodata files (filename e.g. 22_16.l2j)
# L2OFF: Using L2OFF geodata files (filename e.g. 22_16_conv.dat)
GeoDataType = L2OFF
```

**(c) O código não tem nenhuma referência a L2D.** As 2 ocorrências de "l2d" no grep são **falso-positivo** (`L2DarknessFestival`).

### Renomear `.l2d` → `_conv.dat` funcionaria? ❌ **NÃO**

O `GeoEngine.loadGeoBlocks` (linha 118+) parseia assim:
- **L2OFF:** pula **18 bytes de header** → lê tipo de bloco como `short` → `FLAT(0)` / `COMPLEX_L2OFF(0x40)` / default→multilayer
- **L2J:** sem header → tipo de bloco como `byte` → `FLAT(0)` / `COMPLEX(1)` / `MULTILAYER(2)`

Os `.l2d` **começam todos com `0xd0`/`0xd1`** (208/209):
- como **L2J** → `Unknown block type: -47` → `IllegalArgumentException` na 1ª leitura;
- como **L2OFF** → os 18 primeiros bytes seriam comidos como "header" (mas não são header: `16_10.l2d` não contém `0x10`/`0x0A` no início), e os tipos lidos cairiam no `default:` → **misparse silencioso** → geometria inválida.

> ⚠️ **O pior cenário não é falhar — é "funcionar".** Um misparse produziria geodata **corrompida mas carregada**: o servidor acharia que tem colisão válida e tomaria decisões erradas de movimento e line-of-sight. Isso é **pior do que rodar sem geodata**, porque o erro fica invisível.

### Conversão é necessária? ✅ Sim — e **não existe conversor na aCis 409**
Busca por conversor no projeto: **nenhum encontrado**.

## 5. Cobertura (ETAPA 5)

✅ **PERFEITA — 139/139**

| Comparação | Resultado |
|------------|-----------|
| Regiões no download | 139 |
| Regiões na `geoengine.properties` | 139 |
| **Coincidem** | **139** |
| Só no download | **0** |
| **Faltando** | **0** |

**Grade coberta:** X = 16–26 · Y = 10–25 → mapa **Interlude completo**.

> A correspondência exata com a lista da config **não é coincidência**: esta geodata foi produzida para exatamente este conjunto de regiões. É a geodata certa do mapa certo.

## 6. Como a aCis carrega geodata (ETAPA 6)

```
GameServer.main (GameServer.java:111)
   └─▶ GeoEngine.getInstance()                      (GameServer.java:193)
        └─▶ GeoEngine.<init>  (GeoEngine.java:76)
             └─▶ para cada região listada na geoengine.properties:
                  loadGeoBlocks(regionX, regionY)   (GeoEngine.java:118)
                    ├─ filename = GEODATA_TYPE.getFilename() → "%d_%d_conv.dat" | "%d_%d.l2j"
                    ├─ filepath = GEODATA_PATH + filename    (./data/geodata/)
                    ├─ RandomAccessFile + FileChannel.map(READ_ONLY).load()   ← mmap + load
                    ├─ buffer.order(LITTLE_ENDIAN)
                    ├─ L2OFF → pula 18 bytes de header
                    ├─ 256 × 256 blocos por região (REGION_BLOCKS_X/Y)
                    │    └─ tipo → BlockFlat | BlockComplex | BlockMultilayer
                    ├─ se sobrar byte → WARN "Region file can be corrupted"
                    └─ em erro → loadNullBlocks(região) + ERROR
   └─▶ PathFinder (A*) usa os blocos carregados
```
**Componentes:** `GeoEngine` (fachada) · `geodata/{ABlock, BlockFlat, BlockComplex, BlockMultilayer, +Dynamic, GeoStructure}` · `pathfinding/{PathFinder, Node}`.
**Constantes:** `REGION_BLOCKS = 256×256` · `CELL_HEIGHT = 8`.

## 7. Riscos (ETAPA 7)

| Risco | Nível | Análise |
|-------|:-----:|---------|
| **Incompatibilidade de formato** | 🔴 **CERTO** (não é risco — é fato) | aCis 409 não lê L2D |
| **Misparse silencioso** (se renomear) | 🔴 **Crítico** | geodata corrompida "funcionando" → movimento/LoS errados e invisíveis |
| **Falha no boot** | 🟠 Alto | `GeoDataType = L2D` → `Enum.valueOf` lança exceção → servidor não sobe |
| **Regiões inválidas** | 🟢 Baixo | as regiões estão corretas (139/139); o problema é o formato |
| **Consumo de memória** | 🟠 **Alto (atenção)** | 766 MB mapeados via `mmap().load()`. O Readme exige **64-bit + `-Xmx2g`**. Nosso `GameServer_loop.sh` já usa `-Xmx2G` ✅, **mas a VPS tem só 3.8 GB de RAM total** — geodata (~766 MB off-heap) + heap 2 GB + MariaDB + SO fica **apertado** |
| **Travamento** | 🟡 Médio | `.load()` força carga completa na inicialização → boot mais lento e pico de I/O |
| **Arquivos corrompidos** | 🟢 Nenhum | integridade boa |

## 8. Plano de instalação futura (ETAPA 8) — **não executar agora**

> ⚠️ **Pré-condição bloqueante:** obter geodata em formato **L2OFF (`_conv.dat`)** ou **L2J (`.l2j`)** — **ou** um conversor L2D→L2OFF validado. **Nada abaixo deve ser feito com os `.l2d` atuais.**

### Ordem de backup
1. `git status` limpo; branch dedicada (`development/geodata`).
2. Backup do `geoengine.properties` atual (`.bak` datado).
3. Snapshot do runtime (`C:\dev\lbr-runtime\server`) e do banco (`mysqldump acis`).
4. Confirmar que a tag `acis-409-runtime-base` está intacta.

### Ordem de configuração
1. Copiar os arquivos de geodata para `<runtime>/gameserver/data/geodata/` — **nunca** para `source/` (é dado, não código; `.gitignore` deve cobrir).
2. `geoengine.properties`: definir `GeoDataType` **conforme o formato real obtido** (`L2OFF` ou `L2J`).
3. Restaurar a **lista de 139 regiões** (hoje removida — ver `ENVIRONMENT_SETUP`).
4. Conferir `-Xmx2G` (já é o padrão) e **RAM livre ≥ 3 GB**.

### Ordem de validação
1. Subir **apenas 1 região** primeiro (config com 1 bloco) → validar carga sem erro.
2. Log deve mostrar **`Loaded 1 region file`**, sem `WARN ... can be corrupted` e sem `ERROR loading`.
3. Subir as 139 → esperar **`Loaded 139 L2OFF region files`** e **0 falhas**.
4. Medir: tempo de boot, RAM (heap + RSS), CPU.
5. Validar pathfinding com o **debug de GM** (`ExServerPrimitive`, `_isDebugPath`) — ver `audits/movement/MOVEMENT_FLOW.md`.
6. Testar movimento em terreno acidentado (o "Falling/Climb bug", `|ΔZ|>100`).

### Ordem de rollback
1. Sintoma de falha: `ERROR loading ... region file` · `WARN ... can be corrupted` · OOM · boot > aceitável.
2. Parar o servidor.
3. Restaurar `geoengine.properties.bak` (volta a rodar **sem** geodata — estado atual, comprovadamente funcional).
4. Remover os arquivos de geodata do runtime.
5. Subir e confirmar baseline da Sprint 002 (**0 ERROR / 0 WARN**).
6. Registrar o ocorrido neste documento.

## 9. Grau de confiança

| Aspecto | Confiança |
|---------|-----------|
| Origem oficial aCis | ★★★★★ (Readme do próprio autor) |
| Formato = L2D | ★★★★★ (Readme + extensão + bytes) |
| Incompatibilidade com 409 | ★★★★★ (enum + config + código + bytes) |
| Integridade | ★★★★☆ (estrutural; não parseada por falta de leitor) |
| Cobertura correta | ★★★★★ (139/139 exato) |

## 10. Conclusão

**Esta geodata NÃO pode ser usada no LineBR Legacy como está.** Não por má qualidade — ela é oficial, íntegra e tem a cobertura exata — mas porque está em **L2D**, formato introduzido pela aCis **depois da revisão 409**, e a nossa base só lê **L2J** e **L2OFF**.

### Caminhos possíveis (decisão do Owner)
| # | Caminho | Viabilidade |
|:-:|---------|-------------|
| **A** | **Obter geodata em formato L2OFF (`_conv.dat`)** — é o que a config já espera | ✅ **Recomendado** — zero código, zero risco de formato |
| **B** | Obter geodata em formato **L2J (`.l2j`)** | ✅ viável (`GeoDataType = L2J`) |
| **C** | Encontrar/escrever conversor **L2D → L2OFF** | 🟠 possível, mas é código novo + risco de misparse |
| **D** | Migrar a base para uma aCis com suporte a L2D | 🔴 exige revisão > 409 (donator) — hoje indisponível |
| **E** | Renomear `.l2d` → `_conv.dat` | ❌ **NUNCA** — misparse silencioso, pior que sem geodata |

> **Guardar este download.** Ele é oficial, íntegro e com cobertura perfeita — se um dia a base suportar L2D (ou surgir um conversor), ele é imediatamente aproveitável.
