# Análise das contribuições dos testes e plano de ajustes — Estimador de CH

> Documento de trabalho. Processa as contribuições dos testes enviadas pela **Aline Amorim em 22/09/2026** e as transforma em plano de alterações.
> **Estado: fases 1 e 2 aplicadas em 23/09/2026 e fases 3 e 4 em 30/09/2026, todas antes da reunião com a Aline.** Onde a §5 tinha dúvida, valeu a proposta, e a reunião confirma. Faltam D3, F1 e F2, que dependem de insumo da equipe (ver fase 4).
> Última atualização: 2026-09-30.

Testaram o estimador: **Aline Amorim, Rutinelli, Mariella e Bruno**. Antes de enviar, a Aline reuniu-se com a **Vanessa Battestin** para validar as sugestões — é o que a coluna *Decisão* registra.

---

## 1. Resumo

Os testes geraram **32 ajustes**: 21 aprovados, 3 aprovados se forem viáveis, 6 a decidir e 2 para uma fase futura.

O plano aplica tudo só na **Opção A** (`estimador-carga-horaria-a.html`), em cinco fases — todos os textos revisados pela Aline são dessa versão, não da B. A fase 1 corrige dois bugs confirmados no navegador e não depende da reunião.

A tabela de parâmetros virou o **Quadro 3**: três tarefas novas, nova nota de rodapé e nenhuma mudança nos tempos que já existiam.

---

## 2. Ajustes sugeridos

Coluna *Decisão*: **Aprovado** (por Aline e Vanessa) · **Se viável** (aprovado se for tecnicamente possível) · **A decidir** (fica para a reunião) · **Futuro** (fora desta rodada).

### 2.1 Textos da página inicial

| # | Ajuste | Quem sugeriu | Decisão |
|---|---|---|---|
| T1 | Trocar itálico por negrito em todos os destaques | Aline | Aprovado |
| T2 | Título passa a "Estimador de Carga Horária de Curso MOOC EaD" | Aline | Aprovado |
| T3 | Abertura: "Quanto tempo o seu curso realmente demanda do estudante?", com parágrafo novo que cita a adaptação ao Ifes | Aline | Aprovado |
| T4 | Crédito reescrito, incluindo o desenvolvimento técnico de Elton Vinicius Silva e Marcos Vinicius Forecchi Accioly | Aline | Aprovado |
| T5 | "Ninguém ensina o professor a estimar isso" vira "Estimar a carga horária não deveria depender de intuição", com três parágrafos novos | Aline | Aprovado |
| T6 | "Três momentos": CH pretendida com limite de 60 h, em vez de 20, 40 ou 60 h; o momento 2 destaca o cálculo automático | Aline | Aprovado |
| T7 | Juntar "Parâmetros com base em evidências" e "De onde vêm esses números" em "Parâmetros fundamentados em revisão de literatura, não em intuição" | Aline, Rutinelli | Aprovado |
| T8 | Bloco novo "Uma estimativa, não uma medida exata", nascido de uma dúvida do Bruno; falta decidir onde fica | Aline | Aprovado |

O texto integral de T2 a T8 está no **Anexo A**.

### 2.2 Tipos de atividade e parâmetros

| # | Ajuste | Quem sugeriu | Decisão |
|---|---|---|---|
| B1 | Aquisição › Outros: mapa mental, slides, imagem, infográfico, H5P de conteúdo, com tempo informado pelo professor | Aline | Aprovado |
| B2 | Prática › Enquete/Escolha, para coletar impressões sem avaliar; a tabela fixa 15 min, mas o texto do teste sugere 2 min por questão | Aline | Aprovado |
| B3 | Prática › Outras práticas (atualizar perfil, simulação em sala de prática), com tempo informado pelo professor | Aline | Aprovado |
| B4 | Tabela da página inicial: nova descrição de Artefatos, nova nota de rodapé e asterisco em Discussão | Aline | Aprovado |
| B5 | Retirar a trava "Curso MOOC: autoinstrucional: exclui colaboração e atividades síncronas ou presenciais" e orientar em vez de restringir | Aline | Aprovado |
| B6 | Explicar de onde vem o fator "3x a duração" do vídeo de complexidade alta | Rutinelli | A decidir |

### 2.3 Preenchimento das atividades

| # | Ajuste | Quem sugeriu | Decisão |
|---|---|---|---|
| C1 | Impedir que uma atividade seja salva com 0 palavras ou 0 minutos | Aline | Aprovado |
| C2 | Tirar as setas dos campos numéricos e corrigir o salto da página ao clicar no campo | Bruno | Aprovado |
| C3 | Alertar quando um vídeo passar de 20 min ou uma leitura passar de 1 h (limites definidos com a Vanessa; não há limite inferior) | Bruno | Aprovado |
| C4 | O professor escolhe a ação ("Assistir a um vídeo") e a ferramenta deduz o tipo de aprendizagem | Rutinelli | A decidir |
| C5 | Modo rápido, com menos etapas, para professores experientes em EaD | Rutinelli | A decidir |

### 2.4 Resultado e relatórios

| # | Ajuste | Quem sugeriu | Decisão |
|---|---|---|---|
| D1 | Veredito: com o estimado abaixo da meta aparece "curso subestimado"; deve dizer "superestimado" | Aline | Aprovado |
| D2 | Trocar a cor de Prática nos gráficos: o tom ferrugem é lido como vermelho de alerta | Aline | Aprovado |
| D3 | Separar o tempo em consumo de conteúdo, prática e avaliação | Bruno | Se viável |
| D4 | Mostrar o que mais pesa no resultado; a Aline entendeu como gráfico por categoria e por tipo de aprendizagem, como no mapa de aprendizagem | Bruno | Se viável |
| D5 | Exportar a análise do curso em PDF, além do arquivo JSON | Aline | Se viável |
| D6 | Faixa de tempo mínimo, provável e máximo em vez de um valor único | Bruno | A decidir |

### 2.5 Orientação ao professor

| # | Ajuste | Quem sugeriu | Decisão |
|---|---|---|---|
| E1 | Subir o quadro "Ainda não tenho o material pronto: como estimo?", que hoje desce conforme o painel de resultados cresce | Aline | Aprovado |
| E2 | Orientar sobre materiais mistos (livro ou página do Moodle com vídeo e links embutidos): lançar leitura e vídeo separados | Aline | A decidir |
| E3 | Avisar que materiais complementares não entram no cálculo, com texto pronto e decisão tomada com a Vanessa; a Aline prefere o aviso dentro do estimador | Mariella | Aprovado |

Texto aprovado para E3: *"Os materiais complementares não devem ser incluídos no cômputo da carga horária do curso. Eles são opcionais para o aluno, e seu conteúdo não pode ser cobrado nas avaliações."*

### 2.6 Exemplos, suporte e evolução

| # | Ajuste | Quem sugeriu | Decisão |
|---|---|---|---|
| F1 | Trocar os cursos de exemplo, que fecham exatamente na meta, por cursos reais; no de 60 h, as boas-vindas de 10 min contam 3x | Bruno | A decidir |
| F2 | Formulário "Dúvidas e dificuldades" com link na ferramenta; título, descrição e perguntas prontos, caixa de e-mail a definir | Aline | Aprovado |
| F3 | Validar as estimativas com o tempo real dos estudantes | Bruno | Futuro |
| F4 | Marcar um recurso como "extra/opcional", registrado mas fora da soma (vale se a ferramenta virar analisador) | Mariella | Futuro |

Perguntas prontas do formulário (F2): nome; e-mail; em que etapa encontrou a dificuldade (entendendo os tipos de atividade · preenchendo os campos de uma atividade · interpretando o resultado final · navegação ou funcionamento geral · outro); descreva a dificuldade; quer anexar um print da tela.

---

## 3. Atualizações na tabela de parâmetros (Quadro 2 → Quadro 3)

As quatro primeiras linhas estão em vermelho no documento de parâmetros; as outras cinco apareceram na comparação com a versão de junho guardada em `docs/COMO ESTIMAR A CARGA HORÁRIA…IFES.md`. **Nenhum tempo das tarefas que já existiam mudou.**

| Item | Antes (Quadro 2, junho) | Agora (Quadro 3) | Efeito no estimador |
|---|---|---|---|
| Aquisição › Outros | Não existia | Conteúdo interativo em H5P, mapas mentais, slides, imagens, infográficos; tempo definido pelo professor | Tarefa nova com tempo informado à mão |
| Prática › Enquete/Escolha | Não existia | Escolhas simples, coleta de impressões, pesquisa de opinião ou avaliação do curso; complexidade baixa; 15 min | Tarefa nova de tempo fixo: 15 min por enquete |
| Prática › Outras práticas | Não existia | Práticas fora das categorias anteriores, como exercícios em ambiente de prática; tempo definido pelo professor | Tarefa nova com tempo informado à mão |
| Produção › Artefatos | "Artefatos em geral como mídias, apresentações, planos de aula, projetos, etc." | Acrescenta "produtos de qualquer tipo que não sejam produção textual (escrita)" | Novo rótulo da tarefa |
| Nota de rodapé (*) | MOOC sem colaboração nem síncrona; as duas só em pesquisa com planejamento híbrido | MOOC admite discussão e colaboração não avaliativas; síncrona ou presencial só no planejamento híbrido de pesquisa | Muda a regra do modo MOOC (B5) e o texto sob a tabela |
| Discussão | Sem asterisco | Com asterisco | A nota passa a valer para Discussão |
| Síncrona › Complexidade | Em branco | "Duração do evento" | Só o texto da tabela |
| Título | "Quadro 2. Valores para calculadora de carga horária para cursos MOOC" | "Quadro 3 - Valores para estimativa de carga horária adaptado para cursos MOOC do Ifes" | A página cita "o Quadro 2 acima"; o texto novo de T7 já não cita número |
| Fonte | McInnes et al. (2026), Liu e Evans (2020) e Beer (2019) | As mesmas, "e adaptações realizadas para o contexto dos MOOCs no Ifes" | Nenhum: a página não exibe essa legenda |

Nota de rodapé nova, na íntegra: *"No Ifes, os MOOCs são totalmente assíncronos, sem tutoria, com atividades avaliativas autoinstrucionais. Admitem-se atividades de discussão ou colaborativas, desde que não sejam avaliativas. Quando o curso integra uma pesquisa em contexto restrito, admite-se também um planejamento híbrido, nesse caso, atividades síncronas/presenciais podem ser consideradas no cálculo da carga horária."*

O documento de parâmetros também mudou de nome, para "Como Calcular a Carga Horária de Cursos a Distância: Estimador para MOOCs do Ifes". O link da página, inclusive no texto novo de T7, ainda usa o nome antigo.

---

## 4. Plano de alterações

Tudo na Opção A (`estimador-carga-horaria-a.html`). Das 32 sugestões, 27 entram nas fases 1 a 4 e 5 ficam para depois.

**Dependências entre as fases:**

- **Fase 1 (correções)** — não depende de nada, pode começar já.
- **Fase 0 (decisões com a Aline)** — destrava as fases 2, 3 e 4.
- **Fases 2, 3 e 4** — rodam depois da reunião; entre si, são independentes.
- **Fecho** — revisão da Aline e publicação.

*Esforço:* **P** = ajuste localizado · **M** = mexe em várias partes da página.

### Fase 0: decisões com a Aline

Responder as dúvidas da §5, sem mexer em código. As três que travam mais trabalho: confirmar a Opção A como versão única, liberar também a atividade síncrona (B5) e conseguir os dados de um curso real (F1).

### Fase 1: correções

> **Feita em 23/09/2026** na Opção A. A versão testada ficou salva em `arquivo/estimador-carga-horaria-a-2026-09-22.html` e na tag git `estimador-a-2026-09-22`. D2: Prática passou de ferrugem para oliva (`#4C5800`), validada no script de paleta — detalhes em `docs/DESIGN.md`. D1 foi aplicada com a proposta da §5 (os dois lados trocam juntos); confirmar na reunião.

Os dois bugs foram confirmados no estimador publicado em 22/09/2026. Digitar `1200` no campo de palavras deixa só `1`, porque o campo perde o foco a cada tecla — o handler `input` de `#modal-activity-body` chama `renderModalBody()`, que recria o campo. E o botão de adicionar já fica ativo com o campo vazio, gravando a atividade com 0 min.

| Item | O que fazer | Onde no código | Esforço |
|---|---|---|---|
| C2 | Parar de redesenhar o modal a cada tecla: atualizar só a prévia do tempo e o botão. Trocar os campos numéricos por texto com teclado numérico, sem setas, aceitando vírgula (7,5 min) | handler `input` de `#modal-activity-body`, `renderParamFields`, `#target-input` | M |
| C1 | Exigir quantidade maior que zero (palavras, minutos, questões ou horas) para adicionar, com aviso junto ao campo | `draftValid`, `renderParamFields` | P |
| D1 | Rotular pelo lado da carga declarada: abaixo da meta, "carga horária superestimada"; acima, "subestimada" | `statusForDelta` | P |
| D2 | Nova cor para Prática, fora da faixa vermelho-laranja, com contraste AA e distinta das outras seis | token `--cat-2` | P |

### Fase 2: Quadro 3 e tipos de atividade

> **Feita em 23/09/2026** na Opção A, antes da reunião, com as propostas da §5 para B2 (15 min fixos), B5 (os sete tipos liberados, síncrona inclusive, com aviso), B6 (vídeo e atividade interativa só com "Baixa" e "Alta") e H5P (de conteúdo em Aquisição › Outros materiais; com resposta em Prática › Atividade interativa); confirmar na reunião. Também seguem o Quadro 3: as descrições de escrita média e alta, "Alta" e "2x uma produção individual" na linha de Colaboração, e "Definida pelo professor" no lugar de "Não definido" nas tarefas sem parâmetro. Na nota de rodapé, a vírgula antes de "nesse caso" virou ponto e vírgula.

| Item | O que fazer | Onde no código | Esforço |
|---|---|---|---|
| B1 | Tarefa "Outros materiais" em Aquisição, com tempo informado à mão | `TYPES` (aquisicao) | P |
| B2 | Tarefa "Enquete ou escolha" em Prática: 15 min por enquete | `TYPES` (pratica) | P |
| B3 | Tarefa "Outras práticas" em Prática, com tempo informado à mão | `TYPES` (pratica) | P |
| B4 | Tabela da página inicial igual ao Quadro 3: rótulo de Artefatos, asterisco em Discussão, nota de rodapé nova, "Duração do evento" na síncrona | `renderTaxTable`, `.tax-foot` | P |
| B5 | Tirar a chave "Curso MOOC": os sete tipos sempre disponíveis, com aviso no modal (discussão e colaboração não avaliativas; síncrona só em pesquisa híbrida). | `#mooc-toggle` e seu handler, `readMoocMode`, `TEMPLATES` | M |
| B6 | Mostrar no modal a fonte de cada tempo. Trocar as dicas de vídeo e de atividade interativa, escritas por nós e ausentes do Quadro, pelas que a Aline validar | `TYPES` (campo `hint`), `renderModalBody` | P |

### Fase 3: textos e orientação

> **Feita em 30/09/2026** na Opção A, com os textos do Anexo A. Seguiram a proposta da §5: T7 com o nome novo do documento no link, T8 na página inicial (faixa entre Laurillard e os créditos) mais a linha "Tempo médio esperado, não uma medida exata" sob o resultado, e E2 como item do quadro de ajuda, redigido a partir das observações da Aline sobre livros e páginas do Moodle. T1 tirou a Instrument Serif da página: o destaque agora é `<strong>` na própria Inter Tight. Em T5, o travessão do texto da Aline virou dois-pontos, como no resto da página. E3 fica sempre à vista, abaixo do quadro de ajuda, em vez de dentro do item recolhível.

| Item | O que fazer | Onde no código | Esforço |
|---|---|---|---|
| T1 | Trocar `<em>` por `<strong>` e ajustar o estilo, que hoje usa itálico como voz de destaque | CSS `em`, `#view-home` | P |
| T2 a T7 | Aplicar os textos do Anexo A, fundir as duas seções de metodologia e incluir o desenvolvimento técnico no crédito | `#view-home`, `.brand-title`, `.byline-block` | M |
| T8 | Bloco "Uma estimativa, não uma medida exata" na página inicial e uma linha sob o resultado, com link para ele | `#view-home`, `.results-card` | P |
| E1 | Levar "Ainda não tenho o material pronto" para o topo da coluna da lista, fora do painel que cresce | `.support-wrap` | P |
| E2 | Item sobre materiais mistos no mesmo quadro, se aprovado | `.support-wrap` | P |
| E3 | Aviso sobre materiais complementares, com o texto da Aline e da Vanessa | `.support-wrap` | P |

### Fase 4: recursos novos

> **Parcialmente feita em 30/09/2026** na Opção A: C3, D4 (só a lista das cinco atividades que mais pesam; o gráfico individual × social espera a confirmação da §5) e D5 (botão "PDF" na barra, versão de impressão com curso, meta, data, resultado, gráficos e lista). Também entrou a proposta de T6: o campo de meta continua livre e mostra um aviso acima de 60 h. O alerta de C3 diz só que o valor está "acima do esperado" e pede para conferir; não sugere dividir o material, porque isso não está nas fontes. **Faltam:** D3 (depende de definir o que conta como avaliação), F1 (depende dos dados de um curso real) e F2 (depende do formulário e do e-mail que o recebe).

| Item | O que fazer | Onde no código | Esforço |
|---|---|---|---|
| C3 | Alerta que não bloqueia: vídeo com mais de 20 min de duração ou leitura com mais de 1 h estimada, no modal e na lista | `renderModalBody`, `activityRowHtml` | M |
| D5 | Botão "Salvar em PDF": versão de impressão com curso, meta, total, veredito, gráficos e lista de atividades, sem biblioteca nova | CSS `@media print`, `window.print()` | M |
| D4 | Lista das atividades que mais pesam (as 5 maiores, com % do total) e, se confirmado, gráfico individual × social | `renderResults` | M |
| D3 | Separar conteúdo, prática e avaliação, depois de definido o que conta como avaliação | `TYPES` ou campo novo no modal, `renderResults` | M |
| F1 | Trocar os exemplos sintéticos por um curso real, com o total que ele der. Refazer a figura da abertura, que também fecha em 20 h exatas | `TEMPLATES`, `renderMeasure` | M |
| F2 | Link "Relatar dúvida ou problema" no rodapé e na barra da ferramenta | `.site-footer`, `.toolbar` | P |

### Fase 5: fica para depois

- **C4, ação primeiro:** viável como uma lista única de ações ("Ler um texto", "Assistir a um vídeo") com o tipo deduzido. Muda o modal validado em 26/08, então só com aval da Aline.
- **C5, modo rápido:** reavaliar depois da correção C2 e dos relatos do formulário.
- **D6, faixa de tempo:** não recomendado. O Quadro dá um valor por tarefa, e inventar mínimo e máximo fere a regra de não criar parâmetros; T8 responde à dúvida.
- **F3 e F4:** dependem de pesquisa futura e de a ferramenta virar analisador.

### Verificação ao fim de cada fase

Testar no navegador: digitação nos campos, cada tarefa nova, os vereditos, a abertura de um JSON antigo e a impressão. Depois, publicar para a Aline revisar e atualizar o `README.md` e o `docs/ESTADO-E-PROXIMOS-PASSOS.md`.

---

## 5. Dúvidas para a reunião com a Aline

Em ordem de impacto; os três primeiros destravam a maior parte das fases 2 a 4.

| Item | Pergunta | Proposta |
|---|---|---|
| Versão | Os textos revisados são todos da Opção A. Ela vira a versão única? | Sim; arquivar a Opção B |
| B5 | Sem a trava, a atividade síncrona também fica livre? A nota nova ainda a restringe ao planejamento híbrido de pesquisa | Liberar os sete tipos, com aviso no modal |
| F1 | Os quatro exemplos foram montados no desenvolvimento e fecham exatamente na meta; o de 60 h tem 122 atividades. Podemos usar o MOOC do teste 1 da Aline como exemplo real? | Sim, com o total real e os dados cedidos pela Aline |
| B2 | Enquete vale 15 min fixos, como na tabela, ou 2 min por questão, como no texto do teste? | 15 min, como na tabela |
| D1 | Acima da meta, o rótulo passa a "carga horária subestimada"? | Sim, os dois lados trocam juntos |
| C3 | "20 min de vídeo" é a duração da mídia? "1 h de leitura" é o tempo estimado? Há limite para valores baixos? | Duração da mídia; tempo estimado; sem limite inferior |
| T6 | O limite de 60 h vale também no campo de meta da ferramenta? | Manter o campo livre e avisar acima de 60 h, porque a ferramenta também serve a disciplinas |
| B6 | Que descrição usar para vídeo e atividade interativa de complexidade baixa e alta? Qual a fonte do fator 3x? | Até a Aline indicar, mostrar só "Baixa" e "Alta", com a fonte do Quadro |
| H5P | H5P aparece em Aquisição › Outros e em Prática › Atividade interativa. Qual o critério? | H5P que só apresenta conteúdo é aquisição; o que pede resposta com feedback é prática |
| D3 | O que conta como avaliação: um campo "atividade avaliativa" no modal ou uma regra por tipo? | Campo opcional no modal, desmarcado por padrão |
| D4 | O estimador já mostra o equilíbrio pelos sete tipos. Que outra visão o mapa de aprendizagem usa? | Individual × social, mais a lista das atividades que mais pesam |
| T8 | Onde fica "Uma estimativa, não uma medida exata"? | Na página inicial, com uma linha sob o resultado |
| E2 | Entra no quadro de ajuda a orientação sobre materiais mistos? | Sim, em um item curto |
| F2 | Quem cria o formulário e que e-mail recebe: a Aline por um tempo ou a CGTE? No Google Forms, anexar arquivo exige login com conta Google | Aline e Vanessa decidem; print opcional e "Estimador" no título, no lugar de "Calculadora" |
| C4, C5, D6 | Ação primeiro, modo rápido e faixa de tempo ficam para depois? | Sim; C4 volta à pauta com os relatos do formulário |
| T7 | O link da proposta ainda usa o nome antigo do documento. Atualizar? | Usar o nome novo |
| Rutinelli | A lista dela pula da sugestão 2 para a 4. Faltou a 3? | Confirmar com a Rutinelli |

---

## 6. Anexo A — textos integrais da página inicial

Transcritos do documento da Aline, prontos para colar. "Hoje" é o que está no ar na Opção A.

### T2 — Título

- **Hoje:** Estimador de Carga Horária de Curso EaD
- **Novo:** Estimador de Carga Horária de Curso MOOC EaD

### T3 — Abertura

- **Hoje:** Quanto tempo o seu curso *realmente* pede do estudante? / Planejar um curso a distância não vem com nenhum parâmetro de quanto tempo cada recurso exige do estudante. Esta ferramenta usa literatura internacional sobre carga de estudo online para dar esse parâmetro, atividade por atividade.
- **Novo:**

> **Quanto tempo o seu curso realmente demanda do estudante?**
>
> Planejar um curso a distância não costuma vir com parâmetros claros de quanto tempo cada atividade exige do estudante. Esta ferramenta traz essa referência, atividade por atividade, a partir de literatura internacional sobre carga de estudo em cursos on-line, adaptada ao contexto do Ifes.

### T4 — Crédito da pesquisa

- **Hoje:** Uma proposta de carga horária baseada em evidências, da pesquisa de doutorado de Aline Pinto Amorim (Ifes/Cefor) em design de aprendizagem para MOOCs, com orientação de Vanessa Battestin e coorientação de Marize Lyra Silva Passos.
- **Novo:**

> O Estimador foi baseado na pesquisa de doutorado de Aline Pinto Amorim, em Design de Aprendizagem de MOOCs, com orientação de Vanessa Battestin e coorientação de Marize Lyra Silva Passos. O desenvolvimento técnico foi realizado por Elton Vinicius Silva e Marcos Vinicius Forecchi Accioly.

Nomes completos corrigidos em 30/09/2026; o texto da Aline trazia "Elton Silva e Marcos Accioly".

### T5 — Seção do problema

- **Hoje:** "Ninguém ensina o professor a estimar isso", com três parágrafos.
- **Novo:**

> **Estimar a carga horária não deveria depender de intuição**
>
> Ao propor um curso a distância, o professor já precisa declarar de antemão quantas horas o curso terá. Mas no planejamento raramente existe uma referência que traduza "quantos vídeos, textos e atividades" em "quantas horas de estudo" — a decisão fica por conta da intuição.
>
> O resultado, segundo relatos levantados na pesquisa: cursos que ultrapassam muito a carga prevista, estudantes que reclamam do volume de trabalho, e nenhuma forma objetiva de saber se a reclamação é falta de dedicação ou planejamento superestimado.
>
> Esta ferramenta nasce para preencher essa lacuna: ela usa literatura internacional sobre carga de trabalho discente (student workload) para estimar, atividade por atividade, o tempo que o curso realmente vai demandar do estudante, antes mesmo de ele ser produzido.

### T6 — Três momentos

- **Hoje:** "Três momentos em que a ferramenta entra no seu processo"; no momento 1, "o professor já escolhe entre 20, 40 ou 60 horas".
- **Novo:**

> **Três momentos em que a ferramenta apoia o seu processo de elaboração de curso MOOC:**
>
> **1 — Abertura do processo**
> Ao submeter a proposta do curso, o professor já escolhe a carga horária pretendida, com limite de 60 horas. É a primeira decisão, ainda sem detalhe de conteúdo.
>
> **2 — Planejamento do curso (etapa design)**
> Ao elaborar o mapa de aprendizagem, o professor usa o estimador atividade por atividade: escolhe o tipo e a complexidade, e a ferramenta calcula o tempo automaticamente a partir dos parâmetros de cada atividade. O professor acompanha em tempo real o somatório da carga horária estimada. É o uso principal da ferramenta.
>
> **3 — Sala pronta (conferência final)**
> Depois de produzir o material, o professor pode reestimar com os números reais (duração final dos vídeos, tamanho real dos textos) para conferir se a carga horária ficou coerente com o previsto.

### T7 — Metodologia (funde os dois blocos atuais)

- **Hoje:** duas seções separadas, "Parâmetros com base em evidências, não em intuição" (acima da tabela) e "De onde vêm esses números" (mais abaixo).
- **Novo:** um bloco só.

> **Parâmetros fundamentados em revisão de literatura, não em intuição**
>
> Os parâmetros seguem a classificação em tipos de aprendizagem do Conversational Framework de Laurillard (2012): aquisição, prática, produção, discussão, investigação e colaboração. Eles foram reunidos a partir de trabalhos sobre carga de trabalho discente (student workload) em cursos on-line, localizados no Portal de Periódicos da CAPES e no Google Acadêmico, e adaptados ao contexto de planejamento de MOOCs no Ifes.
>
> O resumo com a proposta do estimador pode ser lido em [Como estimar a carga horária de cursos a distância: proposta de calculadora para cursos MOOCs do Ifes](https://docs.google.com/document/d/1ViAMjrAfjyjWvYBa8hL8yW91ot-4sRiotCTge_UJd9M/edit?usp=sharing). Um artigo completo está em preparação para submissão; assim que publicado, a referência definitiva substitui este link.

### T8 — Bloco novo (local a definir)

> **Uma estimativa, não uma medida exata**
>
> O Estimador calcula um tempo médio esperado, e não um tempo exato que cada aluno vai gastar. É como o tempo de uma receita ou de um trajeto no GPS: dá uma referência confiável para planejar, mas cada pessoa pode levar um pouco mais ou um pouco menos, dependendo do seu ritmo e conhecimento prévio. Use o resultado para verificar se a carga horária proposta é realista, não como uma medida exata do tempo de cada estudante.

Observação da Aline: *"Acrescentei porque parece óbvio, mas o Bruno teve essa dúvida… então melhor explicar. Tive dúvida se é melhor na página inicial ou dentro do estimador."*

---

## 7. Fontes

- **Análise estimador de CH — Contribuições gerais**, da Aline Amorim, recebida em 22/09/2026: [Google Doc](https://docs.google.com/document/d/16S2MGkuWqpIATyqqslWhwucHZaw1GKwF3LFDa2_OOTE/edit?usp=sharing). Lida pela cópia `.docx` na raiz do repositório; os comentários dela estão no próprio texto, em vermelho e azul.
- **Como Calcular a Carga Horária de Cursos a Distância: Estimador para MOOCs do Ifes**, com o Quadro 3, alterado em 22/09/2026: [Google Doc](https://docs.google.com/document/d/1ViAMjrAfjyjWvYBa8hL8yW91ot-4sRiotCTge_UJd9M/edit?tab=t.0).
- **Quadro 2 de junho**, em `docs/COMO ESTIMAR A CARGA HORÁRIA…IFES.md`, usado na comparação da §3.
- **Estimador publicado, Opção A**: <https://vertumno.github.io/calculadora-ch-cursos-ead/estimador-carga-horaria-a.html> — testado em 22/09/2026 para confirmar os bugs da fase 1 e os totais dos exemplos.
