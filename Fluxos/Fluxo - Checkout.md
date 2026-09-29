---
tags: [fluxo]
---
# 🔄 Fluxo — Checkout

## Quadro de Event Storming (Excalidraw)
> Versão "quadro branco" para pensar e reorganizar. Clique para abrir e editar.

![[Event Storming - Checkout.excalidraw]]

## Linha do tempo de eventos (estilo Event Storming)
> Laranja = evento · Azul = comando · Amarelo = ator · Rosa = problema/dúvida

```mermaid
flowchart LR
    A([👤 Cliente]):::ator --> C1[Finalizar compra]:::cmd
    C1 --> E1(Pedido criado):::evt
    E1 --> E2(Pré-autorização solicitada):::evt
    E2 --> E3(Pagamento aprovado):::evt
    E3 --> E4(Pedido enviado ao CD):::evt
    E4 --> E5(Pedido despachado):::evt
    E5 --> E6(Pagamento capturado):::evt
    E2 -.-> P1{{E se o webhook nunca chegar?}}:::prob

    classDef evt fill:#f9a825,color:#000
    classDef cmd fill:#64b5f6,color:#000
    classDef ator fill:#fff176,color:#000
    classDef prob fill:#f48fb1,color:#000
```

## Sequência técnica
```mermaid
sequenceDiagram
    participant F as Front
    participant O as Orders API
    participant Q as Fila
    participant P as Payments
    participant G as Gateway
    F->>O: POST /orders
    O->>O: cria Pedido (CRIADO)
    O->>Q: publica OrderCreated
    O-->>F: 201 (status: aguardando)
    Q->>P: consome OrderCreated
    P->>G: pré-autoriza
    G-->>P: webhook: aprovado
    P->>Q: publica PaymentApproved
    Q->>O: consome → Pedido PAGO
```

## Respostas
- Webhook que nunca chega: há um job que expira pedidos em `AGUARDANDO_PAGAMENTO` após 30 min. Ver [[Pedido]].
