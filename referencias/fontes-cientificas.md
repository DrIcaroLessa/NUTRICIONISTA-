# Fontes científicas: bases e periódicos

Lista de onde o subagente `pesquisador-cientifico` busca evidência científica. Adaptada da skill `busca-artigos-cientificos` do Dr. Ícaro (arquivo `references/fontes.md`), que fica na conta dele, fora deste repositório. Mudanças feitas lá não chegam aqui automaticamente: atualize este arquivo quando necessário.

Para uma dúvida rápida, PubMed e PMC bastam. Para um levantamento mais amplo, consulte também as demais bases e os periódicos da especialidade do tema.

Legenda de acesso:
- **[aberto]**: conteúdo completo, ou pelo menos o abstract, acessível publicamente por WebSearch ou WebFetch.
- **[aberto para o resumo]**: o resumo ou abstract é público, mas o texto completo geralmente é pago.
- **[pago/institucional]**: geralmente atrás de assinatura ou login. O subagente não tem acesso: registre a base como "não acessada" e não finja cobertura. Se o Dr. Ícaro tiver acesso institucional, ele pode colar os resultados ou DOIs para síntese.

Observação: em algumas sessões na nuvem, o WebFetch não abre páginas. Nesse caso, as bases que dependem dele ficam como "não consultadas" no relatório.

## Bases bibliográficas gerais

- **PubMed/MEDLINE** [aberto]: base principal, sempre buscar primeiro, com `mcp__PubMed__search_articles` (termos MeSH quando possível) e `mcp__PubMed__get_article_metadata` para conferir os dados de cada artigo.
- **Embase** [pago/institucional]: cobertura mais ampla que o PubMed, forte em farmacologia e estudos europeus.
- **Scopus** [pago/institucional]: multidisciplinar, útil para análise de citações.
- **Web of Science** [pago/institucional]: idem Scopus.

## Evidência sintetizada e revisões sistemáticas

- **Cochrane Library** (cochranelibrary.com) [aberto para o resumo]: revisões sistemáticas e metanálises. O resumo em linguagem simples costuma trazer a conclusão mesmo quando o texto completo é pago. Muitas revisões Cochrane também estão indexadas no PubMed.
- **TRIP Database** (tripdatabase.com) [aberto]: busca focada em medicina baseada em evidência; boa para achar diretrizes.
- **UpToDate** [pago/institucional]: resumo clínico; o conteúdo integral exige login.
- **DynaMed** [pago/institucional]: mesma limitação do UpToDate.

## Registros de ensaios clínicos e de revisões

- **ClinicalTrials.gov** [aberto]: ensaios em andamento e protocolos registrados de ensaios já publicados.
- **PROSPERO** (crd.york.ac.uk/prospero) [aberto]: protocolos de revisões sistemáticas; conferir antes de dizer que "falta evidência" sobre o tema.

## Repositórios de acesso aberto

- **PMC (PubMed Central)** [aberto]: texto completo com `mcp__PubMed__get_full_text_article` quando houver PMCID. O texto pode vir vazio; nesse caso, sintetizar a partir do abstract e sinalizar.
- **SciELO** (scielo.br / scielo.org) [aberto]: produção latino-americana e brasileira; buscar em português e com o termo técnico em inglês.
- **LILACS** (lilacs.bvsalud.org) [aberto]: literatura da América Latina e do Caribe em ciências da saúde; complementa o SciELO.

## Periódicos por especialidade

Buscar primeiro pelo PubMed (a maioria está indexada). Usar WebSearch no site do periódico ou da sociedade só para algo muito recente ainda não indexado ou para diretrizes e posicionamentos.

**Ortopedia e Traumatologia**
- Revista Brasileira de Ortopedia (RBO), SBOT [aberto, via SciELO]
- Journal of Bone and Joint Surgery (JBJS) [pago/institucional]
- The Bone & Joint Journal, BOA [pago/institucional]
- Clinical Orthopaedics and Related Research (CORR) [pago/institucional]
- Knee Surgery, Sports Traumatology, Arthroscopy, ESSKA [pago/institucional]
- Arthroscopy, AANA [pago/institucional]

**Medicina da Dor**
- BrJP (Brazilian Journal of Pain), SBED [aberto, via SciELO]
- Pain, IASP [pago/institucional]
- Pain Medicine, American Academy of Pain Medicine [pago/institucional]
- Regional Anesthesia and Pain Medicine (RAPM), ASRA [pago/institucional]
- Pain Physician, ASIPP [aberto, a maioria dos artigos]
- European Journal of Pain, EFIC [pago/institucional]

**Anestesiologia**
- Brazilian Journal of Anesthesiology, SBA [aberto, via SciELO]
- Anesthesiology, ASA [pago/institucional]
- Anesthesia & Analgesia, IARS [pago/institucional]
- British Journal of Anaesthesia (BJA) [pago/institucional]
- Anaesthesia, Association of Anaesthetists (Reino Unido) [pago/institucional]

**Radiologia**
- Radiologia Brasileira, CBR [aberto, via SciELO]
- Radiology, RSNA [pago/institucional]
- American Journal of Roentgenology (AJR), ARRS [pago/institucional]
- European Radiology, ESR [pago/institucional]
- Journal of the American College of Radiology (JACR), ACR [pago/institucional]
- Skeletal Radiology, ISS [pago/institucional]

**Medicina Regenerativa e Terapia Celular**

Atenção: temas como PRP e BMA têm restrições do CFM e da Anvisa sobre indicação e divulgação. O relatório deve avisar que o Dr. Ícaro precisa confirmar o que pode ser divulgado.

- Cytotherapy, ISCT [pago/institucional]
- Journal of Orthopaedic Research, ORS [pago/institucional]
- Stem Cells Translational Medicine [aberto]
- Regenerative Medicine [pago/institucional]
- American Journal of Sports Medicine (AJSM): forte em PRP e biológicos; ver em Medicina do Esporte
- PM&R, Academy of Physical Medicine and Rehabilitation [pago/institucional]
- ABMR (abmr.med.br/artigos): não é periódico; é uma curadoria com links para DOI e PMC. Serve como ponto de partida, mas sempre seguir até a fonte primária antes de citar.

**Medicina do Esporte**
- Revista Brasileira de Medicina do Esporte (RBME), SBMEE [aberto, via SciELO]
- British Journal of Sports Medicine (BJSM) [pago/institucional, alguns artigos abertos]
- American Journal of Sports Medicine (AJSM), AOSSM [pago/institucional]: também forte em PRP e biológicos
- Sports Medicine [pago/institucional]
- Clinical Journal of Sport Medicine, AMSSM/CASEM [pago/institucional]
- Journal of Science and Medicine in Sport, Sports Medicine Australia [pago/institucional]
- Scandinavian Journal of Medicine & Science in Sports [pago/institucional]
- Arthroscopy, Sports Medicine, and Rehabilitation, AANA [aberto]
- Orthopaedic Journal of Sports Medicine (OJSM), AOSSM [aberto]
