# ADR-004 — Estratégia de Versionamento

- **Status:** Aceito
- **Data:** 2026-07-15
- **Decisores:** Thainan Lima

## Contexto

O LineBR Legacy evolui em duas frentes distintas: (1) acompanhar as **revisões oficiais da aCis** (409 → 410 → 411 …) e (2) aplicar **patches próprios do LineBR** (customizações e ajustes). Misturar essas frentes sem uma estratégia clara tornaria impossível saber "o que é aCis" e "o que é LineBR", e impediria atualizações futuras do upstream.

## Decisão

Adota-se uma **linha de versionamento em camadas**, sempre linear e rastreável:

```
aCis 409  (Base Zero — tag: acis-409-runtime-base)
   │
   ▼
aCis 410  (revisão oficial aplicada — tag: acis-410)
   │
   ▼
aCis 411  (revisão oficial aplicada — tag: acis-411)
   │
   ▼
LineBR Patch 001  (primeira customização LineBR — tag: linebr-p001)
   │
   ▼
LineBR Patch 002  (tag: linebr-p002)
   │
   ▼
   ...
```

### Regras
1. **Camada aCis (upstream):** cada revisão oficial é aplicada em sua própria branch (`development/rev-410`, `development/rev-411`), revisada, e ao ser aceita recebe uma **tag anotada** (`acis-410`, `acis-411`).
2. **Camada LineBR (downstream):** as customizações começam **somente após** a base oficial estar consolidada (411). Cada patch LineBR é numerado sequencialmente (`LineBR Patch NNN`) em branch `feature/*`, e taggeado (`linebr-pNNN`).
3. **Tags são imutáveis.** A tag `acis-409-runtime-base` nunca é movida (ver [ADR-001](ADR-001-base-oficial.md)). Idem para todas as tags de revisão/patch.
4. **Ordem é sagrada:** nunca aplicar um patch LineBR antes de concluir a camada oficial pretendida — assim é sempre possível rebasear/atualizar o upstream.

### Documentação obrigatória por etapa
Cada revisão/patch gera:
- um **registro no `docs/ROADMAP.md`** (marcando a fase concluída);
- um **`CHANGELOG`** específico (o que a revisão/patch mudou, com referência ao diff oficial quando aplicável);
- quando houver decisão arquitetural, um **novo ADR**;
- uma **tag anotada** com mensagem descritiva.

## Consequências

**Positivas**
- Separação total entre base oficial e customizações → upstream atualizável.
- Histórico conta a evolução de forma auditável (tags + changelogs + ADRs).
- Reversibilidade: qualquer camada pode ser inspecionada ou reproduzida por sua tag.

**Negativas / custos**
- Exige disciplina de tagging e changelog a cada etapa.
- Aplicar revisões oficiais exige obter os **diffs oficiais** da aCis (410, 411) e recompilar.

## Alternativas consideradas

- **Aplicar tudo (revisões + customs) numa única linha sem tags** — rejeitada: impossível separar aCis de LineBR e atualizar upstream.
- **Fork total, ignorando futuras revisões oficiais** — rejeitada: perderia correções e melhorias da aCis.
