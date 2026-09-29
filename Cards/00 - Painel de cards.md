---
tags: [indice]
---
# 🗂️ Painel de cards

> [!info] Como funciona
> Só crio nota para card que me **ensinou algo** (ou que ainda vai ensinar). Card de trocar texto de botão não precisa.
> - História → `Templates/Template - Card História`
> - Bug → `Templates/Template - Card Bug`
> - Nome da nota: `CHAVE-DO-CARD Título curto`

## Lista manual (funciona sem plugin)
**Em andamento**
- [[LOJA-510 Cancelamento após separação]] — sprint 43

**Fechados**
- [[LOJA-482 Frete grátis antes do cupom]] — sprint 42
- 🐞 [[LOJA-497 Cliente VIP novo sem frete grátis]] — sprint 42

## Listas automáticas (precisa do plugin Dataview)
> Instale em *Configurações → Plugins da comunidade → Dataview*. Depois disso as tabelas abaixo se montam sozinhas a partir do frontmatter.

### Em andamento
```dataview
TABLE tipo, sprint, toca
FROM "Cards"
WHERE status = "em-andamento"
SORT sprint DESC
```

### Colheita pendente (cards com checklist da colheita incompleto)
```dataview
TASK
FROM "Cards"
WHERE !completed AND contains(meta(section).subpath, "Colheita")
```

### Bugs por regra
```dataview
TABLE toca AS "Toca em", sprint
FROM "Cards"
WHERE tipo = "bug"
```
