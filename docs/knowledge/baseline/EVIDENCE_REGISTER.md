# Registro de Evidências — LineBR Legacy

> Banco central de evidências. Toda afirmação da Baseline aponta para um `EV-NNN` daqui.
> **Regra de imutabilidade:** evidências nunca são apagadas. Refutadas são marcadas `REFUTADA` com justificativa.

---

## ⚠️ Estado atual: o projeto possui **ZERO evidências retail**

| Categoria | Qtd |
|-----------|----:|
| Evidências **sobre a aCis** | 3 |
| Evidências **sobre o retail** (★★★★+) | **0** |
| Evidências **sobre o retail** (qualquer nível) | **0** |

**Consequência formal:** nenhum sistema pode ser marcado 🔵 *Retail validado*, e **nenhuma alteração de gameplay está autorizada** pela [CHANGE_ACCEPTANCE_POLICY](../methodology/CHANGE_ACCEPTANCE_POLICY.md). Sanar isso é o trabalho nº 1 do projeto — ver [ROADMAP_BASELINE.md](ROADMAP_BASELINE.md) Fase 00.

---

## Registro

### EV-001 — Source oficial aCis 409
| Campo | Valor |
|-------|-------|
| **ID** | EV-001 |
| **Fonte** | [gitlab.com/Tryskell/acis_public](https://gitlab.com/Tryskell/acis_public) |
| **Tipo** | Código-fonte oficial da aCis |
| **Data** | commit `55ff8a4e` — 2024-09-07 (coletado 2026-07-15) |
| **Hash** | `55ff8a4ec7e186d9816cd549246b4cf1f59c9f12` |
| **Nível** | ★★★★★ **sobre a aCis** · ☆ **sobre o retail** |
| **Sistemas** | todos |
| **Observações** | Prova o que a aCis **faz**. **Não é evidência retail** — nem quando o autor comenta "retail like" (isso é intenção, não prova). Ver [EVIDENCE_LEVELS](../methodology/EVIDENCE_LEVELS.md). |

### EV-002 — Runtime pack Base Zero (aCis 409 compilado)
| Campo | Valor |
|-------|-------|
| **ID** | EV-002 |
| **Fonte** | `LineBRLegacy.rar` (fornecido pelo dono) → `runtime-reference/` |
| **Tipo** | Binário compilado + datapack |
| **Data** | classes de 2024-09-11 (importado 2026-07-15) |
| **Hash** | commit `d7c8881` · tag `acis-409-runtime-base` |
| **Nível** | ★★★★★ **sobre a aCis** · ☆ **sobre o retail** |
| **Sistemas** | todos |
| **Observações** | Provado equivalente a EV-001: **2.881/2.881 classes byte-idênticas** ao build da source (só o `MANIFEST.MF` difere). Ver [BUILD_VALIDATION](../../engineering/BUILD_VALIDATION.md). |

### EV-003 — Auditoria de Movement (Sprint 004)
| Campo | Valor |
|-------|-------|
| **ID** | EV-003 |
| **Fonte** | Auditoria própria sobre EV-001 |
| **Tipo** | Análise derivada (documental) |
| **Data** | 2026-07-15 |
| **Hash** | commit `774d1bcb` |
| **Nível** | ★★★★★ **sobre a aCis** · ☆ **sobre o retail** |
| **Sistemas** | B03 Movement, B01 GeoData, B02 Pathfinding, B07 Boat, E01 AI |
| **Observações** | 14 divergências suspeitas levantadas ([MOVEMENT_L2OFF_DIFFERENCES](../audits/movement/MOVEMENT_L2OFF_DIFFERENCES.md)). **Nenhuma** atinge ★★★★ como afirmação sobre o retail. |

---

## Buscas realizadas SEM resultado (ausência é dado)

| # | Busca | Data | Resultado |
|:-:|-------|------|-----------|
| N-001 | Documentação técnica pública do L2OFF Interlude (movimento) | 2026-07-15 | ❌ Não existe spec pública |
| N-002 | Fórum L2J (`l2jserver.com/forum`) — thread "Sense of movement on retail vs l2j" | 2026-07-15 | ❌ **Domínio morto** (redireciona p/ fora) |
| N-003 | Changelog aCis 410/411 em detalhe (arquivo/método) | 2026-07-15 | ❌ Só temas; revisões 410/411 são de doador |

> **Lição registrada:** fontes de comunidade **morrem**. Por isso a [regra de arquivamento](../methodology/RESEARCH_SOURCES.md#regra-de-arquivamento-obrigatória) (Wayback + hash + data) é obrigatória **no momento da citação**.

---

## Evidências desejadas (lacunas prioritárias)
| Alvo | Sustentaria | Destrava |
|------|:-----------:|----------|
| **Geodata Interlude (formato L2OFF)** | ★★★★☆ | B01, B02, B03, B04, C01–C07, E01–E04 |
| **Cliente oficial Interlude** | ★★★★★ | quase tudo (comportamento observável) |
| **Servidor L2OFF/PTS Interlude** | ★★★★★ | quase tudo (referência medível) |
| **Patch notes NCSoft 2007 (Wayback)** | ★★★☆☆ | regras declaradas (rates, fórmulas) |
| **Capturas de pacotes contra referência** | ★★★★☆ | protocolo, movimento, combate |

## Como adicionar uma evidência
1. Coletar → 2. **Arquivar** (Wayback + hash + data de acesso) → 3. Registrar aqui com `EV-NNN` → 4. Classificar ★ e declarar *sobre aCis* ou *sobre retail* → 5. Vincular sistemas → 6. Atualizar [RETAIL_ASSUMPTIONS](RETAIL_ASSUMPTIONS.md) e [UNKNOWN_BEHAVIORS](UNKNOWN_BEHAVIORS.md) → 7. PR.

### Template
```
### EV-NNN — <título>
| ID | EV-NNN |
| Fonte | <link arquivado + original> |
| Tipo | <categoria de RESEARCH_SOURCES.md> |
| Data | <data do artefato> (coletado <data>) |
| Hash | <sha256 / commit / id do snapshot> |
| Nível | ★… sobre <aCis|retail> |
| Sistemas | <IDs do SYSTEM_CATALOG> |
| Observações | <limitações, cautelas> |
```
