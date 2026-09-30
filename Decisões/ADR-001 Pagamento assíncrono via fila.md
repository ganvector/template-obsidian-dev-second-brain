---
tags: [adr]
status: aceita
data: 2025-03-10
---
# 🧠 ADR-001 Pagamento assíncrono via fila

**Autora:** [[Bruna Costa|Bruna]]

## Contexto
O gateway de pagamento às vezes demora 20s+ para responder na Black Friday, travando o checkout.

## Decisão
O checkout cria o [[Pedido]] e responde na hora. O [[Pagamento]] é processado de forma assíncrona via fila.

## Consequências
- ✅ Checkout rápido mesmo com gateway lento
- ⚠️ A tela precisa mostrar "aguardando pagamento" e fazer polling
- ⚠️ Precisa de job para expirar pedidos sem resposta (ver [[Fluxo - Checkout]])

## Alternativas descartadas
- Timeout maior no checkout — pior experiência para o cliente
