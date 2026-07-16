# Build — LineBR Legacy (aCis 409)

Guia para compilar a source em `source/`. **Nenhuma alteração de código é necessária.**

## Requisitos

| Ferramenta | Versão | Observação |
|------------|--------|------------|
| **JDK** | **21** (obrigatório) | O `build.xml` falha explicitamente sem JDK 21 (`fail unless="JDK21.present"`). |
| **Apache Ant** | 1.10.x | O runtime original foi buildado com **Ant 1.10.14**. |
| **MariaDB** | 10.x/11.x | Para rodar; não é necessário para compilar. |
| **Git** | com `core.longpaths=true` | Necessário no Windows por causa dos caminhos profundos da AI. |

> **Prova de compilabilidade:** o `runtime-reference/gameserver/libs/l2jserver.jar` foi gerado desta mesma source — seu `MANIFEST.MF` registra `Ant 1.10.14` + `Created-By: 21.0.4+8-LTS-274 (Oracle)`. A source compila limpa.

## Passos (a partir da raiz do repo)

### 1. GameServer + LoginServer (um build gera os dois)
```bash
cd source/aCis_gameserver
ant                     # target padrão: clean → compile → jar → dist
```
Saída (ignorada pelo Git):
- `build/dist/gameserver/` → contém `libs/l2jserver.jar`
- `build/dist/login/`      → loginserver

### 2. Datapack
```bash
cd ../aCis_datapack
ant
```
Empacota `data/` (html/xml) e `sql/` para distribuição.

### 3. Banco de dados
```bash
# criar o schema (banco padrão: acis)
cd tools    # em runtime-reference/ ou aCis_datapack/tools
# usar full_install.sql / database_installer.(sh|bat) conforme o ambiente
```

## Configuração mínima antes de rodar

Editar `source/aCis_gameserver/config/server.properties`:
- `URL = jdbc:mariadb://localhost/acis`
- `Login = <usuário do banco>` (⚠️ o default é `root` — criar usuário dedicado)
- `Password = <senha>` (⚠️ o default vem vazio)

E `loginserver.properties` para restringir o **HexID/porta 9014 a `127.0.0.1`** (nunca expor à internet).

## Verificação pós-build (opcional, recomendada)

Comparar o `l2jserver.jar` recém-compilado com o de `runtime-reference/` para confirmar equivalência funcional (as classes devem casar; timestamps/ordem podem variar).

## Notas Windows

- Habilitar caminhos longos: `git config --global core.longpaths true`.
- Manter o repositório **fora do OneDrive** (ex.: `C:\dev\LineBR-Legacy`) para evitar MAX_PATH e conflitos de sincronização.
