---
tipo: historia
card: https://jira.exemplo.com/browse/LOJA-482
sprint: 42
status: fechado
toca: [RN-002 Frete grátis, Pedido]
---
# LOJA-482 Frete grátis considerar valor antes do cupom

**Card:** [LOJA-482](https://jira.exemplo.com/browse/LOJA-482)
**Toca em:** [[RN-002 Frete grátis]] · [[Pedido]]

## Entendimento inicial
Clientes reclamam que ao aplicar cupom perdem o frete grátis. O negócio quer que o cupom não "puna" o cliente.

## O que descobri
- [[Ana Lima|Ana]] confirmou: vale o subtotal **antes** do cupom. O código estava errado desde o início.
- O cálculo roda em **dois lugares**: checkout (`ShippingCalculator`) e resumo do carrinho (`CartSummary`). Só corrigir um geraria valor diferente entre carrinho e checkout!
- O time chama de "subtotal bruto" (antes do cupom) e "subtotal líquido" (depois).

## Decisões
- Pedidos antigos não serão recalculados, só novos. (Ana, no Slack, 2026-09-22)
- Extraí a regra para `FreeShippingPolicy` para ter um só lugar.

## Dúvidas
- [x] ~~Cupom de frete grátis soma com essa regra?~~ → Não, cupom de frete é outro fluxo, ignora o limite.

## Colheita ✅
- [x] [[RN-002 Frete grátis]]: regra corrigida, tabela atualizada, saiu de #suposicao para #confirmado
- [x] [[Glossário]]: "Subtotal bruto" e "Subtotal líquido"
- [x] Não precisou de ADR (mudança pequena)
