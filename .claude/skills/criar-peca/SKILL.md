---
name: criar-peca
description: Transforma um texto de post já aprovado pelo Dr. Ícaro em uma peça visual (carrossel, página, post único etc.) no Claude Design (/design), com o design system da marca, usando exatamente o texto aprovado. Salva o link, o texto e os arquivos exportados em pecas/, pede ao revisor a comparação palavra por palavra e, se a peça for uma página, aciona o desenvolvedor só com plano e pull request. Nunca publica, agenda nem envia nada. Use quando o Dr. Ícaro pedir para montar ou diagramar no Design uma peça a partir de um texto aprovado.
---

# Criar peça no Design

Esta skill transforma um texto já aprovado pelo Dr. Ícaro em uma peça visual no Claude Design (o `/design`, servidor MCP `claude-design` configurado em `.mcp.json`). Ela coordena dois subagentes: `revisor` e, quando a peça for uma página, `desenvolvedor`.

## Regras fixas

1. **Texto aprovado, sem mudança.** A peça usa EXATAMENTE o texto aprovado, palavra por palavra, com a mesma pontuação e a mesma ordem. Não acrescente frases, títulos, números, dados, chamadas para ação, promessas de resultado nem legendas novas. Não corte, resuma nem reescreva. Se o texto não couber no formato ou faltar algo que a peça exige, pare e pergunte ao Dr. Ícaro.
2. **Imagens.** Nada de imagens de pacientes nem de banco de imagens. Use só os elementos do design system da marca (logo, cores, tipografia, patterns, linha de contorno do símbolo) e texto sobre o fundo da identidade visual. Imagens próprias do Dr. Ícaro ou de ultrassom só se ele as fornecer para esta peça.
3. **Design system da marca.** Use o design system da marca do Dr. Ícaro no Design. Se não encontrar um claramente identificado como da marca, ou se houver mais de um, pare e pergunte qual usar. Não crie nem altere o design system.
4. **Nunca publicar, agendar, enviar nem compartilhar nada**, em nenhum canal, nem mudar a visibilidade do projeto no Design. O resultado é sempre um rascunho para aprovação.
5. **Nunca apagar nem sobrescrever** projetos, versões ou arquivos existentes, no Design ou no repositório.
6. **Sem Design, sem peça.** Se o Design não estiver conectado, as ferramentas do `claude-design` não aparecerem ou o login tiver expirado, **pare e avise o Dr. Ícaro**. Não tente contornar: não monte a peça no Canva, em HTML, em artifact ou em outra ferramenta, e não peça senhas, tokens nem códigos de autorização.

O `CLAUDE.md` da raiz é a fonte de verdade para identidade visual, regra do RQE e checklist CFM; em caso de conflito com esta skill, vale o `CLAUDE.md`.

## Fluxo

### 0. Conferir a entrada

- **Texto aprovado:** colado na conversa ou em um arquivo (por exemplo, de `rascunhos/`). Se o arquivo tiver mais de uma variação, pergunte qual foi aprovada. Se não estiver claro que o texto foi aprovado pelo Dr. Ícaro, pergunte antes de seguir.
- **Formato:** carrossel, post único, página (site, captação) etc. Se não for dito, pergunte.
- **Conferência rápida do texto contra o `CLAUDE.md`**, sem alterá-lo: se faltar nome, CRM/UF e RQE (obrigatórios em toda peça publicitária) ou se algo conflitar com o checklist CFM, avise e pergunte como seguir. Não acrescente nada por conta própria.
- Guarde uma cópia literal do texto aprovado; ela é a referência das etapas seguintes.

### 1. Criar a peça no Design

- Confira se as ferramentas do `claude-design` estão disponíveis (carregue-as com ToolSearch, se for preciso). Se não estiverem, ou se qualquer chamada indicar falta de login ou login expirado, siga a regra fixa 6.
- Localize o design system da marca e crie um projeto novo com ele, no formato pedido.
- Distribua o texto aprovado nas páginas ou seções sem mudar nenhuma palavra. A divisão entre páginas pode seguir as quebras do próprio texto (por exemplo, "Página 1", "Página 2"); se não houver quebras, proponha a divisão ao Dr. Ícaro antes de montar.
- Respeite a identidade visual do `CLAUDE.md`: paleta Maastricht Blue `#041E42`, Âmbar `#FFBF00` e Branco `#FFFFFF`; tipografia Exo; logo sem distorção, efeitos ou mudança de cor; patterns só como suporte.

### 2. Salvar em `pecas/`

Crie a pasta `pecas/AAAA-MM-DD-formato-tema/` (por exemplo, `pecas/2026-10-26-carrossel-dor-no-joelho/`). Se o nome já existir, acrescente `-2`; nunca sobrescreva. Dentro dela:

- `peca.md` com:
  - status: rascunho para aprovação; nada foi publicado, agendado, enviado nem compartilhado;
  - ferramenta: Claude Design, com o link do projeto e o nome do design system usado;
  - formato e data;
  - origem do texto aprovado (arquivo ou "colado na conversa") e o texto literal usado, dividido como na peça;
  - lista dos arquivos exportados;
  - **não exportado:** o que não pôde ser exportado automaticamente, com o motivo e como o Dr. Ícaro pode exportar pelo Design.
- Os arquivos exportados que o Design permitir (por exemplo, uma imagem por página do carrossel, PDF ou o pacote de código de uma página).

### 3. Revisão do texto (`revisor`)

Leia o texto como ficou na peça (pelo projeto no Design ou pelos arquivos exportados) e chame o subagente `revisor` com:
- o texto aprovado (literal);
- o texto extraído da peça, página por página;
- o caminho de `peca.md`.

Peça que ele compare os dois **palavra por palavra**, incluindo pontuação, acentos, maiúsculas, quebras e ordem, e aponte qualquer diferença (palavra trocada, faltando ou acrescentada) com a página e o trecho. Peça também que confira nome, CRM/UF e RQE e o checklist CFM do `CLAUDE.md`.

Se houver diferença, corrija a peça no Design para que fique igual ao texto aprovado e passe de novo pelo `revisor`, no máximo duas vezes. O que continuar diferente vai para a entrega como pendência. Registre o resultado da revisão em `peca.md`.

### 4. Página: acionar o `desenvolvedor`

Só quando o formato for uma página (site, página de captação etc.):

- Salve na pasta da peça o pacote do Design que puder ser exportado (código, imagens, especificações). O `desenvolvedor` não acessa o Design; ele trabalha só com os arquivos do repositório.
- Chame o subagente `desenvolvedor` com o caminho da pasta, o texto aprovado e a instrução de **entregar primeiro só o plano**, sem publicar, sem deploy, sem enviar nada e sem formulários que coletem dados sem avisar (LGPD).
- Leve o plano ao Dr. Ícaro. Só com o OK dele, chame o `desenvolvedor` de novo para implementar numa branch própria e abrir um pull request. O pull request fica aberto para a aprovação do Dr. Ícaro; não faça merge.
- Peça ao `revisor` que confira os arquivos alterados pelo `desenvolvedor`, como pedem as instruções dele.

### 5. Entrega para aprovação

Apresente ao Dr. Ícaro:

1. **Status:** rascunho para aprovação. Nada foi publicado, agendado, enviado nem compartilhado.
2. **Link do projeto no Design** e o caminho da pasta em `pecas/`.
3. **Arquivos exportados** e o que **não** pôde ser exportado, com o motivo.
4. **Resultado da revisão:** as diferenças apontadas pelo `revisor` e o que foi corrigido.
5. **Página (se for o caso):** o plano do `desenvolvedor` ou o link do pull request.
6. **Conferir antes de usar:** pendências, falta de nome, CRM/UF e RQE, temas com restrição do CFM ou da Anvisa e decisões do Dr. Ícaro.

Termine perguntando se aprova a peça ou o que quer ajustar. Qualquer alteração depois da aprovação exige nova aprovação. Commit e push dos arquivos de `pecas/` também só com aprovação.
