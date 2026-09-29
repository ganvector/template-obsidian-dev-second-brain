---
tipo: debug
serve: Roteiro para descobrir por que um pedido específico ficou preso aguardando pagamento
tags: [pagamento, fila, webhook]
toca: ["[[Pedido]]", "[[Pagamento]]", "[[ADR-001 Pagamento assíncrono via fila]]"]
---
# 🐞 Debug — Pedido não sai de "aguardando pagamento"

> **Para que serve:** roteiro passo a passo para um pedido específico preso. Segue o caminho do [[Fluxo - Checkout]] e para no primeiro elo quebrado.

## Quando usar
- Um pedido específico reclamado pelo SAC
- Para vários pedidos de uma vez, comece pela [[Query - Pedidos presos aguardando pagamento]]

## Roteiro (seguir em ordem)
1. **O evento saiu do Orders?** Procure `OrderCreated` com o id do pedido nos logs do Orders API.
   - Não achou → problema na publicação (Orders ou RabbitMQ).
2. **O Payments consumiu?** Veja a fila `payments.order-created` (ver [[Comando - Filas do RabbitMQ]]). Mensagem parada na DLQ?
   - Na DLQ → leia o motivo no header `x-death`.
3. **O Payments pediu pré-autorização ao gateway?** Log `PreAuthorizationRequested` com o id.
4. **O webhook do gateway chegou?** Procure pelo `gateway_transaction_id` nos logs do webhook.
   - Não chegou → consultar o status direto no painel do gateway.
   - Chegou **duplicado** → normal, handler é idempotente (ver [[Pagamento]]).
5. **O `PaymentApproved` voltou para o Orders?** Se sim e o status não mudou → bug no consumer do Orders.

## Cuidados
- Não reprocessar a DLQ inteira sem olhar: pode duplicar pré-autorização em pedidos que já foram cancelados.

## Histórico de uso
- 2026-09-24 — causa: RabbitMQ caiu entre os passos 1 e 2. Reprocessei a DLQ.
