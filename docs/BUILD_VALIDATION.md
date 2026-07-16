# Build Validation — aCis 409 (Sprint 001)

Este documento prova que a **source oficial em `source/` reproduz o runtime preservado** (`runtime-reference/` / tag `acis-409-runtime-base`) e explica como **qualquer desenvolvedor** reproduz o build.

> **Resultado:** das 2.882 entradas do `l2jserver.jar`, **2.881 classes `.class` são byte-idênticas** ao runtime. A única diferença é a linha `Created-By` do `MANIFEST.MF` (fornecedor do JDK). ✅ Fundação reprodutível.

---

## 1. Ambiente de build

| Componente | Versão usada | Versão do runtime original | Observação |
|------------|--------------|----------------------------|------------|
| **JDK** | Temurin **21.0.4+7** LTS (Eclipse Adoptium) | Oracle **21.0.4+8**-LTS-274 | Mesma versão 21.0.4; fornecedor diferente |
| **Apache Ant** | **1.10.14** | 1.10.14 | Idêntico |
| **SO** | Windows 11 x64 | — | — |

Instalação **portável** (sem admin), em `C:\dev\tools\`:
- `jdk-21.0.4+7/` — de [Adoptium](https://adoptium.net) (`OpenJDK21U-jdk_x64_windows_hotspot_21.0.4_7.zip`).
- `apache-ant-1.10.14/` — de [archive.apache.org](https://archive.apache.org/dist/ant/binaries/) (`apache-ant-1.10.14-bin.zip`).

## 2. Como reproduzir (passo a passo)

### 2.1 Instalar as ferramentas (uma vez)
```bash
mkdir -p /c/dev/tools && cd /c/dev/tools
# JDK 21.0.4 (Temurin)
curl -L -o jdk21.zip "https://github.com/adoptium/temurin21-binaries/releases/download/jdk-21.0.4%2B7/OpenJDK21U-jdk_x64_windows_hotspot_21.0.4_7.zip"
# Apache Ant 1.10.14
curl -L -o ant.zip "https://archive.apache.org/dist/ant/binaries/apache-ant-1.10.14-bin.zip"
unzip -q jdk21.zip && unzip -q ant.zip
```

### 2.2 Configurar o ambiente (por sessão de build)
```bash
export JAVA_HOME="/c/dev/tools/jdk-21.0.4+7"
export ANT_HOME="/c/dev/tools/apache-ant-1.10.14"
export PATH="$JAVA_HOME/bin:$ANT_HOME/bin:$PATH"
java -version   # deve mostrar 21.0.4
ant  -version   # deve mostrar 1.10.14
```
> No Windows, garantir `git config --global core.longpaths true` e manter o repositório **fora do OneDrive** (caminho curto, ex.: `C:\dev\LineBR-Legacy`).

### 2.3 Compilar
```bash
# GameServer + LoginServer (um build gera os dois; target padrão: dist)
cd /c/dev/LineBR-Legacy/source/aCis_gameserver
ant

# Datapack
cd ../aCis_datapack
ant
```

Saídas (todas ignoradas pelo `.gitignore`, nunca commitadas):
- `source/aCis_gameserver/build/l2jserver.jar`
- `source/aCis_gameserver/build/dist/{gameserver,login}/`
- `source/aCis_datapack/build/{gameserver/data,sql,tools,login}/`

## 3. Resultado do build

| Métrica | GameServer | Datapack |
|---------|-----------|----------|
| Status | **BUILD SUCCESSFUL** | **BUILD SUCCESSFUL** |
| Arquivos compilados | 2.343 `.java` | — |
| Arquivos sincronizados | — | 15.720 data + 65 sql + 4 tools + 1 login |
| **Warnings** | **0** | 0 |
| **Erros** | **0** | 0 |
| Tempo (Ant) | ~22 s | ~19 s |

## 4. Validação de equivalência (build vs runtime-reference)

Comparação de `source/aCis_gameserver/build/l2jserver.jar` × `runtime-reference/gameserver/libs/l2jserver.jar`:

| Verificação | Resultado |
|-------------|-----------|
| Tamanho do jar | 5.753.291 vs 5.753.294 bytes (**Δ 3 bytes**) |
| Nº de entradas `.class` | **2.881 = 2.881** |
| Conjunto de nomes de classe | **2.881/2.881 idênticos** (0 a mais, 0 a menos) |
| Classes byte-idênticas | **2.881 de 2.881** ✅ |
| Entradas que diferem | **1** — apenas `META-INF/MANIFEST.MF` |
| Diferença no manifest | linha `Created-By`: `Temurin 21.0.4+7` vs `Oracle 21.0.4+8` |

### Reproduzir a comparação
```bash
OUR=source/aCis_gameserver/build/l2jserver.jar
REF=runtime-reference/gameserver/libs/l2jserver.jar
mkdir -p /tmp/jo /tmp/jr
(cd /tmp/jo && unzip -q "$OLDPWD/$OUR"); (cd /tmp/jr && unzip -q "$OLDPWD/$REF")
diff -rq /tmp/jo /tmp/jr    # deve apontar apenas MANIFEST.MF
```

## 5. Interpretação técnica

- **A única diferença funcional é o carimbo do fornecedor do JDK** no manifest. O bytecode das 2.881 classes é **idêntico** — ou seja, o `javac` 21.0.4 (Temurin) produziu exatamente o mesmo resultado do `javac` 21.0.4 (Oracle) para esta source.
- Isso comprova que o `runtime-reference/` foi compilado **exatamente desta source** (aCis 409), sem alterações.
- O datapack já era byte-idêntico à source (auditado: 15.718/15.718 arquivos, SQL 65/65). O build apenas o sincroniza para `build/`.

## 6. Conclusão

✅ **A source oficial aCis 409 reproduz o runtime Base Zero** com fidelidade de bytecode total (2.881/2.881 classes). A fundação é **reprodutível, compilável e verificada**.
