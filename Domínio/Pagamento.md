---
tags: [entidade]
aliases: [Payment]
---
# 🧱 Pagamento

**Em uma frase:** a cobrança de um [[Pedido]], feita em duas etapas (pré-autorização → captura).
**Código:** `payments/` (serviço separado!) · integra com gateway externo
**Por que é assíncrono:** [[ADR-001 Pagamento assíncrono via fila]]

## Ciclo de vida
```mermaid
stateDiagram-v2
    [*] --> PENDENTE
    PENDENTE --> PRE_AUTORIZADO: gateway aprova
    PENDENTE --> RECUSADO: gateway recusa
    PRE_AUTORIZADO --> CAPTURADO: pedido despachado
    PRE_AUTORIZADO --> LIBERADO: pedido cancelado antes do despacho
    CAPTURADO --> ESTORNADO: devolução
```

## Pegadinhas
- Pix não tem pré-autorização: vai direto para `CAPTURADO`. Cancelar Pix = sempre estorno. #confirmado
- Webhook do gateway pode chegar **duplicado**; o handler é idempotente pelo `gateway_transaction_id`.
