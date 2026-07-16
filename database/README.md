# database/

Documentação e artefatos de banco de dados do LineBR Legacy.

## SGBD

- **MariaDB** (driver `mariadb-java-client-3.1.4`).
- Banco padrão da aCis 409: **`acis`** (definido em `source/aCis_gameserver/config/server.properties` → `URL`).

## Onde está o schema (fonte da verdade)

Para **não duplicar** arquivos (e evitar divergência), o schema/seed permanece nas árvores canônicas:

| Conteúdo | Local |
|----------|-------|
| Schema + seed (SQL) da revisão 409 | `source/aCis_datapack/sql/` (67 arquivos) |
| Instaladores de banco | `source/aCis_datapack/tools/` |
| SQL do runtime original (idêntico ao source) | `runtime-reference/sql/` |
| Backup Navicat original | `runtime-reference/Backup limpo.nb3` |

> Auditoria: os 65 `.sql` de datapack são **byte-idênticos** entre source e runtime.

## Uso desta pasta

Este diretório é reservado para artefatos de banco **do desenvolvimento** que NÃO fazem parte da source pura, por exemplo (à medida que forem criados):

- migrações incrementais (ex.: mudanças de schema das revisões 410/411);
- dumps de referência para testes;
- diagramas ER e documentação de tabelas customizadas.

Nada é adicionado aqui na fase atual (Base Zero + migração de estrutura).
