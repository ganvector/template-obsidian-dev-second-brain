---
tags: [indice]
---
# 🧰 Caixa de ferramentas

> [!info] Como funciona
> Tudo que é **"como fazer"** técnico mora aqui, numa pasta só: queries, comandos, processos de debug, snippets, acessos, configurações de ambiente...
> - Crie a nota com `Templates/Template - Ferramenta` e escolha o `tipo` no frontmatter.
> - Tipos sugeridos: `query` · `comando` · `debug` · `snippet` · `ambiente` (pode inventar outros — o índice se adapta sozinho).
> - Em `toca:` ponha as entidades/regras relacionadas → a ferramenta aparece nos *backlinks* da nota de [[Pedido]], por exemplo.
> - O que realmente importa: a linha **"Para que serve"**. É ela que você vai ler daqui a 3 meses.

```dataviewjs
const tipos = { query: "🗃️ Queries", comando: "⌨️ Comandos", debug: "🐞 Processos de debug", snippet: "✂️ Snippets", ambiente: "⚙️ Ambiente e acessos" };
const notas = dv.pages('"Utils"').where(p => p.file.name !== dv.current().file.name);
for (const grupo of notas.groupBy(p => p.tipo ?? "sem tipo").sort(g => g.key)) {
  dv.header(3, tipos[grupo.key] ?? `📎 ${grupo.key}`);
  dv.table(["Nota", "Para que serve", "Toca em"],
    grupo.rows.sort(p => p.file.name).map(p => {
      return [p.file.link, p.serve ?? "", p.toca ?? ""];
    }));
}
```
