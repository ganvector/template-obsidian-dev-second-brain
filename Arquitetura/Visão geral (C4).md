---
tags: [arquitetura]
---
# 🏗️ Visão geral — nível Container (C4)

```mermaid
flowchart TB
    cli([👤 Cliente])
    subgraph Loja
        web[Front Web<br/>React]
        ord[Orders API<br/>Spring Boot]
        pay[Payments Service<br/>Spring Boot]
        db[(Postgres<br/>orders)]
        redis[(Redis<br/>carrinho)]
        mq[[RabbitMQ]]
    end
    gw[Gateway de pagamento<br/>externo]
    erp[ERP / CD<br/>externo]

    cli --> web --> ord
    ord --> db
    ord --> redis
    ord <--> mq <--> pay
    pay --> gw
    ord --> erp
```

## Notas
- Orders e Payments têm bancos **separados**; não existe join entre pedido e pagamento. Consultas combinadas passam pela API.
- Integração com ERP é via arquivo CSV em SFTP a cada 15 min (!!). Sim, é real.
