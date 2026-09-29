---
tags: [regra, confirmado]
entidades: [Pedido, Cliente]
fonte: Ana (PO), via LOJA-482
---
# 📏 RN-002 Frete grátis

## A regra
Frete grátis se o **subtotal bruto** (antes do cupom) ≥ R$ 199, **ou** se o [[Cliente]] é VIP (qualquer valor).

## Exemplos
| Cliente | Subtotal | Frete grátis? |
|---|---|---|
| Comum | R$ 150 | ❌ |
| Comum | R$ 199,00 | ✅ (é ≥, não >) |
| VIP | R$ 30 | ✅ |
| Comum com cupom que baixa de R$ 210 para R$ 180 | R$ 210 bruto | ✅ vale o bruto |
| Cliente que fez o 5º pedido **hoje** | R$ 50 | ❌ só vira VIP após o job da madrugada (aceito) |

## Onde está no código
- `FreeShippingPolicy` (antes ficava duplicado em `ShippingCalculator` e `CartSummary`)

## Dúvidas
- [x] ~~Antes ou depois do cupom?~~ → **antes**; o código estava errado. Ver [[LOJA-482 Frete grátis antes do cupom]]

## Histórico
- Sprint 42 — passou a usar subtotal bruto (antes do cupom) → [[LOJA-482 Frete grátis antes do cupom]]
- Sprint 42 — esclarecido que VIP só vale após o job noturno → 🐞 [[LOJA-497 Cliente VIP novo sem frete grátis]]
