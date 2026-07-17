# Sistemas Custom — LineBR Legacy

> ✅ **Somente estas 5 customs são aprovadas. Todas as demais são PROIBIDAS.**

---

## Customs APROVADAS

| # | Custom | Natureza | Existe na aCis 409? (EV-001) |
|:-:|--------|----------|------------------------------|
| C-1 | **VIP** (Bronze/Silver/Gold) | conveniência + identidade | ❌ não existe → custom completo |
| C-2 | **Marketplace** | conveniência de comércio | ❌ 0 arquivos → custom completo |
| C-3 | **Offline Shop** | conveniência | ❌ 0 arquivos → custom completo |
| C-4 | **Hero Dynasty Skin** | cosmética | ❌ Dynasty **não existe** no datapack Interlude |
| C-5 | **Auto Loot** (VIP Gold) | conveniência de farm | ⚠️ existe como config **global** (`AutoLoot = False`) → **VIP-exclusivo exige custom** |
| C-6 | **Rates escalonadas por faixa de level** | progressão | ⚠️ aCis tem rate **global** → **exige custom** ([PROGRESSION](PROGRESSION.md)) |

> ⚠️ Todas exigem **ADR** de enquadramento pelo [ADR-003](../ADR/ADR-003-retail-first.md) (Retail First), pois divergem do Interlude.

---

## C-4 · Hero Dynasty Skin — especificação oficial

✅ **Custom cosmética aprovada pelo Owner.**

| Regra | Valor |
|-------|-------|
| Quem recebe | **Hero** (exclusivo) |
| Natureza | **Apenas aparência** |
| Atributos | ❌ **nenhum** |
| Status | ❌ nenhum |
| Defesa | ❌ nenhuma |
| Ataque | ❌ nenhum |
| Bônus | ❌ nenhum |
| Vender | ❌ **não pode** |
| Dropar | ❌ **não pode** |
| Trocar | ❌ **não pode** |
| Warehouse | ❌ **não pode** |
| Freight | ❌ **não pode** |
| Clan Warehouse | ❌ **não pode** |
| Ao perder o Hero | **A Skin desaparece automaticamente** |

**Propósito de design:** tornar o Hero **visível** — reforça [P-07](../game-design/DESIGN_PRINCIPLES.md) (*todo Hero deve ser admirado*) sem conferir nenhum poder.

### 📌 FATOS técnicos verificados (EV-001) — a considerar antes de implementar

| Verificação | Resultado |
|-------------|-----------|
| "dynasty" no datapack (xml) | **0 arquivos** |
| "dynasty" no código (java) | **0 arquivos** |
| "dynasty" no html | **0 arquivos** |
| Armaduras de topo presentes no Interlude | `draconic`, `imperial crusader`, `major arcana` (S-grade) |

⚠️ **Implicação crítica:** o set **Dynasty é posterior ao Interlude** (chronicle seguinte). Ele **não existe** no datapack, e — mais importante — **muito provavelmente não existe no cliente Interlude do jogador** (modelos 3D/texturas). Um item só é exibível se o **cliente** possuir a malha.

**Consequência provável:** a Hero Dynasty Skin exigiria **patch de cliente** distribuído a todos os jogadores (o cliente Interlude padrão não renderizaria a skin — apareceria inválida/invisível).

🔴 **PENDENTE DE DECISÃO DO OWNER:** aceitar patch de cliente obrigatório, **ou** escolher uma skin cosmética que já exista no cliente Interlude (ex.: um set S-grade existente). → [OPEN_DECISIONS](OPEN_DECISIONS.md)

> Registro, não objeção: a decisão cosmética está aprovada; o que precisa de decisão é **como viabilizá-la tecnicamente**.

---

## Customs PROIBIDAS

**Todas as demais.** Incluindo (lista não exaustiva):

❌ Auto Farm · ❌ Buffer completo/permanente sem regra · ❌ Teleport VIP · ❌ Farm VIP · ❌ Área VIP · ❌ Drop VIP · ❌ Loja de itens do servidor · ❌ Moeda premium · ❌ Itens exclusivos com stats · ❌ Asas · ❌ Aura · ❌ Cubos · ❌ Transformações · ❌ Mounts exclusivos · ❌ Pets exclusivos · ❌ Skills custom · ❌ Enchant custom · ❌ Grades além do Interlude · ❌ Eventos que criem itens/Adena

Lista completa e permanente: [monetization/FORBIDDEN_FEATURES.md](../monetization/FORBIDDEN_FEATURES.md).

## Regra de admissão de novas customs
```
1. Está nesta lista de aprovadas?  NÃO → PROIBIDA.
2. Owner aprova explicitamente?    NÃO → PROIBIDA.
3. Passa no teste do competidor?   NÃO → PROIBIDA (P2W).
4. Tem ADR de enquadramento?       NÃO → não implementa.
5. Fere P-01..P-15?                SIM → PROIBIDA.
```
