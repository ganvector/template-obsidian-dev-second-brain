---
tipo: historia
card: https://jira.exemplo.com/browse/LOJA-510
sprint: 43
status: em-andamento
toca: [RN-001 Cancelamento de pedido, Pedido]
---
# LOJA-510 Cobrar taxa ao cancelar pedido já separado

**Card:** [LOJA-510](https://jira.exemplo.com/browse/LOJA-510)
**Toca em:** [[RN-001 Cancelamento de pedido]] · [[Pedido]] · [[Pagamento]]

## Entendimento inicial
Hoje dá para cancelar em `EM_SEPARACAO` sem custo, mas devolver itens ao estoque custa ao CD. O negócio quer cobrar uma taxa nesse caso.

## O que descobri
- Isso responde a dúvida aberta da RN-001 ("tem custo devolver ao estoque?") → **sim**, segundo [[Carlos Mendes|Carlos]].
- Problema: cartão está só **pré-autorizado**. Para cobrar taxa, precisa de **captura parcial** do valor da taxa e liberação do resto. O gateway suporta? 🤔
- Pix já está capturado → seria estorno parcial (valor − taxa).

## Decisões
- (pendente) valor da taxa: fixo ou % do pedido?

## Dúvidas
- [ ] Gateway suporta captura parcial? → perguntar para [[Bruna Costa|Bruna]]
- [ ] Taxa fixa ou percentual? → [[Ana Lima|Ana]]
- [ ] Como mostrar a taxa ao cliente ANTES dele confirmar o cancelamento?

## Colheita (antes de fechar o card)
- [ ] [[RN-001 Cancelamento de pedido]]: novas linhas na tabela (cancelamento em separação com taxa)
- [ ] [[Glossário]]: "Captura parcial", "Taxa de cancelamento"
- [ ] [[Pagamento]]: novo estado/transição de captura parcial?
- [ ] Provável ADR se mudar o fluxo de pagamento
