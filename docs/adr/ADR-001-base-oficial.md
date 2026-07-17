# ADR-001 — Base Oficial do Projeto

- **Status:** Aceito
- **Data:** 2026-07-15
- **Decisores:** Thainan Lima (dono do projeto)

## Contexto

O LineBR Legacy precisa de uma fundação de código única, confiável e sustentável. Havia três candidatos a "base":

1. O **runtime pack compilado** (`LineBRLegacy.rar`) — pronto para rodar, porém **sem código-fonte** (só `l2jserver.jar`), impossibilitando aplicar revisões e evoluir o core.
2. A **source customizada** preservada do antigo LineBR (`linebr-audit`) — uma aCis mais antiga já misturada com customizações (VIP, Skins, Coins), sem separação clara entre base e custom.
3. A **source oficial pública da aCis** — [gitlab.com/Tryskell/acis_public](https://gitlab.com/Tryskell/acis_public), commit `55ff8a4e` ("aCis 409").

A auditoria comparativa (registrada no histórico do projeto) provou que o runtime pack é a **forma compilada exata** da source oficial aCis 409 limpa:

- datapack **15.718/15.718** arquivos idênticos (path + tamanho);
- SQL **65/65** byte-idênticos;
- configs default idênticas;
- mesma biblioteca (`mariadb-java-client-3.1.4`);
- `MANIFEST.MF` do jar registra build com **Apache Ant 1.10.14 + JDK 21.0.4**, com classes datadas 4 dias após o commit 409;
- **zero** classes customizadas (`Linebr*`) na source → aCis 100% limpa.

## Decisão

A **source oficial `Tryskell/acis_public @ aCis 409`** é adotada como a **fundação permanente** do LineBR Legacy, importada para `source/` **sem qualquer modificação**.

O **runtime pack original** é preservado em `runtime-reference/` e na tag imutável **`acis-409-runtime-base`**, servindo **apenas como referência histórica e prova de equivalência** — nunca como base de desenvolvimento.

## Justificativa

- **É código-fonte real**: permite compilar, aplicar as revisões oficiais 410/411 e evoluir com controle total.
- **É limpa**: partir de uma base sem customs garante rastreabilidade — cada custom futura será um commit isolado e reversível.
- **É oficial e autêntica**: mantida pelo próprio autor da aCis, com histórico versionado (revisões 310→409).
- **É comprovadamente a origem do nosso runtime**: adotá-la não descarta nada — o runtime continua reproduzível e verificável.

## Consequências

**Positivas**
- Fundação versionada, compilável e evolutiva.
- Separação limpa entre *base oficial* e *futuras customizações*.
- Capacidade de provar, a qualquer momento, que um build reproduz o runtime original.

**Negativas / custos**
- Exige ambiente de build (**JDK 21 + Apache Ant**) — ver [Build.md](../engineering/BUILD.md).
- As customizações do antigo LineBR **não** vêm de graça: precisarão ser reimplementadas/portadas deliberadamente sobre a base (fase futura).

## Alternativas consideradas

- **Usar o runtime compilado como base** — rejeitada: sem source, é um beco sem saída para desenvolvimento.
- **Usar a source customizada antiga** — rejeitada como *base*: mistura base + custom, dificulta aplicar revisões oficiais e auditar. Poderá ser **consultada** como referência das customizações a reintroduzir.
