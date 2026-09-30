---
tags: [entidade]
aliases: [Order, Venda]
---
# 🧱 Pedido

**Em uma frase:** a intenção de compra do cliente, do checkout até a entrega.
**Código:** `orders/domain/Order.java` · tabela `orders`
**Dono no negócio:** [[Ana Lima|Ana (PO)]]

## Ciclo de vida
```mermaid
stateDiagram-v2
    [*] --> CRIADO: cliente finaliza checkout
    CRIADO --> AGUARDANDO_PAGAMENTO: pré-autorização enviada
    AGUARDANDO_PAGAMENTO --> PAGO: pagamento aprovado
    AGUARDANDO_PAGAMENTO --> CANCELADO: recusado / timeout 30min
    PAGO --> EM_SEPARACAO: CD recebe
    EM_SEPARACAO --> DESPACHADO: captura + nota fiscal
    DESPACHADO --> ENTREGUE: transportadora confirma
    PAGO --> CANCELADO: cliente cancela (RN-001)
    EM_SEPARACAO --> CANCELADO: cliente cancela (RN-001)
    ENTREGUE --> [*]
    CANCELADO --> [*]
```

## Regras que afetam
- [[RN-001 Cancelamento de pedido]]
- [[RN-002 Frete grátis]]

## Relações
- Pertence a um [[Cliente]]
- Tem um [[Pagamento]] (1:1 hoje, mas ver [[Dúvidas em aberto]])

## Pegadinhas que já descobri
- O status no banco é em inglês (`AWAITING_PAYMENT`), na tela aparece em português. Mapeamento em `OrderStatusLabel`.
- Pedido nunca é deletado, só cancelado (auditoria fiscal). #confirmado
