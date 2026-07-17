# Auditoria Comparativa de Geodata — L2J vs L2D (Sistema B01)

> **Sprint 012 — auditoria READ-ONLY.** Nada copiado, nada instalado, nenhuma config alterada.
> **Material:** `Downloads/Geodata L2OFF - Convertida L2J/.../Geodata` (563 MB, 180 arquivos)
> **Comparação:** geodata L2D da [Sprint 011](GEODATA_AUDIT.md) · base aCis 409 (EV-001, `55ff8a4e`)

---

## 🟢 Veredito executivo

| | |
|---|---|
| **Formato real** | **L2J** (`.l2j`) — **não** é L2OFF |
| **Compatível com aCis 409?** | ✅ **SIM** — `GeoType.L2J("%d_%d.l2j")` é suportado nativamente |
| **Precisa de conversão?** | ❌ **Não** |
| **Precisa de mudança de código?** | ❌ **Não** — só configuração |
| **Cobre as 139 regiões da config?** | ✅ **139/139** |
| **Integridade** | ✅ Boa — 0 vazios, 0 truncados, 100% dos tipos de bloco válidos |
| **Pode ser adotada?** | ✅ **SIM** |

> **O projeto finalmente possui uma geodata compatível.** Após 8 sprints, o bloqueador P0 tem solução.

---

## 1. Estrutura (ETAPA 1)

```
Geodata/  (plano, sem subdiretórios)
└── 180 × *.l2j        (15_18.l2j … 26_16.l2j)
```
| Métrica | Valor |
|---------|-------|
| Total | **563.3 MB** · 180 arquivos · 1 diretório |
| Extensões | **180 × `.l2j`** (100%) |
| Tamanhos | 0.19 MB – 16.16 MB (**média 3.13 MB**) |
| Vazios | **0** |
| Nomenclatura | `{X}_{Y}.l2j` — **180/180** no padrão `NN_NN.l2j` |

## 2. Formato (ETAPA 2) — **é L2J, não L2OFF**

⚠️ **O nome da pasta diz "Geodata L2OFF - Convertida L2J".** Lendo com rigor: é geodata de **origem** L2OFF, **convertida para o formato L2J**. A origem L2OFF é uma **alegação do empacotador** (★☆ — não verificável). O **formato**, esse sim, foi provado nos bytes.

### Como a conclusão foi obtida (3 evidências independentes)

**(a) Tipos de bloco — o teste decisivo**
A aCis lê L2J com tipo de bloco em **1 byte**: `FLAT=0`, `COMPLEX_L2J=1`, `MULTILAYER_L2J=2` (`GeoStructure.java:26-29`).
Primeiro byte de **todos os 180 arquivos**:
```
141 arquivos → 0x00  (FLAT)
 39 arquivos → 0x01  (COMPLEX_L2J)
  0 arquivos → valor inválido
```
**100% dos valores são tipos L2J válidos.** (Comparação: os `.l2d` começam com `0xd0`/`0xd1` = 208/209 → inválidos.)

**(b) Assinatura matemática do formato**
Bloco L2J *flat* = 1 byte (tipo) + 2 bytes (altura) = **3 bytes**. Região = 256×256 = **65.536 blocos**.
→ Região 100% plana = 65.536 × 3 = **196.608 bytes**.
Arquivos `15_22.l2j` e `16_14.l2j` = **exatamente 196.608 bytes**. ✅

**(c) Estrutura interna visível**
```
15_18.l2j:  00 c0ed | 00 c0ed | 00 c0ed | 00 c0ed   ← FLAT + altura, repetindo
16_10.l2j:  01 0fd9 07d9 0fd9 0fd9 ...              ← COMPLEX + células
```
Padrão textbook do formato L2J.

## 3. Comparação com a geodata L2D (ETAPA 3)

| Aspecto | **L2J** (Sprint 012) | **L2D** (Sprint 011) |
|---------|----------------------|----------------------|
| Arquivos | **180** | 139 |
| Tamanho | 563 MB | 766 MB |
| Média/arquivo | 3.13 MB | 5.5 MB |
| Formato | **L2J** ✅ suportado | **L2D** ❌ não suportado |
| Grade | X=**15**–26 · Y=10–**26** | X=16–26 · Y=10–25 |
| Extras vs o outro | **+41 regiões** | 0 |
| Documentação | nenhuma | Readme/geo_bugs/jpg oficiais |

### Representam o mesmo mapa?
**Sim — o L2J é um superset do L2D:**
- **139 regiões em comum** (todas as do L2D estão no L2J)
- **0 regiões só no L2D**
- **41 regiões só no L2J**: `15_18..15_26`, `16_13..16_18`, `16_26`, `17_13..17_17`, `17_26`, `18_15`, `18_16`, `18_26`, `19_12`, `19_26`, `20_12`, `20_26`, `21_10..21_12`, `22_10..22_12`, `22_26`, `23_26`, `24_26`, `25_22..25_24`

**Coerência entre os dois:** a maior região é `16_10` em ambos (L2D 22.6 MB · L2J 16.16 MB). O L2D é ~40% maior por carregar **informação de movimento diagonal** além dos flags NSWE (conforme o Readme do Tryskell) — ou seja, os dois descrevem o mesmo terreno; o L2D é mais rico, o L2J é o que a nossa base lê.

## 4. Compatibilidade com a Base Zero (ETAPA 4)

| Componente | Verificação |
|------------|-------------|
| **`GeoType`** (`enums/GeoType.java`) | ✅ `L2J("%d_%d.l2j")` — **existe** |
| **`Config.GEODATA_TYPE`** (`Config.java:643`) | ✅ `Enum.valueOf(GeoType.class, "L2J")` → válido |
| **`GeoEngine.loadGeoBlocks`** (`GeoEngine.java:118`) | ✅ ramo `if (GEODATA_TYPE == GeoType.L2J)` existe e lê `byte` de tipo |
| **Nomenclatura** | ✅ `String.format("%d_%d.l2j", 16, 10)` → `16_10.l2j` — bate 180/180 |
| **Header** | ✅ L2J **não tem header** (os 18 bytes são pulados só no L2OFF) — coerente com os arquivos |
| **GeoDriver / GeoDataLoader** | ⚠️ **não existem na aCis 409** — a aCis usa `GeoEngine` + `geodata/ABlock` (são nomes de outros forks) |

### ✅ Carrega sem NENHUMA modificação de código
Basta configuração. **Zero custom.**

### 🔴 ARMADILHA: as 41 regiões extras estouram os limites do mundo
```java
World.TILE_X_MIN = 16;  TILE_X_MAX = 26;
World.TILE_Y_MIN = 10;  TILE_Y_MAX = 25;
blockX = (regionX - TILE_X_MIN) * 256;      // GeoEngine.java:139
_blocks = new ABlock[GEO_BLOCKS_X][GEO_BLOCKS_Y];   // 11×256 por 16×256
```
- Região **X=15** → `(15-16)*256 = -256` → **ArrayIndexOutOfBoundsException**
- Região **Y=26** → `(26-10)*256 = 4096` → array vai até 4095 → **ArrayIndexOutOfBoundsException**

> ⚠️ **As 41 regiões extras NÃO podem ser adicionadas à `geoengine.properties`.** Elas ficam no disco, ignoradas. Adicioná-las derruba o servidor no boot. A lista de 139 da config **já é a correta** — não é limitação da geodata, é o tamanho do mundo da aCis 409.

## 5. Integridade (ETAPA 5)

| Verificação | Resultado |
|-------------|-----------|
| Arquivos vazios | **0** |
| Arquivos abaixo do mínimo válido (196.608 B) | **0** — nenhum truncado |
| Tipos de bloco inválidos (1º byte) | **0 de 180** |
| Nomenclatura fora do padrão | **0 de 180** |
| Regiões faltando (vs config) | **0 de 139** |
| Sequência quebrada | ❌ não |
| Inconsistência estrutural | ❌ nenhuma detectada |

**Limitação declarada:** a validação completa exige **parsear** os 65.536 blocos de cada região (só o próprio GeoEngine faz isso). O que foi verificado é **estrutural** (tamanho, tipos, nomenclatura, cobertura) — forte, mas não substitui a carga real. A prova final é o teste de carga do plano de instalação.

## 6. Configuração necessária (ETAPA 6) — **não aplicar agora**

```properties
# geoengine.properties
GeoDataPath = ./data/geodata/     # (já é o padrão — não muda)
GeoDataType = L2J                 # ← ÚNICA mudança obrigatória (hoje: L2OFF)

# + restaurar a lista das 139 regiões ao final do arquivo
# (hoje removida — ver engineering/ENVIRONMENT_SETUP.md)
# ⚠️ NÃO adicionar as 41 extras (X=15 / Y=26) — estouram os bounds
```
**Onde copiar os arquivos:** `<runtime>/gameserver/data/geodata/` — **nunca** em `source/` (é dado, não código).

## 7. Motivo técnico da incompatibilidade da OUTRA (ETAPA 7)
Não se aplica a esta. Para o L2D, ver [GEODATA_AUDIT.md §4](GEODATA_AUDIT.md).

## 8. Tabela comparativa (ETAPA 8)

| Critério | **L2J (Sprint 012)** | **L2D (Sprint 011)** |
|----------|----------------------|----------------------|
| **Origem** | 🟡 alegada L2OFF convertida (★☆ — não verificável) | 🟢 **oficial aCis** (Readme do Tryskell) ★★★★★ |
| **Formato** | **L2J** — ✅ suportado | **L2D** — ❌ não suportado pela 409 |
| **Compatibilidade** | ✅ **total, sem código** | 🔴 **nenhuma** |
| **Cobertura** | ✅ 139/139 + 41 extras (inutilizáveis) | ✅ 139/139 exato |
| **Integridade** | ✅ boa (tipos 100% válidos) | ✅ boa |
| **Qualidade** | 🟡 boa — NSWE padrão | 🟢 **superior** — inclui movimento diagonal |
| **Risco** | 🟢 **baixo** (só config + teste de carga) | 🔴 **crítico** (inutilizável; rename = misparse silencioso) |
| **Recomendação** | ✅ **ADOTAR** | 📦 **guardar** para o futuro |

---

## Respostas objetivas

**1. É realmente L2OFF?** ❌ **Não — é L2J.** O nome da pasta indica origem L2OFF *convertida para L2J*. O formato provado nos bytes é **L2J**. (A origem L2OFF é alegação do empacotador, não verificável.)

**2. Pode ser usada na Base Zero?** ✅ **SIM.** `GeoType.L2J` existe na aCis 409, o parser tem o ramo L2J, a nomenclatura bate 180/180, e os 139 blocos necessários estão presentes.

**3. Precisa de conversão?** ❌ **Não.** Já está no formato que a base lê.

**4. Risco de corrupção?** 🟢 **Baixo.** Todas as verificações estruturais passaram. Risco residual: só um parse real detecta inconsistência interna — coberto pelo teste de carga incremental.

**5. Melhor ou pior que a L2D?** **Tecnicamente inferior, praticamente superior.** A L2D tem qualidade maior (movimento diagonal) e origem oficial comprovada — mas é **inutilizável** na 409. A L2J tem qualidade padrão e origem não verificável — mas **funciona hoje, sem código**. Geodata que não carrega tem qualidade zero na prática.

**6. Qual adotar?** ✅ **A L2J.** É a única viável. **Guardar a L2D** — se a base um dia suportar L2D (ou surgir conversor), ela é superior.

**7. O projeto finalmente possui geodata compatível?** ✅ **SIM.** Pela primeira vez em 8 sprints, o bloqueador P0 tem solução concreta — pendente apenas do teste de carga.
