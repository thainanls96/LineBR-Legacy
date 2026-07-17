# Base Zero — LineBR Legacy

## O que é a Base Zero

A **Base Zero** é o ponto de partida imutável do projeto: o **runtime pack original da aCis 409**, importado exatamente como foi obtido, sem nenhuma modificação de código, datapack, SQL ou configuração.

Ela está eternizada por:

- **Commit:** `d7c8881` — `chore(acis): import original aCis 409 source`
- **Tag permanente:** `acis-409-runtime-base` — *"Base Zero - aCis 409 runtime pack preserved"*
- **Branch:** `main`

> ⚠️ A tag `acis-409-runtime-base` **nunca deve ser movida, recriada ou apagada**. Ela é a prova de integridade do runtime original. Para voltar a ele a qualquer momento:
> ```
> git checkout acis-409-runtime-base
> ```

## Origem dos artefatos

| Artefato | Origem | Observação |
|----------|--------|------------|
| **Runtime pack** | `LineBRLegacy.rar` (fornecido pelo dono) | 15.819 arquivos versionados; datapack + `l2jserver.jar` compilado |
| **Source oficial** | [gitlab.com/Tryskell/acis_public](https://gitlab.com/Tryskell/acis_public) `@ 55ff8a4e` | commit "aCis 409" (2024-09-07) |

## Prova: o runtime foi gerado da source oficial 409

A auditoria comparativa confirmou correspondência com altíssima confiança:

| Verificação | Resultado |
|-------------|-----------|
| Revisão | Ambos = **aCis 409** |
| Datapack (html + xml) | **15.718 / 15.718 idênticos** (path + tamanho) |
| SQL | **65 / 65 byte-idênticos** (md5) |
| Configs default (`server`/`players.properties`) | diff vazio |
| Biblioteca | `mariadb-java-client-3.1.4.jar` (idêntica) |
| `MANIFEST.MF` do `l2jserver.jar` | `Ant 1.10.14` + `JDK 21.0.4 (Oracle)`; classes de 2024-09-11 (4 dias após o commit 409) |
| Customizações no source | **zero** classes `Linebr*` → aCis 100% limpa |

**Conclusão:** o `runtime-reference/` é a forma **compilada** da source oficial `aCis 409` limpa. As duas árvores são complementares — uma é o código-fonte, a outra o binário pronto para rodar da mesma revisão.

## O que a Base Zero NÃO contém

- Nenhuma customização do antigo LineBR (VIP/Skins/Coins) — essas estão em uma base **diferente** (a source customizada preservada em `linebr-audit`, de uma aCis mais antiga).
- Nenhuma alteração de gameplay, rates ou features.

## Regras de ouro

1. Não perder a Base Zero nem a tag `acis-409-runtime-base`.
2. Não alterar `runtime-reference/` — é referência histórica byte-a-byte.
3. Todo desenvolvimento acontece sobre `source/`, em branches próprias, nunca na `main`.
