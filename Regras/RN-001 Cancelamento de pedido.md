---
tags: [regra, confirmado]
entidades: [Pedido, Pagamento]
fonte: Ana (PO) em 2026-09-29
---
# 📏 RN-001 Cancelamento de pedido

## A regra
O cliente pode cancelar sozinho **até o despacho**. Depois disso, só via devolução (outro fluxo).

## O porquê
Após o despacho já houve captura e nota fiscal; desfazer isso tem custo operacional e fiscal.

## Exemplos (a parte mais importante!)
| Situação | Status atual | Pagamento | Resultado esperado |
|---|---|---|---|
| Cancela 10 min após comprar | PAGO | Cartão, pré-autorizado | ✅ Cancela, **libera** a reserva |
| Cancela durante separação | EM_SEPARACAO | Cartão, pré-autorizado | ✅ Cancela, libera reserva, avisa o CD |
| Cancela pedido pago com Pix | PAGO | Pix, capturado | ✅ Cancela, gera **estorno** (até 2 dias úteis) |
| Tenta cancelar após despacho | DESPACHADO | Capturado | ❌ Botão some; mostra "solicitar devolução" |

## Onde está no código
- `Order.cancel()` — valida o status
- `CancelOrderUseCase` — orquestra liberação/estorno
- Testes: `CancelOrderUseCaseTest` (cobre as 4 linhas acima)

## Dúvidas
- [x] ~~E se o CD já separou mas ainda não despachou? Tem custo?~~ → Sim, tem custo. Virou o card [[LOJA-510 Cancelamento após separação]] (em andamento)
