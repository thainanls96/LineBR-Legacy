# Auditoria da VPS — LineBR Legacy

> **Sprint 014 (FASE 4 do projeto) — auditoria read-only.** Nenhuma alteração feita na VPS.
> VPS: **177.7.48.204** (`srv1630430`) · acesso `ssh vps` (chave ed25519) · auditado 2026-07-17.

---

## Veredito: 🟡 **A VPS AINDA NÃO está pronta — mas está perto.**

Falta pouco (instalar MariaDB, abrir portas, deploy da Base Zero), **mas há dois pontos de atenção sérios**: RAM/CPU apertados e segurança do SSH. Detalhes abaixo.

---

## 1. Inventário

| Recurso | Estado | Avaliação |
|---------|--------|:---------:|
| **SO** | Ubuntu 24.04.4 LTS | ✅ |
| **Kernel** | 6.8.0-134-generic x86_64 | ✅ |
| **Atualizações** | 26 pacotes atualizáveis, **0 de segurança** | 🟡 aplicar |
| **CPU** | AMD EPYC 9354P — **1 vCPU** | 🟠 limitado |
| **RAM** | **3.8 GB** total · **3.35 GB disponível** | 🟠 apertado |
| **Swap** | 4 GB (42 MB usados) | ✅ |
| **Disco** | 48 GB · 11 GB usados · **38 GB livres (22%)** | ✅ |
| **Java** | **OpenJDK 21.0.11** | ✅ (atende JDK 21) |
| **Apache Ant** | `/usr/bin/ant` | ✅ |
| **Git** | 2.43.0 | ✅ |
| **Docker** | 29.4.0 | ✅ |
| **Traefik** | `traefik-traefik-1` Up 6 dias (80/443) | ✅ intacto |
| **MariaDB** | ❌ **NÃO instalado** (sem pacote, sem datadir) | 🔴 **falta** |
| **LoginServer / GameServer** | ❌ não implantados | 🔴 falta (é o objetivo) |
| **SSL** | Traefik + Let's Encrypt (`acme.json`) | ✅ |
| **Firewall (UFW)** | **ativo** — libera 22, 80, 443 | ✅ (falta abrir 2106/7777) |
| **Cron** | nenhum | ✅ limpo |
| **FOX** | `/root/projects/fox` (3.6 MB) intacto, sem container | ✅ **não tocar** |

## 2. Segurança 🟠

| Item | Estado | Risco |
|------|--------|-------|
| **`PermitRootLogin`** | **yes** | 🟠 root acessível remotamente |
| **`PasswordAuthentication`** | **yes** | 🔴 **login root por SENHA habilitado** — alvo de brute-force |
| Chave SSH | ed25519 em uso (autenticação por chave funciona) | ✅ |
| UFW | ativo | ✅ |

> ⚠️ **Antes de expor portas de jogo à internet, recomendo endurecer o SSH** (`PasswordAuthentication no`, idealmente `PermitRootLogin prohibit-password`). Um servidor de jogo atrai scanners; root+senha é a porta mais fácil.

## 3. Portas em uso
| Porta | Serviço |
|-------|---------|
| 80, 443 | Traefik |
| 22 | SSH |
| 53 (localhost) | systemd-resolved |
| **2106 / 7777 / 9014** | ❌ **nenhum L2 ainda** |

## 4. Estrutura de diretórios (`/root/projects/`)
```
fox/           🦊 intocável (3.6 MB)
linebr-legacy/ 🆕 vazio — destino do deploy (0 arquivos)
habitar/ · backups/ · logs/ · shared/
```
- `/root/archive/linebr-final-20260714-033954.tar.gz` (1.34 GB) — arquivo do LineBR antigo, preservado.
- `/root/backups/` (7.5 MB) — snapshots phoenix_jarvis / recovery (legado, não-CAPTA).

## 5. ⚠️ O ponto crítico: RAM e CPU vs. geodata

A [Sprint 013](../knowledge/audits/geodata/GEODATA_INSTALL_VALIDATION.md) mediu: com geodata, o GameServer usa **~1.36 GB de heap / ~1.7 GB de working set**.

Conta na VPS (3.35 GB disponível):
```
GameServer (heap 2G + geodata)   ~1.7 GB working set
LoginServer                       ~0.07 GB
MariaDB                           ~0.2–0.5 GB
Sistema + Traefik + Docker        ~0.6 GB
                                  ─────────
                          Total  ~2.6–2.9 GB  →  cabe, mas com pouca folga
```
**Veredito:** cabe para **homologação/baixa população**, com `-Xmx` ajustado (ex.: `-Xmx1500m`–`1800m`, como o Readme da geodata sugere). Para **produção com jogadores**, **1 vCPU + 3.8 GB é o gargalo** — aCis é multi-thread e a geodata pesa. Recomendo planejar upgrade de RAM antes de abrir ao público.

## 6. "A VPS está pronta para receber o LineBR Legacy?"

**Para HOMOLOGAÇÃO: quase — falta instalar/configurar (itens abaixo).**
**Para PRODUÇÃO pública: não sem upgrade de RAM.**

### O que falta (para o deploy da Base Zero)
| # | Item | Tipo |
|:-:|------|------|
| 1 | **Instalar MariaDB** + criar DB `acis` + usuário app não-root | 🔴 obrigatório |
| 2 | **Deploy da Base Zero** (build ou runtime) em `/root/projects/linebr-legacy/` | 🔴 obrigatório |
| 3 | **Copiar geodata L2J** (139 arquivos) + config `GeoDataType=L2J` | 🔴 obrigatório |
| 4 | **Abrir portas 2106 e 7777** no UFW (9014 fica **localhost**) | 🔴 obrigatório |
| 5 | **Ajustar `-Xmx`** do GameServer para a RAM da VPS | 🟠 recomendado |
| 6 | **Endurecer SSH** (senha off) antes de expor à internet | 🟠 recomendado |
| 7 | Aplicar as 26 atualizações do apt | 🟡 higiene |
| 8 | Usuário Linux dedicado (não rodar o L2 como root) | 🟡 boas práticas |

> Nada disso foi executado — aguarda aprovação (ver plano da FASE 3).
