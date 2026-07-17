# Changelog — LineBR Legacy Bible

> Histórico de todas as mudanças da Constituição. Formato: *Keep a Changelog*.
> **Regra:** toda alteração da Bíblia é registrada aqui, com data, autor da decisão e motivo.

---

## [1.0.0] — 2026-07-15 · Sprint 009 — Criação da Bíblia

### Adicionado — Identidade
- Missão, visão, objetivo, público-alvo e filosofia oficial (`SERVER_IDENTITY`)
- Máxima: *"Tudo deve ter importância. Nada deve ser descartável"*

### Adicionado — Progressão ⭐ (decisão nova do Owner)
- **Rates de XP aprovadas:** 1~30 = **3x** · 30~60 = **2x** · 60~75 = **1x** · 75~80 = **0.75x**
- **Rates de SP:** mesmo comportamento da XP
- ➡️ **Resolve** a pendência `D-001` (rates) do [game-design/DECISION_LOG](../game-design/DECISION_LOG.md)

### Adicionado — Economia
- Adena 1x · Drop 1x · Spoil 1x · Craft 100% · Quest Retail
- Regras E-1..E-8 (só Adena; servidor nunca cria itens nem Adena)
- Taxa do Marketplace: **aprovada para implementação futura** (valores pendentes)
- Marketplace **em Giran**

### Adicionado — Gameplay
- Learning Skills **manual** · Skills com **SP** · **Guild Masters obrigatórios** · **Teleport Retail**
- **NPC Buffer gratuito existe** (level limite: 🔴 pendente)

### Adicionado — Quests e Mundo
- Todas as quests importantes; profissão e acesso **obrigatórias**; nada pulado, nada simplificado
- Mundo vivo: Giran centro econômico; Catacombs, Necropolis, Raid/Grand Boss, Siege, Olympiad, Seven Signs — **nada descartado**

### Adicionado — Social
- Clãs, alianças, castle, clan hall, Hero, Olympiad, PvP, PK — importantes
- **Comunidade acima de conveniência**

### Adicionado — Customs ⭐ (decisão nova do Owner)
- **5 customs aprovadas:** VIP · Marketplace · Offline Shop · **Hero Dynasty Skin** · Auto Loot
- **Todas as demais: PROIBIDAS**
- **Hero Dynasty Skin** (nova): só aparência; sem atributos/status/defesa/ataque/bônus; não vende, não dropa, não troca, não vai para Warehouse/Freight/Clan Warehouse; **desaparece quando acaba o Hero**

### Adicionado — Serviços
- Consolidação integral da Sprint 008 (VIP Bronze/Silver/Gold, Auto Loot Gold, Marketplace, serviços administrativos) — **sem alteração**

### Adicionado — Regras
- Bot · Walker · Exploit · Dupes · RMT · Compra de Adena · Venda de Adena — **proibidos**

### Adicionado — Governança
- `OWNER_DECISIONS` (101 decisões aprovadas, somente fatos)
- `OPEN_DECISIONS` (16 pendências)

### Fatos técnicos registrados (EV-001 — aCis 409, commit `55ff8a4e`)
- `AutoLearnSkills = False` é **nativo** → "Learning manual" **não exige custom** ✅
- Rates nativas = **x1** → rates escalonadas por faixa **exigem custom** ⚠️
- Economia 1x **coincide** com o nativo → **zero custom** ✅
- `AutoLoot` é config **global** (`False`) + `AutoLootRaid` separado → VIP-exclusivo **exige custom** ⚠️
- **Marketplace e Offline Shop: 0 arquivos** → customs completos ⚠️
- **Dynasty: 0 arquivos** no datapack Interlude → skin **provavelmente exige patch de cliente** ⚠️ (OD-09)
- Buffer **nativo** (`SchemeBuffer`, `BufferManager`) → habilitar **não exige custom** ✅
- Inventory/Warehouse são **mecânica de classe** (`Dwarf` +20 slots) ⚠️ (OD-10)

### Superado
- `game-design/DECISION_LOG D-001` (rates) → **resolvido** por O-10/O-11
- `game-design/DECISION_LOG D-006` ("sem buffer NPC gratuito") → **superado** por O-34
- `game-design/MONETIZATION_PHILOSOPHY` → superado por [`monetization/`](../monetization/)

---

## Formato para próximas entradas
```
## [X.Y.Z] — AAAA-MM-DD · Sprint NNN — <título>
### Adicionado / Alterado / Superado / Removido
- <mudança> (decisão: Owner, <data>) — <motivo>
```
