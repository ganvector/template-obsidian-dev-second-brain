# 🧠 Vault de Onboarding em Projetos

Template de vault do [Obsidian](https://obsidian.md) para **entender, registrar e lembrar as regras de negócio** de um projeto de software. Ele funciona como uma "segunda memória" enquanto você trabalha em cards e sprints.

Vem preenchido com um projeto fictício (**Loja Online**) para mostrar como cada tipo de nota fica na prática. Para usar num projeto real, veja [Começando um projeto novo](#-começando-um-projeto-novo).

---

## 💡 A ideia

Desenvolvedor bom não memoriza: **externaliza** o conhecimento e o reconstrói quando precisa. Este vault se apoia em três princípios:

1. **Anotar na hora, organizar depois.** Primeiro vai para o Diário ou para a nota do card, mesmo mal escrito. Uma vez por semana, o que for útil vai para as notas permanentes.
2. **Separar o temporário do permanente.** Cards fecham e somem; regras, entidades e o glossário ficam. Ao fechar um card, faça a **colheita**: leve o que ele te ensinou para as notas permanentes.
3. **Exemplos concretos acima de regras abstratas.** Toda regra tem uma tabela de exemplos. Exemplos são o que fica na memória (e viram testes).

---

## 🗂️ Estrutura

| Pasta / Nota | O que guarda | Permanente? |
|---|---|---|
| `00 - Comece aqui` | Índice geral, gerado automaticamente | — |
| `Glossário` | Linguagem ubíqua: termo → significado → onde está no código → confusões comuns | ✅ |
| `Domínio/` | Entidades (Pedido, Cliente…) com ciclo de vida em diagrama de estados e "pegadinhas" | ✅ |
| `Regras/` | Regras de negócio (`RN-XXX`) com o porquê, uma tabela de exemplos e o histórico de mudanças | ✅ |
| `Fluxos/` | Fluxos ponta a ponta (Event Storming + diagrama de sequência) | ✅ |
| `Arquitetura/` | Visão de sistemas (C4) | ✅ |
| `Decisões/` | ADRs: o *porquê* das decisões técnicas | ✅ |
| `Pessoas/` | Quem sabe o quê: para quem perguntar cada assunto | ✅ |
| `Caixa de ferramentas/` | Queries, comandos, roteiros de debug, snippets — separados pelo campo `tipo` | ✅ |
| `Excalidraw/` | Desenhos livres (quadros de Event Storming, rascunhos) | ✅ |
| `Cards/` | Uma nota por card da sprint que **te ensinou algo** (história ou bug) | ⏳ |
| `Diário/` | Nota diária: o que aprendi, onde travei, dúvidas novas | ⏳ |
| `Dúvidas em aberto` | Lista **automática** de todas as dúvidas não respondidas do vault | — |
| `Templates/` | Modelos de cada tipo de nota | — |

---

## 🔌 Plugins

| Plugin | Tipo | Para quê |
|---|---|---|
| Templates | Nativo | Criar notas a partir de `Templates/` |
| Notas diárias | Nativo | Diário em `Diário/AAAA-MM-DD` |
| [Dataview](https://github.com/blacksmithgu/obsidian-dataview) | Comunidade | Índices, listas de dúvidas e painel de cards automáticos |
| [Excalidraw](https://github.com/zsviczian/obsidian-excalidraw-plugin) | Comunidade | Desenhos e quadros de Event Storming |

Os plugins e as configurações já vêm na pasta `.obsidian/`. Ao abrir o vault, o Obsidian pergunta se você confia nos plugins; clique em **"Confiar e ativar"**.

> [!IMPORTANT]
> **Dataview com JavaScript:** o índice do `00 - Comece aqui` e o da Caixa de ferramentas usam consultas em JavaScript, que ficam desligadas por padrão no Dataview. Este template já vem com elas ligadas (`.obsidian/plugins/dataview/data.json`). Se aparecer código em vez de links, ative em *Configurações → Dataview*:
> - Enable JavaScript Queries
> - Enable Inline JavaScript Queries

---

## 🔁 Rotina de uso

| Quando | O que fazer |
|---|---|
| **Todo dia** | Abrir a nota diária: o que aprendi, onde travei, dúvidas novas |
| **Termo novo** | Direto para o `Glossário` |
| **Regra descoberta** | Nova nota em `Regras/`, com tag `#suposicao` até confirmar com o negócio |
| **Pegou um card que vai ensinar algo** | Nota em `Cards/` (template História ou Bug) com links para as regras e entidades que ele toca |
| **Fechou o card** | **Colheita**: atualizar regras (exemplos + histórico), glossário, pegadinhas, ADR se for o caso |
| **Resolveu algo técnico que vai usar de novo** | Nota na `Caixa de ferramentas/` |
| **Fim da sprint** | Abrir `Cards/00 - Painel de cards`, conferir colheitas pendentes e revisar `Dúvidas em aberto` |

> Nem todo card precisa de nota. Só crie para os que te ensinaram algo.

---

## 📐 Convenções

**Nomes de arquivo**
- Regras: `RN-001 Nome curto`
- Decisões: `ADR-001 Nome curto`
- Cards: `CHAVE-123 Título curto` (a chave do Jira/Azure)
- Ferramentas: `Query - …`, `Comando - …`, `Debug - …`

**Tags de confiança**
- `#confirmado`: validado com alguém do negócio
- `#suposicao`: deduzido do código, falta confirmar (aparece com ⚠️ no índice)

**Dúvidas:** escreva `- [ ] pergunta` sob um título que contenha **"Dúvida"** em qualquer nota. Ela aparece sozinha em `Dúvidas em aberto`. Marcou o checkbox, saiu da lista.

**Mermaid × Excalidraw**
- **Mermaid** (texto, dentro da nota) para o que precisa ser preciso e ficar atualizado: estados, sequências, arquitetura.
- **Excalidraw** para pensar, descobrir e explicar. É uma foto do quadro branco e não precisa ser mantido.

### Campos de frontmatter usados pelo Dataview

| Onde | Campo | Valores |
|---|---|---|
| `Cards/` | `tipo` | `historia` · `bug` |
| `Cards/` | `status` | `em-andamento` · `fechado` |
| `Cards/` | `sprint`, `card`, `toca` | número, URL do card, notas relacionadas |
| `Caixa de ferramentas/` | `tipo` | `query` · `comando` · `debug` · `snippet` · `ambiente` (ou qualquer outro) |
| `Caixa de ferramentas/` | `serve` | uma frase dizendo para que serve (aparece no índice) |
| `Caixa de ferramentas/` | `toca` | links para entidades e regras (`"[[Pedido]]"`) |

---

## 🚀 Começando um projeto novo

1. **Crie o vault a partir deste template.** No GitHub, use o botão *Use this template*, ou clone:
   ```bash
   git clone <url-deste-repo> "Vault - Nome do Projeto"
   ```
2. **Abra no Obsidian:** *Abrir pasta como vault* e confie nos plugins.
3. **Apague o conteúdo de exemplo**, mas mantenha as pastas, os templates e os índices:
   ```bash
   cd "Vault - Nome do Projeto"
   find Domínio Regras Fluxos Arquitetura Decisões Diário Excalidraw -name "*.md" -delete
   find Cards "Caixa de ferramentas" -name "*.md" ! -name "00 - *" -delete
   ```
4. **Limpe as notas únicas**, mantendo a estrutura: `Glossário`, `Pessoas/Quem sabe o quê`, a seção "Dúvidas gerais" de `Dúvidas em aberto` e o título do `00 - Comece aqui`.
5. **Primeira semana:**
   - Glossário desde o primeiro dia
   - Um Event Storming (no Excalidraw, mesmo sozinho) do fluxo principal
   - Diagrama de estados das 2 ou 3 entidades centrais

> Se preferir manter o exemplo da Loja como referência, faça o passo 3 numa branch ou guarde uma cópia em `_exemplo/`.

---

## 📚 Técnicas por trás do template

- **DDD — Linguagem Ubíqua** → `Glossário`
- **Event Storming** e **Domain Storytelling** → `Fluxos/` e `Excalidraw/`
- **Example Mapping (BDD)** → tabelas de exemplos em `Regras/`
- **C4 Model** → `Arquitetura/`
- **ADR (Architecture Decision Records)** → `Decisões/`
- **Técnica Feynman** → escrever cada regra como se fosse explicar para alguém
