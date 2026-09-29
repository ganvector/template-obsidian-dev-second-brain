---
tags: [entidade]
aliases: [Customer]
---
# 🧱 Cliente

**Em uma frase:** quem compra. Pode ser comum ou VIP (ver [[Glossário]]).
**Código:** `customers/domain/Customer.java`

## Pegadinhas
- O tier VIP é recalculado por um job noturno (`RecalculateTiersJob`, 3h da manhã). Um cliente pode virar VIP e só ganhar o benefício no dia seguinte. #confirmado
  - Já gerou reclamação: 🐞 [[LOJA-497 Cliente VIP novo sem frete grátis]]
