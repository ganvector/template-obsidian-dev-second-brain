---
tags: [glossario]
---
# 📖 Glossário (Linguagem Ubíqua)

> [!tip] Formato
> **Termo** — significado em uma frase, *no idioma do negócio*.
> Onde aparece no código · Cuidado com (confusões comuns)

---

**Pedido** — Intenção de compra de um [[Cliente]], com itens, endereço e forma de pagamento. Ver [[Pedido]].
- Código: `Order` (módulo `orders`)
- ⚠️ Cuidado: o time de negócio chama de "venda" só depois de *pago*. Pedido ≠ Venda.

**Venda** — Pedido com pagamento aprovado. Não existe como entidade no código; é um `Order` com status `PAID` ou além.

**Carrinho** — Itens escolhidos antes de virar pedido. Expira em 7 dias.
- Código: `Cart` (Redis, não vai pro banco)

**Pré-autorização** — Reserva do valor no cartão *sem cobrar*. A cobrança real é a **captura**.
- Código: `PaymentAuthorization`
- ⚠️ Cuidado: se não capturar em 5 dias, o banco libera o valor sozinho. #confirmado

**Captura** — Cobrança efetiva de um valor pré-autorizado. Acontece no despacho.

**Despacho** — Momento em que o pedido sai do centro de distribuição (CD). Gera nota fiscal.

**SLA de separação** — Prazo interno para o CD separar os itens: 24h úteis. #suposicao

**Cliente VIP** — Cliente com 5+ pedidos pagos nos últimos 12 meses. Ver [[RN-002 Frete grátis]].
- Código: `CustomerTier.VIP` — calculado por job noturno, não em tempo real!

**Estorno** — Devolução de valor já *capturado*. Diferente de cancelar pré-autorização (que é só liberar a reserva).

**Subtotal bruto** — Soma dos itens **antes** de cupons. É o que vale para [[RN-002 Frete grátis]].
**Subtotal líquido** — Soma dos itens **depois** de cupons. É o que o cliente paga (mais frete).
- ⚠️ Cuidado: no código antigo `subtotal` às vezes é um, às vezes é outro. Aprendido no [[LOJA-482 Frete grátis antes do cupom]].
