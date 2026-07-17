# Catálogo de Fontes de Pesquisa — LineBR Legacy

> Classificação oficial de confiabilidade. Toda evidência citada deve apontar para uma categoria daqui.

---

## Ranking de confiabilidade

| # | Fonte | Nível máximo que sustenta | Natureza |
|:-:|-------|:-------------------------:|----------|
| 1 | **Cliente oficial Interlude** (arquivos, `.dat`, `.u`, comportamento observável) | ★★★★★ | **Oficial — primária** |
| 2 | **Binários/servidor L2OFF (PTS) Interlude** | ★★★★★ | **Oficial — primária** |
| 3 | **Patch notes / anúncios NCSoft** da época | ★★★★☆ | **Oficial — secundária** |
| 4 | **Captura de pacotes** (própria, contra referência oficial) | ★★★★☆ | **Empírica** |
| 5 | **Arquivos históricos** (manuais, guias oficiais, sites arquivados via Wayback) | ★★★☆☆ | Oficial-derivada |
| 6 | **Vídeos antigos** (gameplay 2007 verificável) | ★★☆☆☆ – ★★★☆☆ | Observacional |
| 7 | **Fóruns técnicos** (devs experientes, wikis de comunidade) | ★★☆☆☆ | Comunidade |
| 8 | **Relatos de jogadores** ("eu lembro que…") | ★☆☆☆☆ | Memória |
| — | **Código oficial da aCis** | ★★★★★ **sobre a aCis** · ☆ **sobre o retail** | Código (ver aviso) |
| — | **Outros emuladores** (L2J, Mobius, forks) | ☆ **sobre o retail** | ❌ não é fonte retail |

## Avisos por categoria

### 1–2 · Cliente oficial e binários L2OFF — o padrão-ouro
São os únicos artefatos que **contêm** o comportamento original. O cliente Interlude é acessível; binários/PTS de servidor L2OFF circulam em comunidades de preservação.
⚖️ **Cautela legal/ética:** são material proprietário da NCSoft. Usar **como referência de comportamento** (medir/observar) é diferente de redistribuir. O projeto **não redistribui** binários oficiais; documenta observações.

### 3 · Patch notes NCSoft
Excelentes para regras declaradas (rates, fórmulas anunciadas, mudanças de sistema). Limitação: descrevem a **intenção**, nem sempre o **comportamento real** (bugs do retail eram parte do retail).

### 4 · Captura de pacotes
A evidência empírica mais forte que **nós** podemos produzir. Requer um alvo de referência (servidor L2OFF/PTS ou gravação histórica). Uma captura contra **um emulador** prova apenas o emulador — não conta.

### 5 · Arquivos históricos
Wayback Machine, manuais e guias oficiais arquivados. Úteis; envelhecem mal quanto a detalhes numéricos.

### 6 · Vídeos antigos
Servem para comportamento **observável e grosseiro** (ex.: personagem anda com teclado? animação de arranque existe?). Não servem para números.
Cuidado: muitos vídeos "de 2007" são de servidores privados — **verificar a origem** antes de contar como evidência.

### 7 · Fóruns técnicos
Valor real como **pista** e para levantar hipóteses. **Nunca** como prova.
⚠️ **Lição da Sprint 004:** as principais fontes históricas **morreram** (o fórum do L2J não resolve mais). Fóruns são efêmeros — **sempre arquivar** (Wayback/cópia local) o que for citado.

### 8 · Relatos de jogadores
★☆☆☆☆ por definição. Servem para gerar hipótese, jamais para decidir.

### ⚠️ Código da aCis — o mal-entendido perigoso
Prova **★★★★★ o que a aCis faz**. Prova **nada** sobre o retail — mesmo quando o comentário do autor diz "retail like". Comentário de autor é **intenção**, não evidência do original.

### ❌ Outros emuladores
L2J/Mobius/forks são **interpretações** do retail, muitas vezes copiadas entre si (inclusive erros). Usá-los como prova cria **falso consenso**. Podem inspirar hipóteses; nunca provar.

## Regra de arquivamento (obrigatória)
Toda fonte citada num documento do projeto deve ser **arquivada no momento da citação**:
1. Preferir link do **Wayback Machine** ao link vivo;
2. Registrar **data de acesso**;
3. Se for imagem/vídeo/pacote, guardar o artefato (ou seu hash) em local próprio;
4. Se a fonte morrer depois, o registro sobrevive.

## Formato de citação
```
Fonte: [categoria #3 — patch note NCSoft] "Interlude Update Notes", 2007-xx-xx
Arquivo: https://web.archive.org/web/…  (acesso: 2026-07-15)
Sustenta: ★★★☆☆
```

## Estado atual das fontes (2026-07-15)
| Fonte | Situação |
|-------|----------|
| Cliente oficial Interlude | 🟡 disponível na comunidade — **ainda não usado como referência pelo projeto** |
| Servidor L2OFF/PTS Interlude | 🟡 existe na comunidade — **não obtido** |
| Patch notes NCSoft (2007) | 🟡 provavelmente recuperáveis via Wayback — **não pesquisados sistematicamente** |
| Captura de pacotes | 🔴 **inexistente** — requer alvo de referência |
| Fórum L2J (l2jserver.com) | 🔴 **morto** (domínio não resolve) |
| Código aCis 409 | 🟢 disponível e auditado (evidência sobre a aCis) |

> Ou seja: **o projeto ainda não possui nenhuma fonte retail de nível ★★★★+ instalada.** Sanar isso é pré-requisito para qualquer "retail fix" — ver [SYSTEM_INDEX.md](../baseline/SYSTEM_CATALOG.md) e o backlog de Movement.
