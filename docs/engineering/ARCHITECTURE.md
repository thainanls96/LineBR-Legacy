# Arquitetura — aCis 409

A **aCis** é um emulador de Lineage II (chronicle **Interlude**), escrito em Java, derivado historicamente do L2J e mantido como projeto enxuto por Tryskell. A revisão **409** é a base do LineBR Legacy.

## Componentes

A aCis moderna concentra **core + login** em um único projeto de source (`aCis_gameserver`) e mantém o **datapack** separado.

```
source/
├── aCis_gameserver/
│   ├── java/net/sf/l2j/
│   │   ├── Config.java, Server.java          ← bootstrap
│   │   ├── commons/         (61 .java)        ← utilidades, pool, rede (ex-"mmocore")
│   │   ├── gameserver/      (~2200 .java)     ← lógica do mundo, IA, skills, itens
│   │   └── loginserver/     (55 .java)        ← autenticação, GameServer registration
│   ├── config/              (10 .properties)  ← server, players, npcs, siege, loginserver…
│   ├── lib/                 mariadb-java-client-3.1.4.jar
│   ├── dist/                scripts de start (Game/Login/SQLAccountManager)
│   └── build.xml            (Apache Ant)
└── aCis_datapack/
    ├── data/                html (15.320) + xml (399)  ← NPCs, quests, multisell, zonas, skills
    ├── sql/                 (67)                       ← schema + seed do banco
    ├── tools/               instaladores de banco
    └── build.xml
```

> **MMOCore:** nas revisões antigas existia um módulo `aCis_mmocore` separado. Ele foi **removido/fundido** (commit oficial *"Delete legacy aCis_mmocore"*); sua funcionalidade de rede vive hoje em `commons`.

## Divisão de responsabilidades

| Camada | Papel |
|--------|-------|
| **LoginServer** | Autentica contas, mantém a lista de GameServers, entrega a sessão. Compila para `dist/login`. |
| **GameServer** | Simula o mundo: jogadores, NPCs, IA, skills, itens, clãs, cercos, economia. Compila para `dist/gameserver`. |
| **commons** | Base compartilhada: rede (mmocore), pools, math, coleções, random. |
| **Datapack** | Dados NÃO-código: diálogos (html), definições (xml), schema (sql). Editável sem recompilar. |

## Banco de dados

- SGBD: **MariaDB** (driver `mariadb-java-client-3.1.4`).
- Banco padrão da aCis: **`acis`** (configurável em `server.properties` → `URL`).
- Schema/seed: `aCis_datapack/sql/` (67 arquivos) + instaladores em `aCis_datapack/tools/`.

## Fluxo de execução

```
Cliente L2 (Interlude) ──▶ LoginServer (2106)  ──auth──▶ sessão
                                   │ (registro HexID via 9014, interno)
Cliente L2 ────────────────▶ GameServer (7777) ──JDBC──▶ MariaDB (acis)
```

## Filosofia aCis (a ser respeitada)

- Código **enxuto e coeso**; evita over-engineering e "features de painel".
- Datapack em XML/HTML legível.
- Sem customizações "de graça" no core — customização é responsabilidade de quem deriva.

O LineBR Legacy **mantém essa filosofia** na fase atual: nenhuma custom é adicionada até a base 409 → 410 → 411 estar consolidada.
