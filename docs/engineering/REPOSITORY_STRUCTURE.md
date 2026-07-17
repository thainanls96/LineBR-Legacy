# Estrutura do Repositório — LineBR Legacy

```
LineBR-Legacy/
├── source/                 ← BASE DE DESENVOLVIMENTO (aCis 409 oficial, limpa)
│   ├── aCis_gameserver/    ← código Java (game + login + commons) + build.xml + config + lib
│   └── aCis_datapack/      ← datapack (data/html, data/xml, sql, tools) + build.xml
│
├── runtime-reference/      ← RUNTIME ORIGINAL PRESERVADO (referência histórica, NÃO editar)
│   ├── gameserver/         ← pack compilado (libs/l2jserver.jar + datapack + configs + log/)
│   ├── login/              ← loginserver compilado + configs
│   ├── sql/                ← SQL do pack
│   ├── tools/              ← instaladores de banco do pack
│   └── Backup limpo.nb3    ← backup Navicat original
│
├── database/               ← documentação/artefatos de banco (ver database/README.md)
├── docs/                   ← documentação técnica (este diretório)
├── tools/                  ← utilitários de desenvolvimento do projeto
│
├── .gitattributes          ← EOL/binários; protege runtime-reference byte-a-byte
├── .gitignore              ← ignora build outputs, IDE, logs
└── README.md
```

## Por que duas árvores (source + runtime-reference)?

| | `source/` | `runtime-reference/` |
|---|-----------|----------------------|
| **É** | código-fonte | binário compilado |
| **Contém** | 2.343 `.java` + build.xml | `l2jserver.jar` (sem `.java`) |
| **Editável?** | ✅ é onde se desenvolve | ❌ imutável, só consulta |
| **Origem** | gitlab Tryskell/acis_public @ 409 | pack `LineBRLegacy.rar` |
| **Papel** | fundação do LineBR Legacy | prova/verificação da Base Zero |

O `runtime-reference/` serve para: (1) preservar a Base Zero exatamente; (2) comparar o resultado de builds futuros contra o binário original; (3) permitir subir o servidor imediatamente sem compilar, se necessário.

## Convenções

- **Nunca** editar `runtime-reference/`.
- Todo código novo vive em `source/`.
- Artefatos gerados (`bin/`, `build/`, `log/`) são ignorados pelo `.gitignore` — nunca commitados.
- Documentação sempre atualizada em `docs/` a cada mudança estrutural.

## Ramificações

- `main` — Base Zero (runtime original). Protegida; só recebe merges aprovados.
- `development/source-migration` — esta migração (source oficial + reestruturação).
- Futuras: `development/rev-410`, `development/rev-411`, `feature/vip`, `feature/skins`, etc.
