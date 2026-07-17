# Environment Setup — LineBR Legacy (aCis 409)

Guia para montar, do zero, um ambiente **de execução** da aCis 409 compilada. Reproduz o que foi validado na Sprint 002.

> **Princípio:** a source em `source/` **nunca** é alterada. Todos os ajustes de execução vivem na **área de runtime** (`build/dist/...` copiado para uma pasta de trabalho, ex.: `C:\dev\lbr-runtime\server`), fora do repositório. Ver [Base-Zero](../constitution/BASE_ZERO.md) e [ADR-002](../adr/ADR-002-estrutura-repositorio.md).

## 1. Requisitos

| Componente | Versão validada | Origem |
|------------|-----------------|--------|
| JDK | **Temurin 21.0.4+7** | [Adoptium](https://adoptium.net) |
| Apache Ant | **1.10.14** | [Apache](https://archive.apache.org/dist/ant/binaries/) |
| MariaDB | **10.11.10** (LTS) | [archive.mariadb.org](https://archive.mariadb.org/) |
| SO | Windows 10/11 x64 | — |

Instalação **portável** (sem admin) em `C:\dev\tools\` — ver [BUILD_VALIDATION.md](BUILD_VALIDATION.md) para JDK/Ant.

## 2. Banco de dados (MariaDB portável)

### 2.1 Inicializar e subir
```bash
MDB=/c/dev/tools/mariadb-10.11.10-winx64
# datadir isolado
"$MDB/bin/mariadb-install-db.exe" --datadir="C:\dev\lbr-runtime\mariadb-data"
# subir (bind local)
"$MDB/bin/mariadbd.exe" --datadir="C:\dev\lbr-runtime\mariadb-data" --port=3306 --bind-address=127.0.0.1 --console
```

### 2.2 Banco + usuário dedicado (NUNCA usar root para a aplicação)
```sql
CREATE DATABASE acis CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
CREATE USER 'linebr_app'@'127.0.0.1' IDENTIFIED BY '<STRONG_PASSWORD>';
CREATE USER 'linebr_app'@'localhost'  IDENTIFIED BY '<STRONG_PASSWORD>';
GRANT ALL PRIVILEGES ON acis.* TO 'linebr_app'@'127.0.0.1';
GRANT ALL PRIVILEGES ON acis.* TO 'linebr_app'@'localhost';
FLUSH PRIVILEGES;
```
> Privilégio mínimo: `USAGE` global (só login) + `ALL` **apenas** em `acis.*`. Sem acesso a outros bancos, sem privilégios administrativos.

### 2.3 Importar o schema oficial (65 arquivos)
```bash
for f in source/aCis_datapack/sql/*.sql; do
  "$MDB/bin/mysql.exe" -u linebr_app -p'<STRONG_PASSWORD>' -h 127.0.0.1 acis < "$f"
done
```
Resultado esperado: **65 tabelas**, 113 índices, 0 FK, 0 procedures, 0 triggers, engine InnoDB.

## 3. Montar a área de runtime
```bash
RUN=/c/dev/lbr-runtime/server
cp -r source/aCis_gameserver/build/dist/gameserver "$RUN/gameserver"
cp -r source/aCis_gameserver/build/dist/login      "$RUN/login"
cp -r source/aCis_datapack/build/gameserver/data/* "$RUN/gameserver/data/"   # datapack do game
cp -rn source/aCis_datapack/build/login/*          "$RUN/login/"             # serverNames.xml etc.
```

## 4. Ajustes de ambiente (SOMENTE na área de runtime — nunca na source)

| Arquivo (runtime) | Ajuste | Por quê |
|-------------------|--------|---------|
| `gameserver/config/server.properties` | `Login=linebr_app` · `Password=<...>` | usuário dedicado (não root) |
| `login/config/loginserver.properties` | `Login=linebr_app` · `Password=<...>` | idem |
| `login/config/loginserver.properties` | `AcceptNewGameServer=True` | auto-registro do GS no 1º start |
| `login/config/loginserver.properties` | `LoginHostname=127.0.0.1` · `LoginserverHostname=127.0.0.1` | segurança: bind local |
| `gameserver/config/hexid.txt` | criar com `HexID=<32 hex>` + `ServerID=1` | ID de registro do GS |
| `gameserver/config/geoengine.properties` | remover a lista de 139 regiões (`NN_NN`) | sem arquivos de geodata (idêntico ao runtime original) |

> Estes ajustes **não alteram gameplay**. São exatamente as mesmas escolhas do operador do runtime original (o `runtime-reference` também roda sem geodata e com credenciais próprias).

## 5. Portas

| Porta | Serviço | Exposição recomendada |
|-------|---------|-----------------------|
| 2106 | LoginServer (cliente) | pública (produção) / local (teste) |
| 9014 | Login ↔ GameServer (interno) | **127.0.0.1 apenas** |
| 7777 | GameServer (cliente) | pública (produção) / local (teste) |
| 3306 | MariaDB | **127.0.0.1 apenas** |

## 6. Execução
```bash
export JAVA_HOME=/c/dev/tools/jdk-21.0.4+7; export PATH="$JAVA_HOME/bin:$PATH"
# 1) LoginServer
cd $RUN/login      && java -Xmx32m -cp "libs/*" net.sf.l2j.loginserver.LoginServer
# aguarde "Loginserver ready on 127.0.0.1:2106."
# 2) GameServer
cd $RUN/gameserver && java -Xmx2G  -cp "libs/*" net.sf.l2j.gameserver.GameServer
# aguarde "Gameserver has started" e "Registered as server: [1] Bartz."
```
> No Windows, o separador de classpath é `;`. Os scripts `.sh` originais usam `:` (Unix) — por isso rodamos o `java` diretamente com `-cp "libs/*"`.

## 7. Logs
- Saída principal: redirecionar para `stdout_*.log` (feito acima) e/ou `log/` (aCis grava `log/console`, `log/error`).
- Sucesso esperado: **0 `[ERROR]`, 0 `[ WARN]`, 0 `Exception in thread`**.

## 8. Shutdown
- **Limpo (produção):** comando GM `//shutdown` no cliente, ou `Ctrl+C` no console do servidor → aciona o hook `net.sf.l2j.gameserver.Shutdown` (salva dados, desconecta jogadores).
- **MariaDB:** `mysqladmin -u root -h 127.0.0.1 shutdown`.
- Em execução **destacada** (sem console/cliente), só é possível terminar o processo (o hook de save não roda) — use apenas em teste sem jogadores.

## 9. Solução de problemas (encontrados na Sprint 002)

| Sintoma | Causa | Solução |
|---------|-------|---------|
| `Access denied for user ... (using password: NO)` | Password vazio no `.properties` | Preencher `Password=` no config de runtime |
| `Could not parse file: serverNames.xml` | datapack do login não copiado | copiar `aCis_datapack/build/login/*` para o dir do login |
| `NumberFormatException: Cannot parse null` (gameserver) | `hexid.txt` ausente | criar `config/hexid.txt` (HexID + ServerID) |
| `Failed to load 139 L2OFF region files` → crash | geodata listado mas ausente | remover as linhas `NN_NN` de `geoengine.properties` |
| GameServer não aparece p/ o cliente | GS não registrado no login | `AcceptNewGameServer=True` + hexid válido |
