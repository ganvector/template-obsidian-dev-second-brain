---
tags: [indice]
---
# 🧭 Comece aqui — Projeto Loja Online

> [!info] O que é este vault
> Minha "segunda memória" do projeto. **Regra de ouro:** se eu precisei perguntar ou descobrir algo, anoto aqui em até 5 minutos, mesmo que mal escrito. Revisar depois é mais fácil que lembrar.

## Mapa do conhecimento
> [!tip] Gerado automaticamente
> As linhas com 🔄 🧱 📏 🧠 🎨 🗂️ se atualizam sozinhas (Dataview) conforme você cria notas nas pastas. ⚠️ = regra ainda com `#suposicao`.

- 📖 [[Glossário]] — termos do negócio (comece por aqui sempre)
- 🏗️ Arquitetura: `$= dv.pages('"Arquitetura"').sort(p => p.file.name).file.link.join(" · ")`
- 🔄 Fluxos: `$= dv.pages('"Fluxos"').sort(p => p.file.name).file.link.join(" · ")`
- 🧱 Entidades: `$= dv.pages('"Domínio"').sort(p => p.file.name).file.link.join(" · ")`
- 📏 Regras: `$= dv.pages('"Regras"').sort(p => p.file.name).map(p => p.file.link + (p.file.tags.includes("#suposicao") ? " ⚠️" : "")).join(" · ")`
- 🧠 Decisões: `$= dv.pages('"Decisões"').sort(p => p.file.name).file.link.join(" · ")`
- 🎨 Desenhos: `$= dv.pages('"Excalidraw"').sort(p => p.file.name).file.link.join(" · ")`
- 🗂️ Cards em andamento: `$= (l => l.length ? l.join(" · ") : "nenhum")(dv.pages('"Cards"').where(p => p.status == "em-andamento").file.link)` — ver [[00 - Painel de cards]]
- 🧰 Caixa de ferramentas: `$= dv.pages('"Caixa de ferramentas"').where(p => p.tipo).length` itens — ver [[00 - Caixa de ferramentas]]
- 👥 [[Quem sabe o quê]]
- ❓ [[Dúvidas em aberto]] — `$= dv.pages('-"Templates"').file.tasks.where(t => !t.completed && (t.section.subpath || "").includes("Dúvida")).length` abertas

## Como uso
1. **Todo dia**: nota no Diário (atalho da nota diária) com o que aprendi e o que ficou em dúvida.
2. **Toda sexta**: 15 min passando o diário para as notas "oficiais" (Regras, Entidades, Glossário).
3. **Termo novo?** → vai pro [[Glossário]] na hora.
4. **Descobri uma regra?** → nova nota a partir de `Templates/Template - Regra`.
5. **Peguei um card que vai me ensinar algo?** → nota em `Cards/` (template História ou Bug). Ao fechar, faço a **colheita**: levo o que aprendi para Regras/Entidades/Glossário.
6. **Resolvi algo técnico que vou precisar de novo?** (query, comando, roteiro de debug) → nota em `Caixa de ferramentas/` com o template Ferramenta.
7. **Fim da sprint** → abro o [[00 - Painel de cards]] e confiro se toda colheita foi feita.

## Convenções
- Regras de negócio: `RN-XXX Nome curto`
- Decisões: `ADR-XXX Nome curto`
- Tags de status: `#confirmado` (validei com alguém de negócio) · `#suposicao` (deduzi do código, falta confirmar)
