---
tags: [duvidas]
---
# ❓ Dúvidas em aberto

> [!info] Como funciona
> A lista abaixo junta **automaticamente** todo checkbox não marcado que esteja sob um título com a palavra **"Dúvida"** em qualquer nota (Regras, Cards, Diário, Entidades...).
> - Para registrar uma dúvida: escreva `- [ ] pergunta` na seção **Dúvidas** da nota onde ela surgiu.
> - Para responder: marque o checkbox (pode ser direto aqui na lista, ele marca na nota original) e escreva a resposta ao lado → some da lista.
> - Dúvida que não pertence a nenhuma nota? Escreva em **Dúvidas gerais**, no fim desta página.

## 🔴 Abertas (por nota)
```dataview
TASK
FROM -"Templates"
WHERE !completed
  AND contains(meta(section).subpath, "Dúvida")
  AND file.path != this.file.path
GROUP BY file.link
```

## ✅ Respondidas (para revisar de vez em quando)
```dataview
TASK
FROM -"Templates"
WHERE completed
  AND contains(meta(section).subpath, "Dúvida")
GROUP BY file.link
```

## Dúvidas gerais
- [ ] Pedido vai algum dia aceitar dois meios de pagamento (ex: cartão + vale)? Se sim, a relação 1:1 com [[Pagamento]] quebra.
- [ ] Por que o carrinho expira em 7 dias? Regra de negócio ou limite técnico do Redis?
- [x] ~~O que acontece se o webhook não chegar?~~ → respondido em [[Fluxo - Checkout]]
