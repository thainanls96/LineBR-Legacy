# Runtime Validation — aCis 409 (Sprint 002)

Prova de que a source oficial da aCis 409, **compilada**, **executa corretamente**. Encerra a fase de fundação.

> **Resultado:** LoginServer + GameServer sobem com **0 erros e 0 warnings**, o GameServer registra-se no LoginServer, o banco importa e opera sem inconsistências, e ambos aceitam conexões de rede. Fundação **operacional**.

## 1. Ambiente utilizado

| Componente | Versão |
|------------|--------|
| JDK | Temurin 21.0.4+7 |
| Apache Ant | 1.10.14 (build da Sprint 001) |
| MariaDB | 10.11.10 (portável, `127.0.0.1:3306`) |
| Artefato | `l2jserver.jar` compilado da source (Sprint 001) |
| SO | Windows 11 x64 |

Detalhes de instalação/execução em [ENVIRONMENT_SETUP.md](ENVIRONMENT_SETUP.md).

## 2. Banco de dados (ETAPA 2)

| Verificação | Resultado |
|-------------|-----------|
| Importação (65 arquivos SQL) | **65/65 OK, 0 erros** |
| Tabelas | **65** |
| Índices | 113 |
| Foreign keys | 0 (aCis não usa FK) |
| Procedures / Triggers | 0 / 0 |
| Engine | InnoDB (todas) |
| Tabelas-chave | `accounts`, `gameservers`, `characters`, `items`, `clan_data` ✅ |
| Dados iniciais | seed presente (clanhall 44, castle 9, seven_signs_festival 10, …) |
| Usuário | `linebr_app` (não-root; `ALL` só em `acis.*`) |

## 3. Execução dos servidores (ETAPA 3)

### LoginServer
```
Loginserver ready on 127.0.0.1:2106.
Listening for gameservers on 127.0.0.1:9014.
Loaded 127 server names.  Loaded 0 banned IP(s).
```
### GameServer
```
Loaded 857 regular scripts and 6 scheduled scripts.
Spawned 2616 Seven Signs - Event NPCs.  (+ NPCs, boats, sieges, events)
Loaded 93 admin / 74 skill / 26 item / 25 target / 15 user command handlers.
Gameserver has started, used memory: 358 / 2048 Mo.  Maximum allowed players: 100.
Registered as server: [1] Bartz.
```
LoginServer confirmou: `Hooked [1] Bartz gameserver on: 127.0.0.1.`

| Métrica | LoginServer | GameServer | MariaDB |
|---------|-------------|------------|---------|
| Inicialização | imediata (< 5 s) | **~45 s** (datapack + scripts + spawns) | — |
| Memória (início) | ~68 MB | **358 MB** (log) / ~760 MB working set | ~24 MB |
| Heap configurado | `-Xmx32m` | `-Xmx2G` | — |
| Portas | 2106 + 9014 | 7777 | 3306 |
| **Warnings / Erros** | **0 / 0** | **0 / 0** | 0 |

## 4. Fluxo de cliente (ETAPA 4) — até o limite do ambiente

| Passo | Status |
|-------|--------|
| LoginServer aceita conexão + envia pacote **Init** (186 bytes) | ✅ validado (nível de protocolo) |
| GameServer aceita conexão TCP (7777) | ✅ validado |
| `AutoCreateAccounts` | `True` (conta criada no 1º login) |
| Login → seleção de servidor → criação/seleção de personagem → entrada no mundo → logout | ⚠️ **não executável** |

**Limitação declarada:** a validação do fluxo completo exige um **cliente Lineage II Interlude** (protocolo criptografado, GUI) — indisponível neste ambiente e não automatizável. Validou-se tudo o que **não** depende do cliente: listeners de rede ativos, handshake inicial do login (pacote Init real), registro GS↔LS e prontidão do mundo.

## 5. Auditoria de logs (ETAPA 5)

| Nível | LoginServer | GameServer | Interpretação |
|-------|-------------|------------|---------------|
| INFO | normal (config, pools, listeners) | normal (loaders, spawns, handlers) | ✅ comportamento esperado |
| WARNING | **0** | **0** | — |
| ERROR | **0** | **0** | — |

Ocorrências investigadas e resolvidas como **ajuste de ambiente** (não são bugs da aCis): password de DB vazio, `serverNames.xml` ausente, `hexid.txt` ausente, geodata listado sem arquivos. Todas documentadas em [ENVIRONMENT_SETUP.md](ENVIRONMENT_SETUP.md#9-solução-de-problemas-encontrados-na-sprint-002). Nenhum indício de comportamento suspeito ou problema real de código.

## 6. Auditoria técnica (ETAPA 6)

| Pergunta | Resposta |
|----------|----------|
| Indício de corrupção? | **Não.** `CHECK TABLE` → todas OK após execução |
| Arquivo inconsistente? | **Não** |
| Configuração incorreta? | Apenas ajustes **intencionais** de ambiente (credenciais, geodata, hexid, bind) |
| Diferença runtime-reference × ambiente em execução? | Somente **config operacional** (mesmas escolhas do operador original); source e datapack byte-idênticos |
| Source oficial íntegra? | **Sim.** `git status` limpo, `source/` intocada, tag `acis-409-runtime-base` e `main` preservadas |

## 7. Conclusão

✅ A fundação da aCis 409 **compila (Sprint 001) e executa (Sprint 002)** corretamente, com banco, login e game operacionais e sem erros. Está pronta para receber as revisões oficiais 410/411.
