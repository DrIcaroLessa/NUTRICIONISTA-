---
name: criar-post
description: Produz o rascunho de um post para Instagram e YouTube Shorts a partir de um tema e do material de pesquisa fornecido pelo Dr. Ícaro, passando pelo pesquisador-cientifico, pelo curador-tendencias, pelo redator-marketing e pelo revisor. Só faz busca de artigos científicos, pelo pesquisador-cientifico; não pesquisa tendências e nunca publica, entregando sempre um rascunho para aprovação. Use quando o Dr. Ícaro pedir para criar um post, carrossel, Reels ou Shorts.
---

# Criar post

Esta skill transforma um tema e o material de pesquisa do Dr. Ícaro em um rascunho de post pronto para a aprovação dele. Ela coordena quatro subagentes: `pesquisador-cientifico`, `curador-tendencias`, `redator-marketing` e `revisor`.

## Regras fixas

1. **Buscas: só de artigos científicos, só pelo `pesquisador-cientifico`.** A busca de artigos científicos é uma etapa permitida do fluxo, feita somente pelo subagente `pesquisador-cientifico` e somente em bases científicas (PubMed/PMC, Cochrane, SciELO, LILACS, ClinicalTrials.gov e sites de periódicos e sociedades médicas). Continua proibido pesquisar tendências na web, abrir o Instagram ou usar o Chrome, seja pela skill, seja por qualquer subagente chamado por ela. A busca científica não substitui o material de tendências e formatos fornecido pelo Dr. Ícaro: se esse material faltar, peça-o antes de seguir.
2. **Entrada:** o tema do post e os dados compilados pelo Dr. Ícaro, colados na conversa ou em arquivos de `tendencias/`, mais o relatório de evidências (da etapa 1 ou o reaproveitado na etapa 0).
3. **Fluxo:** conferir a entrada → evidência científica → curador → redator → revisor → entrega (detalhes abaixo).
4. **Nunca publicar, agendar nem enviar nada**, em nenhum canal. O resultado final é sempre um rascunho para aprovação do Dr. Ícaro.
5. **Descartes aparecem no resultado final.** Tudo o que qualquer etapa descartar por conflito com as regras de publicidade médica do `CLAUDE.md` deve constar na entrega, com a etapa, o item, o motivo e a regra.

O `CLAUDE.md` da raiz é a fonte de verdade para tom de voz, personas, funil, serviços, regra do RQE e checklist CFM. As preferências de produção abaixo se somam a ele; em caso de conflito, vale o `CLAUDE.md`.

## Preferências de produção do Dr. Ícaro

**Plataformas:** Instagram e YouTube Shorts.

**Formatos:**
- **Carrossel** de 6 a 9 páginas.
- **Reels** de fala direta (o Dr. Ícaro falando para a câmera), de 30 a 60 segundos.
- **YouTube Shorts:** vídeo vertical curto. Use o mesmo roteiro do Reels nas duas plataformas.
- **Stories:** pouco usados; só quando o Dr. Ícaro pedir.

**Tom:**
- Tratar o público por "você".
- Sem emojis.
- Evitar qualquer palavra ou expressão que dê ideia de entrega de resultado (por exemplo: "resolver", "acabar com", "curar", "eliminar", "livre da dor", "volte a", "garantido", "definitivo"). Descreva a avaliação e o cuidado, nunca o desfecho.

**Sempre:**
- Legenda do post curta e objetiva.
- Legenda escrita no vídeo (texto na tela), para quem assiste sem som.
- Nome, CRM/UF e RQE em toda peça publicitária, como exige o `CLAUDE.md` (no último card do carrossel e no fim do vídeo ou na legenda).
- Chamada para ação **só quando o Dr. Ícaro pedir**. Ainda não há um padrão: quando for pedida, proponha opções neutras, sem urgência, e deixe a escolha com ele.

**Nunca:**
- Citar as fontes na legenda do post (elas ficam só no rascunho, para conferência).
- Mencionar as clínicas.
- Usar hashtags.
- Usar imagens genéricas (banco de imagens). Nas sugestões visuais, proponha imagens próprias do Dr. Ícaro, ultrassom, ilustrações da marca ou texto sobre o fundo da identidade visual.
- Fazer comparações com outros profissionais ou desmerecer colegas.

## Fluxo

### 0. Conferir a entrada

- Confirme o **tema** e o **formato** (carrossel, Reels/Shorts ou Stories). Se o formato não for dito, pergunte ou escolha o mais coerente com a curadoria e informe a escolha.
- Identifique o **material de tendências e formatos**: texto colado na conversa ou arquivos de `tendencias/` indicados pelo Dr. Ícaro. Se ele não indicar arquivos, liste os de `tendencias/` e pergunte quais usar.
- **Sem material de tendências e formatos, pare e peça.** Não o substitua pela busca científica, por outras buscas nem por conhecimento próprio.
- Se já existir em `tendencias/` um relatório de evidências sobre o mesmo tema (arquivos `AAAA-MM-DD-evidencias-assunto.md` ou levantamentos científicos anteriores), pergunte ao Dr. Ícaro se quer reaproveitá-lo ou fazer uma busca nova. Se ele escolher reaproveitar, pule a etapa 1 e use esse arquivo.
- Se o tema envolver PRP, BMA, hidrogel, mesoterapia ou terapias de infusão venosa, avise já nesta etapa que o Dr. Ícaro precisará confirmar o que pode ser divulgado.

### 1. Evidência científica (`pesquisador-cientifico`)

Chame o subagente `pesquisador-cientifico` com o tema, o formato e as afirmações clínicas que o post provavelmente vai fazer. Peça que ele:
- liste no relatório o que descartou por conflito com o `CLAUDE.md`;
- busque só em bases científicas, começando pelo PubMed, conforme as instruções dele;
- salve o relatório em `tendencias/AAAA-MM-DD-evidencias-assunto.md`;
- devolva o caminho do arquivo, o resumo para quem vai escrever (afirmações que podem e que não podem ser feitas, com a força de cada uma), os descartes por conflito com o `CLAUDE.md`, as bases que não puderam ser consultadas e os pontos de conferência.

Se o conector de PubMed não estiver ativo ou a busca falhar, **pare e avise o Dr. Ícaro**. Não siga sem fonte científica, a menos que ele indique um relatório de evidências já existente.

### 2. Curadoria (`curador-tendencias`)

Chame o subagente `curador-tendencias` com o tema e o material: os caminhos dos arquivos ou o texto colado pelo Dr. Ícaro e o caminho do relatório de evidências (da etapa 1 ou o reaproveitado na etapa 0), indicado como parte do material desta rodada. Peça que ele:
- trabalhe só com esse material, sem pesquisar;
- classifique as fontes científicas pelo nível de evidência e pelo desenho do estudo (e não por dados de engajamento), e descarte afirmações que exagerem o que a fonte diz;
- selecione as melhores fontes e formas para esse tema e esse formato;
- salve a seleção em `curadoria/`, conforme as instruções dele;
- devolva o caminho do arquivo, o resumo para quem vai escrever e os descartes.

Se o curador pedir informação que falta, leve a pergunta ao Dr. Ícaro e espere a resposta antes de seguir.

### 3. Redação (`redator-marketing`)

Chame o subagente `redator-marketing` com:
- o tema, o formato e as preferências de produção desta skill;
- o caminho do arquivo de curadoria gerado na etapa 2, para usar as fontes e formas escolhidas;
- o caminho do relatório de evidências (da etapa 1 ou o reaproveitado na etapa 0), com a instrução de só fazer afirmações clínicas que estejam em "Afirmações que podem ser feitas" ou na curadoria, sem citar fontes na legenda;
- a instrução de consultar `referencias/marketing.md` e informar a referência usada;
- a instrução de não salvar arquivo nesta etapa (a skill salva o pacote final).

Ele entrega 3 variações. Para carrossel, peça o texto de cada página e a sugestão visual de cada uma. Para Reels/Shorts, peça o roteiro com gancho, falas, texto na tela e duração estimada (30 a 60 segundos). Em ambos, a legenda curta do post.

### 4. Revisão (`revisor`)

Chame o subagente `revisor` com as 3 variações e peça que confira:
- erros, trechos confusos e inconsistências;
- o `CLAUDE.md`: tom de voz, regra do RQE, serviços, nome, CRM/UF e RQE e todo o checklist CFM;
- as preferências desta skill (sem emojis, sem hashtags, sem menção às clínicas, sem fontes na legenda, sem palavras de entrega de resultado, tamanho do carrossel e duração do vídeo);
- se as afirmações clínicas estão apoiadas nas fontes da curadoria e do relatório de evidências (passe os dois caminhos), sem exagerar o que elas dizem.

Se o revisor apontar problemas, devolva ao `redator-marketing` para corrigir e passe de novo pelo `revisor`, no máximo duas vezes. O que continuar sem solução vai para a entrega como pendência.

### 5. Entrega para aprovação

Salve o pacote em `rascunhos/AAAA-MM-DD-formato-tema.md` (por exemplo, `rascunhos/2026-10-25-carrossel-dor-neuropatica.md`). Nunca sobrescreva nem apague arquivos existentes; se o nome já existir, acrescente `-2`.

Apresente ao Dr. Ícaro, na conversa e no arquivo:

1. **Status:** rascunho para aprovação. Nada foi publicado, agendado nem enviado.
2. **As 3 variações** revisadas, cada uma com a abordagem em uma linha.
3. **Fontes usadas:** as que sustentam as afirmações, com link, referência ABNT e classificação (forte, média ou fraca), o relatório de evidências de `tendencias/` e o arquivo de `curadoria/` gerado. As bases que não puderam ser consultadas também aparecem aqui.
4. **Referências usadas:** seção, autor e obra de `referencias/marketing.md` e o conceito aplicado.
5. **Descartes por conflito com as regras de publicidade médica:** tudo o que foi descartado pelo `pesquisador-cientifico` (as seções "Afirmações que não podem ser feitas" e "Descartados por conflito com o CLAUDE.md" do relatório de evidências), pelo curador, pelo redator ou pelo revisor, com a etapa, o item, o motivo e a regra do `CLAUDE.md`. Se não houver, diga isso explicitamente.
6. **Resultado da revisão:** o que o revisor apontou e o que foi corrigido.
7. **Conferir antes de usar:** dúvidas, números a confirmar no original, temas com restrição do CFM ou da Anvisa e decisões pendentes do Dr. Ícaro.

Termine perguntando qual variação ele aprova ou o que quer ajustar. Qualquer alteração depois da aprovação exige nova aprovação. Commit e push do rascunho também só com aprovação.
