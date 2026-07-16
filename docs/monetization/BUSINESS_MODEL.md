# Modelo de Negócio — LineBR Legacy

> Como o servidor se sustenta sem vender poder. **Nada implementado.**

---

## 1. Fontes de receita (todas aprovadas na filosofia)

| Fonte | Tipo | Recorrência | Risco de P2W |
|-------|------|-------------|:------------:|
| **VIP Bronze / Silver / Gold** | assinatura de conveniência | 🟢 recorrente | ver §4 |
| **Serviços administrativos** | avulso | 🔴 esporádico | 🟢 nenhum |
| **Doação/apoio voluntário** | avulso/recorrente | 🟡 imprevisível | 🟢 nenhum |

> Nenhuma dessas fontes injeta itens ou Adena na economia ([regras E-7/E-8](MONETIZATION_PHILOSOPHY.md)).

## 2. Por que VIP é a espinha dorsal
É a **única fonte recorrente e previsível** do modelo. Doação não paga contas de forma confiável; serviços são esporádicos. Sem receita recorrente, o projeto depende do bolso do dono — o que é legítimo, mas precisa ser uma **decisão consciente**, não uma descoberta no terceiro mês.

## 3. Estrutura de custos (a estimar)

| Custo | Natureza | Observação |
|-------|----------|------------|
| VPS | recorrente | hoje o LineBR cabe numa VPS modesta |
| Domínio | anual | baixo |
| Backup / storage | recorrente | crítico ([P-13](../game-design/DESIGN_PRINCIPLES.md) — tempo do jogador é sagrado) |
| Proteção DDoS | recorrente | vira necessidade quando o servidor cresce |
| **Tempo do Owner** | 🔴 **o maior custo real** | desenvolvimento, suporte, moderação, serviços administrativos manuais |

> **O gargalo do LineBR Legacy não é dinheiro — é tempo.** Os serviços administrativos ([SERVICE_POLICY](SERVICE_POLICY.md)) são todos manuais; o VIP exige suporte; a moderação é diária. Receita não compra tempo do dono de volta.

## 4. Sustentabilidade × Integridade — a pressão estrutural

O modelo VIP resolve a recorrência, mas cria uma pressão permanente e previsível: **"o que mais podemos colocar no VIP para vender mais?"**

Historicamente, é assim que servidores caem — não por uma decisão, mas por uma sequência de pequenas ampliações razoáveis. Por isso:

| Mecanismo de defesa | Como funciona |
|---------------------|---------------|
| **Escopo congelado** | os benefícios de cada tier são fixados em [VIP_SYSTEM](VIP_SYSTEM.md); ampliar exige ADR + revisão |
| **Lista proibida imutável** | [FORBIDDEN_FEATURES](FORBIDDEN_FEATURES.md) só cresce, nunca encolhe |
| **Teste do competidor** | aplicado a toda proposta nova |
| **Transparência** | o que é vendido é público |

## 5. Recorrência sem P2W — como manter
1. **VIP com escopo fixo** — o valor está na conveniência e identidade, não em vantagem.
2. **Serviços administrativos** — receita marginal, zero risco.
3. **Doação com reconhecimento simbólico** — quem paga é quem quer que o projeto exista.
4. **Nunca**: ampliar VIP sob pressão financeira. É exatamente aí que a política é testada.

## 6. Cenários

| Cenário | Receita | Integridade | Nota |
|---------|:-------:|:-----------:|------|
| VIP + serviços + doação | 🟢 previsível | 🟡 sob pressão constante | requer disciplina de escopo |
| Só doação | 🔴 instável | 🟢 total | dono banca a diferença |
| VIP ampliado sob pressão | 🟢 alta | 🔴 zero | **é a morte do projeto** — proibido |

## 7. A pergunta que precede o modelo

> **O LineBR Legacy precisa se pagar, ou é um projeto que o Owner banca porque quer que ele exista?**

Ambas as respostas são legítimas — mas levam a servidores diferentes:
- **Se banca:** o VIP é um bônus; a pressão some; a integridade fica trivial de manter.
- **Se precisa se pagar:** o VIP é essencial; a pressão é permanente; a integridade exige disciplina ativa e uma política escrita a frio (que é justamente o que esta pasta é).

Registrado como decisão em aberto: [DECISION_LOG M-007](DECISION_LOG.md).

## 8. Pendências
| # | Pendência |
|---|-----------|
| B-1 | Estimar custo mensal real (VPS + backup + DDoS) |
| B-2 | Definir preços dos tiers VIP |
| B-3 | Definir duração/renovação do VIP |
| B-4 | Responder M-007 (banca × se paga) |
| B-5 | Definir política de transparência (o que será público) |
