---
tags: [pessoas, indice]
---
# 👥 Quem sabe o quê

> [!info] Como funciona
> Cada pessoa é uma nota nesta pasta (template `Templates/Template - Pessoa`). A tabela abaixo se monta sozinha, ordenada por **projeto** e depois por **nome**.
> Nas outras notas, cite a pessoa com um link (`[[Ana Lima|Ana]]`) → ela ganha a seção "Aparece em" automaticamente.

```dataview
TABLE WITHOUT ID
  aliases AS "Apelidos",
  projeto AS "Projeto",
  file.link AS "Pessoa",
  funcao AS "Função",
  sabe AS "Sabe sobre",
  contato AS "Contato"
FROM "Pessoas"
WHERE tipo = "pessoa"
SORT projeto ASC, file.name ASC
```
