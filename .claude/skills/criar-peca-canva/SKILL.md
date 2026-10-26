---
name: criar-peca-canva
description: Transforma um texto de post já aprovado pelo Dr. Ícaro em uma peça no Canva, a partir de uma cópia dos modelos e do kit de marca que ele já tem, usando exatamente o texto aprovado. Nunca altera o modelo original nem o kit de marca. Exporta a peça, salva o link e a lista de arquivos em pecas/ e pede ao revisor a comparação palavra por palavra. Nunca publica, agenda, compartilha nem apaga nada. Use quando o Dr. Ícaro pedir para montar no Canva uma peça a partir de um texto aprovado.
---

# Criar peça no Canva

Esta skill transforma um texto já aprovado pelo Dr. Ícaro em uma peça no Canva, usando o conector do Canva, o kit de marca e os modelos que ele já tem. Ela chama o subagente `revisor`.

## Regras fixas

1. **Duplicar antes de editar.** Antes de qualquer edição, crie uma cópia do modelo original (`copy-design` para um design; `create-design-from-brand-template` para um modelo de marca, que gera um design novo) e edite **apenas a cópia**. Antes de cada edição, confira que o ID do design é o da cópia. Nunca altere nem sobrescreva o original.
2. **Texto aprovado, sem mudança.** Use EXATAMENTE o texto aprovado, palavra por palavra, com a mesma pontuação e a mesma ordem. Não acrescente frases, títulos, números, dados, chamadas para ação, promessas de resultado nem legendas novas. Não corte, resuma nem reescreva. Textos de exemplo do modelo que sobrarem devem ser removidos da cópia, não preenchidos com texto novo. Se o texto não couber no modelo, pare e pergunte ao Dr. Ícaro.
3. **Imagens.** Nada de imagens de pacientes, de banco de imagens nem geradas por IA. Use só os elementos do kit de marca e do modelo. Imagens próprias do Dr. Ícaro ou de ultrassom só se ele as fornecer para esta peça. Se o modelo tiver uma foto de exemplo de pessoa, pergunte o que colocar no lugar.
4. **Sem ações proibidas.** Não altere o kit de marca, não apague nada, não mova itens entre pastas, não compartilhe, não comente, não publique nem agende, não crie nem publique modelos de marca. Se uma ação exigir qualquer uma dessas coisas, **pare e pergunte ao Dr. Ícaro**.
5. **Sem Canva, sem peça.** Se o Canva não estiver conectado, as ferramentas do Canva não aparecerem ou a autorização tiver expirado, **pare e avise o Dr. Ícaro** que ele precisa reconectar o Canva nas configurações de conectores do claude.ai. Não tente contornar: não monte a peça em outra ferramenta e não peça senhas, tokens nem códigos de autorização.

O `CLAUDE.md` da raiz é a fonte de verdade para identidade visual, regra do RQE e checklist CFM; em caso de conflito com esta skill, vale o `CLAUDE.md`. Para editar a cópia, siga também a skill `canva:edit-design`, se estiver disponível, sem desrespeitar as regras acima.

## Fluxo

### 0. Conferir a entrada

- **Texto aprovado:** colado na conversa ou em um arquivo (por exemplo, de `rascunhos/`). Se o arquivo tiver mais de uma variação, pergunte qual foi aprovada. Se não estiver claro que o texto foi aprovado pelo Dr. Ícaro, pergunte antes de seguir.
- **Formato:** carrossel, post único, Stories etc., e o formato de exportação (PNG, JPG, PDF etc.). Se o formato de exportação não for dito, use uma imagem PNG por página no carrossel; nos outros casos, pergunte.
- **Conferência rápida do texto contra o `CLAUDE.md`**, sem alterá-lo: se faltar nome, CRM/UF e RQE (obrigatórios em toda peça publicitária) ou se algo conflitar com o checklist CFM, avise e pergunte como seguir. Não acrescente nada por conta própria.
- Guarde uma cópia literal do texto aprovado; ela é a referência das etapas seguintes.

### 1. Escolher o modelo e o kit de marca

- Carregue as ferramentas do Canva (com ToolSearch, se for preciso). Se falharem por falta de conexão ou autorização, siga a regra fixa 5.
- Liste os kits de marca (`list-brand-kits`) e os modelos do Dr. Ícaro para o formato (`search-brand-templates` e `search-designs`), só lendo.
- Se houver mais de um modelo ou kit possível, mostre as opções e pergunte qual usar. Se não houver nenhum modelo para o formato, pare e pergunte; não crie um do zero sem o OK dele.

### 2. Duplicar e editar a cópia

- Crie a cópia do modelo (regra fixa 1) e dê a ela um título como `AAAA-MM-DD formato tema - rascunho`.
- Leia a cópia (`read-design`) e coloque o texto aprovado nos campos de texto, sem mudar nenhuma palavra. A divisão entre páginas segue as quebras do próprio texto (por exemplo, "Página 1", "Página 2"); se não houver quebras ou se o número de páginas do modelo for diferente, proponha a divisão ao Dr. Ícaro antes de editar.
- Respeite a identidade visual do `CLAUDE.md`: só a paleta e a tipografia do kit de marca, logo sem distorção, efeitos ou mudança de cor.

### 3. Exportar e salvar em `pecas/`

- Exporte a cópia (`export-design`) no formato pedido ou, no carrossel, uma imagem por página. Baixe os arquivos exportados para a pasta da peça.
- Crie a pasta `pecas/AAAA-MM-DD-formato-tema/` (por exemplo, `pecas/2026-10-26-carrossel-dor-no-joelho/`). Se o nome já existir, acrescente `-2`; nunca sobrescreva. Dentro dela, `peca.md` com:
  - status: rascunho para aprovação; nada foi publicado, agendado, enviado nem compartilhado;
  - ferramenta: Canva, com o link da cópia, o nome do modelo original e do kit de marca usados;
  - formato, formato de exportação e data;
  - origem do texto aprovado (arquivo ou "colado na conversa") e o texto literal usado, dividido como na peça;
  - lista dos arquivos exportados;
  - **não exportado:** o que não pôde ser exportado ou baixado automaticamente, com o motivo e como o Dr. Ícaro pode exportar pelo Canva.

### 4. Revisão do texto (`revisor`)

Leia o texto como ficou na cópia (`read-design`) e chame o subagente `revisor` com:
- o texto aprovado (literal);
- o texto extraído da peça, página por página;
- o caminho de `peca.md`.

Peça que ele compare os dois **palavra por palavra**, incluindo pontuação, acentos, maiúsculas, quebras e ordem, e aponte qualquer diferença (palavra trocada, faltando ou acrescentada, ou texto de exemplo do modelo que sobrou) com a página e o trecho. Peça também que confira nome, CRM/UF e RQE e o checklist CFM do `CLAUDE.md`.

Se houver diferença, corrija a cópia para que fique igual ao texto aprovado, exporte de novo e passe outra vez pelo `revisor`, no máximo duas vezes. O que continuar diferente vai para a entrega como pendência. Registre o resultado da revisão em `peca.md`.

### 5. Entrega para aprovação

Apresente ao Dr. Ícaro:

1. **Status:** rascunho para aprovação. Nada foi publicado, agendado, enviado nem compartilhado; o modelo original e o kit de marca não foram alterados.
2. **Link da cópia no Canva** e o caminho da pasta em `pecas/`.
3. **Arquivos exportados** e o que **não** pôde ser exportado, com o motivo.
4. **Resultado da revisão:** as diferenças apontadas pelo `revisor` e o que foi corrigido.
5. **Conferir antes de usar:** pendências, falta de nome, CRM/UF e RQE, temas com restrição do CFM ou da Anvisa e decisões do Dr. Ícaro.

Termine perguntando se aprova a peça ou o que quer ajustar. Qualquer alteração depois da aprovação exige nova aprovação. Commit e push dos arquivos de `pecas/` também só com aprovação.
