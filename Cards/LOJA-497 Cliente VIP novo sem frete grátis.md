---
tipo: bug
card: https://jira.exemplo.com/browse/LOJA-497
sprint: 42
status: fechado
toca: [RN-002 Frete grátis, Cliente]
---
# 🐞 LOJA-497 Cliente que acabou de virar VIP não ganha frete grátis

**Card:** [LOJA-497](https://jira.exemplo.com/browse/LOJA-497)
**Toca em:** [[RN-002 Frete grátis]] · [[Cliente]]

## Sintoma
Cliente fez o 5º pedido de manhã, voltou à tarde para comprar de novo e pagou frete. Reclamou no SAC: "sou VIP e fui cobrado".

## Como reproduzir
1. Cliente com 4 pedidos pagos nos últimos 12 meses
2. Fazer e pagar o 5º pedido
3. No mesmo dia, montar carrinho de R$ 50 → frete é cobrado

## Causa raiz
**Não era bug de código, era entendimento da regra.** O tier VIP é recalculado pelo `RecalculateTiersJob` às 3h. O cliente só vira VIP na madrugada seguinte.

## Regra envolvida
[[RN-002 Frete grátis]] — a regra dizia "cliente VIP", mas não dizia *desde quando*.

## Correção
- Conversado com Ana: calcular em tempo real custaria caro (consulta pesada). **Comportamento aceito.**
- Ajuste só de texto: e-mail de "Parabéns, você é VIP!" agora sai junto com o job, não com o 5º pedido. Antes o e-mail criava a expectativa errada.

## Prevenção ✅
- [x] Nova linha na tabela da [[RN-002 Frete grátis]] (VIP recém-promovido)
- [x] Teste `ShippingCalculatorTest.vipRecemPromovidoSoValeAposJob`
- [x] Pegadinha já existia em [[Cliente]]; adicionei o link para este bug

> [!note] Lição
> Nem todo bug é bug. Às vezes o sistema está certo e a **regra estava incompleta** na cabeça de todo mundo. Registrar isso evita que o próximo dev "corrija" e quebre o desempenho.
