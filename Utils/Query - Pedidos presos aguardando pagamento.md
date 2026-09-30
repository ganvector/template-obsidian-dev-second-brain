---
tipo: query
serve: Achar pedidos travados em AGUARDANDO_PAGAMENTO há mais de 30 min (o job de expiração falhou?)
tags: [postgres, pedidos]
toca: ["[[Pedido]]", "[[Fluxo - Checkout]]"]
---
# 🗃️ Query — Pedidos presos aguardando pagamento

> **Para que serve:** achar pedidos travados em `AWAITING_PAYMENT` há mais tempo do que o job de expiração permite (30 min). Se aparecer algo, o job falhou ou o webhook se perdeu.

## Quando usar
- SAC reclama de "pedido que não anda"
- Depois de incidente com a fila / RabbitMQ

## Conteúdo
```sql
SELECT o.id,
       o.customer_id,
       o.created_at,
       now() - o.created_at AS parado_ha
FROM   orders o
WHERE  o.status = 'AWAITING_PAYMENT'
  AND  o.created_at < now() - interval '30 minutes'
ORDER  BY o.created_at;
```

## Cuidados
- Banco de **orders** só. O status do pagamento está no banco de payments (bancos separados, ver [[Visão geral (C4)]]) → para cruzar, use o id no [[Debug - Pedido não sai de aguardando pagamento|processo de debug]].
- Rodar na **réplica de leitura**, nunca na primária.

## Histórico de uso
- 2026-09-24 — achou 12 pedidos depois da queda do RabbitMQ
