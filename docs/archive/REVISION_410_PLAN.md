> 📦 **DOCUMENTO ARQUIVADO — NÃO VIGENTE.**
> Obsoleto: a estratégia de perseguir a revisão 410 foi abandonada na Sprint 004 (o projeto passou a mirar o L2OFF retail).
> Preservado para rastreabilidade. Ver [archive/README.md](README.md) e [CHANGELOG](../CHANGELOG.md).

---

# Plano da Revisão 410 — LineBR Legacy

> **Status:** PLANEJAMENTO. Nenhuma linha de código foi/será alterada nesta fase.
> **Escopo:** aplicar a revisão oficial da aCis **409 → 410**, mantendo Retail First (ver [ADR-003](../adr/ADR-003-retail-first.md)) e a estratégia de versionamento (ver [ADR-004](../adr/ADR-004-estrategia-versionamento.md)).

---

## ⚠️ BLOQUEIO CRÍTICO — o changeset da 410 ainda não está disponível

O repositório oficial público (`Tryskell/acis_public`) está na revisão **409** (é a versão pública/gratuita). O log de commits encerra em `aCis 409` (`55ff8a4e`). As revisões **410 e 411 são liberadas apenas a doadores/assinantes** da aCis e **não estão no repositório público**.

**Consequência:** a auditoria por-arquivo/classe/método (ETAPA 3, perguntas 1–3) e a contagem exata por categoria (ETAPA 4) **não podem ser produzidas sem o diff oficial 409→410**. Fabricar nomes de arquivos/classes seria irresponsável e contra o princípio de rastreabilidade.

**Ação necessária do dono (pré-requisito para implementar):** obter o **changeset oficial 409→410** de uma destas formas:
1. Conta de doador no fórum oficial aCis ([acis.i-live.eu](https://acis.i-live.eu)) → baixar a revisão 410 ou o diff 409→410; **ou**
2. Fornecer o pacote/patch da 410 que você já possua.

Assim que o diff 410 estiver disponível localmente, a auditoria detalhada (abaixo, seção "Auditoria por correção") será preenchida arquivo a arquivo antes de qualquer implementação.

---

## 1. O que se sabe da revisão 410 (changelog oficial)

Do changelog público da aCis, a revisão **410** concentra-se em (temas):
- **Makers** (sistema de produção/manor/makers).
- **NpcAi / Desires** (comportamento de IA de NPCs, "desires").
- **Cursed Weapon** (rework do sistema de armas amaldiçoadas).
- **Admincommands** (comandos de GM).
- **Movement** (movimentação).
- **Bugfixes** — inclui correção de *ghost corpses* (corpos fantasma), *task managers* para agendamento de spawn (MultiSpawn) e tarefas de respawn/despawn de NPCs.
- **Organization** (refatorações organizacionais, sem mudança funcional).

> Estes são **temas**, não a lista de arquivos. A tradução para arquivos/classes exige o diff (ver bloqueio acima).

## 2. Classificação por categoria (ETAPA 4) — framework

Contagens marcadas **TBD** só serão preenchidas com o diff 410. Risco/dificuldade/prioridade abaixo são estimativas **qualitativas** baseadas na natureza de cada área na arquitetura aCis.

| Cat | Área | Arquivos | Classes | Risco | Dificuldade | Prioridade | Notas |
|-----|------|----------|---------|-------|-------------|-----------|-------|
| A | **Core / Organization** | TBD | TBD | Médio | Baixa | 1ª | Refatorações organizacionais; base para as demais |
| B | **Network** | TBD | TBD | Alto | Média | — | Mexer em pacotes afeta o cliente; validar handshake |
| C | **Movement** | TBD | TBD | Alto | Alta | — | Movimentação toca geoengine/validação de posição |
| D | **NPC / NpcAi / Desires** | TBD | TBD | Médio-Alto | Alta | — | IA e desires; risco de regressão de comportamento |
| E | **Makers / Manor** | TBD | TBD | Médio | Média | — | Produção/manor; impacto econômico controlado |
| F | **Cursed Weapon** | TBD | TBD | Médio | Média | — | Rework isolado do sistema de arma amaldiçoada |
| G | **Task Managers / Spawn** | TBD | TBD | Médio | Média | — | MultiSpawn, respawn/despawn; corrige ghost corpses |
| H | **Admincommands** | TBD | TBD | Baixo | Baixa | — | Comandos de GM; baixo impacto em gameplay do jogador |
| I | **Misc / Bugfixes** | TBD | TBD | Baixo-Médio | Baixa | Última | Correções pontuais diversas |

> As categorias do exemplo do dono (Pet, PartyMatch, Quest, Drop, Craft, Clan, Castle, Olympiad) serão mapeadas conforme o diff real as tocar; a 410 pode não afetar todas.

## 3. Estratégia de implementação (ETAPA 5) — segura e incremental

Regra de ouro: **uma categoria por vez**, com validação completa entre cada uma. Nenhuma categoria implementada junto de outra.

```
Para CADA categoria (ordem por risco crescente):
  410-<Cat>  → aplicar SÓ os arquivos daquela categoria (do diff oficial)
       ↓ Build (JDK 21 + Ant) — deve compilar 0 erros
       ↓ Runtime Validation (subir login+game, 0 erros, comparar com runtime-reference)
       ↓ Commit atômico  feat(410-<Cat>): ...
       ↓ Documentação (changelog da categoria + atualizar este plano)
  → próxima categoria
Ao concluir todas: tag anotada  acis-410
```

**Ordem sugerida (menor risco/dependência primeiro):**
`A (Core/Org)` → `H (Admincommands)` → `I (Misc bugfixes)` → `G (Task/Spawn)` → `F (Cursed Weapon)` → `E (Makers)` → `D (NpcAi/Desires)` → `C (Movement)` → `B (Network)`.
Justificativa: começa pelo alicerce (Core) e pelos itens de baixo risco/baixa dependência, terminando nas áreas de maior risco (Movement, Network) que se beneficiam de já ter todo o resto validado.

## 4. Auditoria por correção (ETAPA 3) — a preencher com o diff 410

Para **cada** arquivo alterado pela 410 (assim que o diff existir), responder:
1. Arquivo alterado — *TBD*
2. Classe alterada — *TBD*
3. Método alterado — *TBD*
4. Comportamento na 409 — *TBD*
5. Problema que a 410 resolve — *TBD (mapear ao changelog)*
6. Risco de regressão — *TBD*
7. Dependência com outra correção — *TBD*
8. Impacto em gameplay — *TBD*
9. Aproxima do L2OFF/Interlude? — *esperado SIM (correções oficiais são Retail First)*
10. Obrigatória ou opcional — *esperado obrigatória (correção oficial), salvo exceções documentadas*

## 5. Estratégia de rollback (ETAPA 6)

- **Commits atômicos por categoria** → `git revert <commit>` desfaz uma categoria sem afetar as outras.
- **Tags por marco** (`acis-410` só ao final; e opcionalmente `acis-410-<Cat>` por categoria) → retorno a qualquer ponto.
- **Base Zero intacta** (`acis-409-runtime-base`) → possível voltar 100% à fundação.
- **Comparação com `runtime-reference/`** a cada build → detecta divergência não intencional.
- **Branch isolada** (`development/rev-410`) → a `main` nunca é tocada até PR aprovado.
- **Validação obrigatória** (build + runtime) antes de cada commit → nenhuma categoria entra quebrada.

## 6. Pré-condições para iniciar a implementação
1. Merge da fundação (`development/source-migration → main`) aprovado. ✅ PR aberto (#1).
2. Branch `development/rev-410` criada a partir da `main` mergeada.
3. **Diff/changeset oficial 409→410 disponível localmente.** ⛔ pendente (ver bloqueio).
4. Ambiente de build+runtime pronto (JDK 21 + Ant + MariaDB) — ✅ já validado nas Sprints 001/002.
