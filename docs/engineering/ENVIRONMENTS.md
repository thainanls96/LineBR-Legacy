# Ambientes e Fluxo de Deploy — LineBR Legacy

> **FASE 2 + FASE 4** da infraestrutura. Define os três ambientes oficiais e o fluxo obrigatório de promoção.
> Complementa o [DEVELOPMENT_WORKFLOW.md](DEVELOPMENT_WORKFLOW.md) (que rege branches/commits) com a camada de **deploy**.

---

## Os três ambientes oficiais

```
┌──────────────────┐     ┌──────────────────┐     ┌──────────────────┐
│   1. GitHub      │     │   2. LOCAL       │     │   3. VPS         │
│  Fonte oficial   │◀───▶│  Desenvolvimento │────▶│  Homologação     │
│                  │     │                  │     │                  │
│ thainanls96/     │     │ C:\dev\          │     │ 177.7.48.204     │
│ LineBR-Legacy    │     │ LineBR-Legacy    │     │ /root/projects/  │
│                  │     │ + C:\dev\        │     │ linebr-legacy    │
│ verdade do code  │     │ lbr-runtime      │     │                  │
└──────────────────┘     └──────────────────┘     └──────────────────┘
```

### 1. GitHub — Fonte oficial do projeto
- Repositório: `github.com/thainanls96/LineBR-Legacy`
- **A verdade do código.** Toda a `source/`, documentação e histórico vivem aqui.
- `main` protegida; desenvolvimento em branches; Base Zero na tag `acis-409-runtime-base`.
- **Nunca** recebe push direto na `main` — só via PR aprovado.

### 2. Ambiente LOCAL — Desenvolvimento
- Máquina do desenvolvedor: `C:\dev\LineBR-Legacy` (repo) + `C:\dev\lbr-runtime` (servidor de teste).
- Ferramentas: JDK 21 + Ant + MariaDB (portáteis em `C:\dev\tools`).
- **Toda alteração é feita e testada AQUI primeiro.** É onde se compila, sobe login+game, valida.
- ⚠️ **Nenhuma feature experimental é desenvolvida na VPS.**

### 3. VPS — Homologação
- `177.7.48.204` · `/root/projects/linebr-legacy/`
- **Recebe apenas o que foi aprovado.** É onde se valida em ambiente parecido com produção (rede, latência, recursos reais).
- Convive com FOX (intocável) e Traefik.
- **Não é palco de desenvolvimento** — é palco de validação.

## Fluxo oficial de desenvolvimento (obrigatório)

```
   ┌─────────────────────────────────────────────────────────────┐
   │                                                             │
   │   Desenvolvimento LOCAL                                     │
   │        ↓                                                    │
   │   Testes (Build + Runtime + Logs)  ── VALIDATION_PROCESS    │
   │        ↓                                                    │
   │   Aprovação do Owner                                        │
   │        ↓                                                    │
   │   Commit (atômico, Conventional Commits)                   │
   │        ↓                                                    │
   │   Push → GitHub (branch → PR)                               │
   │        ↓                                                    │
   │   Deploy → VPS (homologação)                                │
   │        ↓                                                    │
   │   Validação na VPS                                          │
   │        ↓                                                    │
   │   Produção                                                  │
   │                                                             │
   └─────────────────────────────────────────────────────────────┘
```

**Regra inviolável:** ⛔ **Nunca desenvolver diretamente na VPS.** A VPS só recebe o que passou por Local → Testes → Aprovação → GitHub.

### Por etapa
| Etapa | Onde | Critério de passagem |
|-------|------|----------------------|
| Desenvolvimento | Local | código compila |
| Testes | Local | Build 0 erros + Runtime sobe + Logs limpos ([VALIDATION_PROCESS](../knowledge/methodology/VALIDATION_PROCESS.md)) |
| Aprovação | Owner | decisão explícita registrada |
| Commit + Push | Local → GitHub | Conventional Commits; branch, não `main` |
| Deploy | GitHub → VPS | `git pull` na VPS + build/deploy; **nunca** editar direto na VPS |
| Validação | VPS | servidor sobe, geodata carrega, 0 erro |
| Produção | VPS | aprovação final + hardening |

## Regras de deploy para a VPS
1. **Origem única:** a VPS puxa da `main` do GitHub (ou de uma tag). Nunca recebe arquivos editados à mão.
2. **Backup antes de cada deploy:** config + banco + estado atual.
3. **Rollback sempre possível:** manter a versão anterior até a nova ser validada.
4. **Geodata e dados grandes** (não versionados) são sincronizados por processo próprio (rsync/scp), fora do git.
5. **Segredos** (senha do DB, hexid) ficam **só na VPS**, nunca no git ([SERVER_RULES](../specification/SERVER_RULES.md)).
6. **FOX e Traefik** nunca são afetados por um deploy do LineBR.

## Separação de responsabilidades
| | Código | Dados/Geodata | Segredos | Runtime |
|---|:---:|:---:|:---:|:---:|
| **GitHub** | ✅ fonte | ❌ | ❌ | ❌ |
| **Local** | ✅ clone | ✅ (Downloads) | local | `lbr-runtime` |
| **VPS** | ✅ deploy | ✅ sincronizada | ✅ só aqui | `/root/projects/linebr-legacy` |
