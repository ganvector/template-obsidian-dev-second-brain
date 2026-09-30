---
tipo: comando
serve: Ver tamanho das filas, mensagens na DLQ e reprocessar mensagens no RabbitMQ
tags: [rabbitmq, fila, infra]
toca: ["[[ADR-001 Pagamento assíncrono via fila]]"]
---
# ⌨️ Comando — Filas do RabbitMQ

> **Para que serve:** inspecionar filas e reprocessar mensagens da DLQ sem abrir o painel web.

## Quando usar
- Passo 2 do [[Debug - Pedido não sai de aguardando pagamento]]
- Alerta de fila crescendo

## Conteúdo
```bash
# Listar filas com contagem de mensagens
kubectl exec -it rabbitmq-0 -n loja -- rabbitmqctl list_queues name messages consumers

# Ver só as DLQs
kubectl exec -it rabbitmq-0 -n loja -- rabbitmqctl list_queues name messages | grep dlq

# Mover mensagens da DLQ de volta para a fila (shovel)
kubectl exec -it rabbitmq-0 -n loja -- rabbitmqctl set_parameter shovel reprocessa-dlq \
  '{"src-queue":"payments.order-created.dlq","dest-queue":"payments.order-created","src-delete-after":"queue-length"}'
```

## Cuidados
- ⚠️ Em **produção**, avise no canal do time antes de mover a DLQ.
- O shovel se apaga sozinho após mover o que havia na fila (`queue-length`).

## Histórico de uso
- 2026-09-24 — reprocessei 12 mensagens após a queda
