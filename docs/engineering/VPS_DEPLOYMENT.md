# Deploy da Base Zero na VPS — Homologação

> **Sprint 014 (FASE 3).** Base Zero (aCis 409) implantada e **online** na VPS de homologação.
> **Sem gameplay, sem customs, sem rates, sem VIP.** Apenas a Base Zero funcionando.

---

## 🟢 Estado: ONLINE

| | |
|---|---|
| **LoginServer** | ✅ `Loginserver ready on *:2106` |
| **GameServer** | ✅ `Gameserver has started` + `Registered as server: [1] Bartz` |
| **Geodata** | ✅ `Loaded 139 L2J region files` |
| **Erros** | 0 `[ERROR]` (2 avisos não-fatais conhecidos: `19_11`/`20_11`) |
| **RAM** | 2499 MB usado / **1415 MB livre** (swap ~0) |
| **FOX / Traefik** | ✅ intactos |

## O que foi implantado

| Componente | Detalhe |
|-----------|---------|
| **Código** | `git clone` (deploy key read-only) da branch `development/docs-consolidation` → `ant` na VPS (JDK 21 + Ant nativos). Build 27s, `l2jserver.jar` 5.753.291 B |
| **Runtime** | `/root/projects/linebr-legacy/server/` (login + gameserver + datapack) |
| **Banco** | MariaDB 10.11.14 · DB `acis` · usuário **`linebr_app`** (não-root) · 65 tabelas |
| **Geodata** | 139 `.l2j` (534 MB) em `gameserver/data/geodata/`; `GeoDataType = L2J` |
| **Rede** | UFW abriu **2106** e **7777**; **9014 fica em 127.0.0.1** (não exposto) |
| **Segurança** | SSH endurecido: `PasswordAuthentication no`, `PermitRootLogin prohibit-password` (acesso por chave validado) |

## Estrutura na VPS
```
/root/projects/linebr-legacy/
├── repo/                    ← git clone (fonte, para rebuild/deploy)
├── server/                  ← runtime online
│   ├── login/  gameserver/  (com data/geodata/ = 139 .l2j)
│   ├── start.sh  stop.sh    ← controle manual
│   └── .db_password         ← senha do app (chmod 600, fora do git)
└── _deploy-backup/state-before.txt   ← snapshot pré-deploy
```

## Como controlar
```bash
ssh vps
/root/projects/linebr-legacy/server/start.sh   # sobe login + game
/root/projects/linebr-legacy/server/stop.sh    # encerra
```

## Endereço para o cliente
- **VPS:** `177.7.48.204` — porta de login **2106**
- **Local:** `127.0.0.1` — porta de login 2106

## Backups e rollback
- Snapshot do estado pré-deploy: `_deploy-backup/state-before.txt`
- Backup do `sshd_config`: `/etc/ssh/sshd_config.bak-*`
- **Rollback total:** `stop.sh` + `rm -rf /root/projects/linebr-legacy/server` + `DROP DATABASE acis` + `ufw delete allow 2106/7777` + restaurar `sshd_config.bak`. FOX/Traefik nunca afetados.

## ⚠️ Pendências (não são gameplay — são operação)

| # | Item | Prioridade |
|:-:|------|:----------:|
| 1 | **Systemd services** (auto-start no boot, auto-restart) — hoje é `start.sh` manual, sobrevive à sessão mas **não** a reboot | 🟠 Alta |
| 2 | **Usuário Linux dedicado** (rodar o L2 como não-root) | 🟠 Alta |
| 3 | **Backup automatizado** do banco `acis` + geodata (cron) | 🟠 Alta |
| 4 | **Reconverter** `19_11.l2j` / `20_11.l2j` (2 bytes de lixo — cosmético) | 🟢 Baixa |
| 5 | Aplicar as 26 atualizações do apt | 🟡 Média |
| 6 | **Upgrade de RAM antes de produção pública** (1 vCPU + 3.8 GB é limite; hoje ok p/ homologação) | 🟠 Alta (produção) |
| 7 | **Validação com cliente L2 real** (login → mundo) — ver proposta FASE 5 | 🟠 Alta |

## Conformidade
- ✅ Deploy via GitHub (fluxo oficial: VPS puxa do repositório).
- ✅ Nada desenvolvido na VPS — só implantado o que já existia no repo.
- ✅ `source/` no repo e a Base Zero **inalterados** — nenhum gameplay tocado.
- ✅ FOX intocável preservado.
