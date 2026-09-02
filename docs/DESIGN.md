# DESIGN.md — Estimador de Carga Horária

Sistema visual de `estimador-carga-horaria-a.html`. Arquivo único, sem build.
Toda cor passa por token; nenhum literal de cor vive fora do bloco `:root`.

---

## Tese

Um estimador é um **instrumento de medição**, não uma landing page de SaaS.
A página lê como referência de pesquisa: tabelas reais, fios, uma cor de sinal.
Recusa explícita a *kicker*/*eyebrow*, trilhos coloridos em card e ao template
"número gigante + rótulo pequeno + estatísticas de apoio".

## Tema: claro, único, comprometido — e colorido

Não há modo escuro, nem `prefers-color-scheme`, nem `data-theme`. A decisão é
da cena de uso — professor planejando um curso numa mesa iluminada.

Mas também não é preto sobre branco. O chão é um branco puxado para o verde, a
tinta carrega matiz em vez de tender ao preto, e **cor é taxonomia**: cada tipo
de atividade tem uma família própria, usada em todo lugar onde aquele tipo
aparece. Não existe matiz decorativa na página.

Consequência técnica: `body` pinta `background` a partir de token e **toda** cor
é declarada explicitamente, para a página se sustentar sobre qualquer fundo do
hospedeiro (o artifact compõe sobre um fundo pintado pelo visualizador).

---

## Cor

### Fundos

| Token | Valor | Onde |
|---|---|---|
| `--paper` | `#F6F9F4` | chão da página — branco com viés verde, nunca branco puro |
| `--surface` | `#FFFFFF` | painéis e linhas de atividade |
| `--surface-quiet` | `#E9F1E6` | faixas de seção, cabeçalho de tabela |
| `--well` | `#D9E4D6` | poço neutro do medidor |
| `--row-hover` | `#F2F7F0` | linha de atividade sob o cursor |

### Fios

| Token | Valor | Papel |
|---|---|---|
| `--border` | `rgba(40,54,47,0.22)` | separador interno |
| `--border-strong` | `rgba(40,54,47,0.55)` | contorno de controle — **3.2:1** |
| `--rule` | `rgba(31,112,39,0.85)` | régua de seção — verde, não preta |

### Tinta — com matiz, contraste medido sobre branco

| Token | Valor | Razão | Uso |
|---|---|---|---|
| `--ink` | `#28362F` | 12.7:1 | títulos, números de leitura |
| `--ink-soft` | `#3D4A44` | 9.3:1 | corpo longo, micro-rótulos em caixa alta |
| `--muted` | `#5A6660` | 6.0:1 | texto secundário |
| `--muted-2` | `#5F6B65` | 5.6:1 (4.8:1 na faixa) | legendas, placeholder |

A tinta principal saiu de `#0E1114` (18.9:1, quase preto) para `#28362F`
(12.7:1, verde-ardósia). Continua muito acima do piso de AA e lê visivelmente
mais macia — o contraste extremo era o que dava a sensação de "preto no branco".

### Acento — verde Cefor

| Token | Valor | Nota |
|---|---|---|
| `--accent` | `#1F7027` | 6.2:1; ação primária, link, estado ativo |
| `--accent-deep` | `#16531D` | 9.2:1; hover, ordinal dos momentos |
| `--accent-quiet` | `#E4F1E2` | lavagem clara dos dois painéis de leitura |
| `--accent-line` | `#7CB37F` | moldura suave que substituiu a de tinta cheia |

### Marca (pixel-mark) — valores obrigatórios

`--mark-green #3DA63D` · `--mark-red #E2211C`. O manual de identidade da Rede
Federal fixa esses dois valores; o pixel-mark **não herda** `--accent`.

### Estado — reservado, com par tinta + fundo claro

| Estado | Tinta | Fundo | Tinta sobre fundo |
|---|---|---|---|
| good | `#0F7A22` | `#E0EEE2` | 4.56:1 |
| warning | `#8A5D0B` | `#F0EADF` | 4.80:1 |
| serious | `#A64A1C` | `#F3E7E1` | 4.81:1 |
| critical | `#B23434` | `#F5E5E5` | 5.00:1 |

Nunca reaproveitados como cor de série, e sempre com ícone + rótulo — nunca cor
sozinha. O rótulo de estado vive numa ficha arredondada do seu próprio fundo.

### Famílias por tipo de atividade

Ordem fixa, jamais ciclada. Quatro tons por tipo: **marca** (a cor da barra),
**-soft** (fundo claro), **-line** (fio), **-ink** (tinta da família).

| Slot | marca | -soft | -line | -ink | Tipo |
|---|---|---|---|---|---|
| 1 | `#17509E` | `#E1E8F2` | `#A7BDDA` | `#17509E` | Aquisição |
| 2 | `#C2521A` | `#F7E9E1` | `#E8BDA8` | `#AF4A17` | Prática |
| 3 | `#00A0C6` | `#DEF3F8` | `#9EDBE9` | `#00738F` | Produção |
| 4 | `#B08600` | `#F5EFDE` | `#E1D19E` | `#866600` | Discussão |
| 5 | `#D24A9E` | `#F9E7F2` | `#EEBADA` | `#AC3D82` | Investigação |
| 6 | `#008300` | `#DEEFDE` | `#9ED09E` | `#007900` | Colaboração |
| 7 | `#8452D6` | `#EFE9FA` | `#D0BDEF` | `#7C4DC9` | Síncrona ou presencial |

**Validação das marcas** (`dataviz/scripts/validate_palette.js --mode light
--surface #ffffff`): banda de luminosidade ✓, piso de croma ✓, separação para
daltonismo em pares vizinhos ΔE 16.1 (pior caso, deutan) ✓, piso de visão normal
ΔE 20.8 ✓, **contraste ≥ 3:1 nas sete** ✓ — acima da paleta de referência da
própria skill, que aceita três slots abaixo de 3:1.

Cada `-ink` passa **≥ 4.5:1 sobre o seu próprio -soft** (4.64 a 6.37); `--ink`
sobre qualquer `-soft` fica entre 10.3 e 11.0.

Pares não-vizinhos mais próximos: ouro ↔ ferrugem (ΔE 12.8 normal). Aceito
porque toda marca do sistema carrega rótulo de texto ao lado — identidade nunca
depende só de cor.

---

## Onde a família de cada tipo aparece

O CSS é **o mesmo para os sete**: o elemento recebe `--c-base / --c-soft /
--c-line / --c-ink` em variáveis locais (`catVars(idx)` no JS, `style=` inline
no HTML estático) e as regras leem essas variáveis.

| Superfície | Como veste |
|---|---|
| **Quadro 2**, coluna "Tipo de atividade" | célula inteira em `-soft`, texto em `-ink`, fio direito em `-line` |
| **Classificação de Laurillard**, os 6 itens | ficha em `-soft` com fio `-line`; o nome do tipo em `-ink` |
| **Lista de atividades** | ficha arredondada com o nome do tipo, em `-soft`/`-ink`/`-line` — substituiu o ponto de 8px, que dizia menos |
| **Modal, seletor de tipo** | cada card em `-soft` com fio `-line`; hover e seleção sobem para a marca sólida, seleção com anel interno de 2px |
| **Gráfico de equilíbrio** | trilho em `-soft`, barra na marca sólida |

Rótulo e valor de cada série vestem token de texto (`--ink-soft` / `--muted`),
nunca a cor da série.

---

## Tipografia

| Papel | Face | Uso |
|---|---|---|
| Texto | **Inter Tight** 300–600 | tudo: títulos, leitura grande, listas, rótulos, controles |
| Ênfase | **Instrument Serif** itálico 400, em `--accent` | `<em>` — a única voz fora da família |

Duas faces fixadas pelo cliente. O que faz o conjunto não ler como padrão não é
a escolha da família — é o **tratamento**: peso 300 nos tamanhos grandes com
tracking bem fechado, de modo que a presença venha do tamanho e não da gordura
da letra; e uma serifa itálica verde como único contraponto.

**A regra do peso segue o tamanho.** 300 só onde o texto é grande o bastante
para sustentar traço fino; abaixo disso a legibilidade manda:

| Tamanho | Peso | Onde |
|---|---|---|
| ≥ 1.5rem | 300 | H1, títulos de seção |
| 1.05–1.3rem | 400–500 | subtítulos, nome do curso, título de modal |
| < 1rem | 500–600 | listas, botões, fichas, rótulos em caixa alta |

**A exceção é a leitura** (`#stat-total`): `2.9rem/600`, o único texto pesado da
página. É o número que a ferramenta existe para entregar — ele ancora o painel e
não divide peso com nada. Tracking em `-0.028em`, menos fechado que o dos títulos
leves, porque peso maior precisa de mais ar entre as letras.

**A ênfase** (`em`) troca de família, entra em itálico e assume `--accent`
(#1F7027 — 5.8:1 sobre o papel, 5.3:1 sobre a faixa). Vem 8% maior para casar a
altura-x com a grotesca ao lado. Aparece quatro vezes na página inteira: uma no
H1 e três na prosa. Ênfase que aparece em todo lugar deixa de enfatizar.

- H1 em 300, `letter-spacing: -0.032em`, `clamp(2.4rem, 4.2vw, 3.7rem)`.
- Leitura em `2.9rem/600` com `-0.028em` — a exceção deliberada à regra do peso.
- Medida de leitura em 68ch (`.prose`), dentro da faixa 65–75.
- `font-variant-numeric: tabular-nums` em toda coluna de dígitos.
- Micro-rótulos em caixa alta levam `letter-spacing: 0.08em` e vão em `--ink-soft`.

---

## Estrutura e profundidade

Não há sombra em card. Profundidade vem da escada de fundos, dos fios e das
lavagens claras. A única sombra do sistema é a do modal, com deslocamento e
desfoque — nunca halo colorido de deslocamento zero.

**Lavagem verde** marca as duas faces do instrumento, e só elas: a barra e a
leitura de `.app-preview` (a prévia, na abertura) e o primeiro bloco de
`.results-card` (a leitura da ferramenta).

O elemento lateral da abertura é **a medida**, não a interface em miniatura.
Uma régua vertical de 20 horas com o MOOC de exemplo empilhado nela, faixa por
faixa: cada faixa é uma atividade, a altura é o tempo que ela pede do estudante
e a cor é a família do tipo na taxonomia. Aquisição ocupa a largura cheia e os
demais tipos entram recuados, de modo que o perfil serrilhado da direita separe
os tipos sem depender só da cor. O empilhamento fecha exatamente na marca das
20 h declaradas, o único traço em cor de sinal do desenho.

Nada ali é desenho decorativo nem número copiado à mão: `renderMeasure()` monta
a régua, as faixas e os rótulos a partir de `TEMPLATES["20"]` e de
`computeMinutes()` — as mesmas fontes que alimentam a ferramenta. Trocar o
exemplo redesenha a abertura no mesmo commit, e a contagem no rodapé da figura
("49 atividades em 4 módulos") é lida do template, nunca digitada.

Antes ali houve duas coisas, nesta ordem: uma tabela de referência
(`.readout-box`) com seis conversões isoladas — números corretos, objeto que não
existia em lugar nenhum do produto —, e depois a própria ferramenta em
miniatura, montada com `.result-block`, `.gauge-*` e `.balance-*`. A miniatura
resolvia a divergência entre promessa e produto, mas era literal demais para a
primeira dobra: repetia a interface que está a um clique de distância. A régua
mantém a garantia (mesma matéria, mesmo commit) e devolve o símbolo. As seis
conversões continuam sendo o Quadro 2, logo abaixo, onde a tabela é a forma
certa.

A figura não tem moldura, fundo nem sombra: ela se apoia no papel da página.
`.m-band` desenha com `shape-rendering: crispEdges` para que faixas de 3 px não
saiam borradas, e os rótulos da régua e dos módulos ficam em `--muted`, com a
tipografia da página (`var(--font-display)` aplicada ao `<svg>`).

**Adicionar atividade** é a única ação em tamanho cheio da barra (1rem, 13×22px),
isolada no primeiro grupo por uma divisória, e repetida como botão primário dentro
do estado vazio. Tudo o mais na barra é `btn-sm`.

**A linha inteira da atividade abre a edição.** Um alvo de 30×30px para a ação
mais frequente da lista era estreito demais; agora o alvo é a linha toda — nome,
ficha do tipo, tempo e o espaço entre eles —, e o nome muda para `--accent-deep`
sob o cursor para anunciar isso. As três zonas de gesto próprio ficam de fora:
a alça de arrastar, as setas e os dois botões de ação. O lápis continua ali como
atalho visível e como o caminho de teclado, que uma `div` clicável não oferece.

**O campo do nome do curso** é uma caixa com contorno próprio, não um sublinhado:
o sublinhado repetia a régua do cabeçalho logo abaixo e lia como linha dupla.

**Régua de seção**: `.h-section::before` desenha um traço de 64×3px em `--rule`
acima de cada título. É marcação de instrumento, não rótulo — nenhum *kicker* de
texto entra na página.

Numeração 1/2/3 aparece só em "Três momentos", onde a ordem é cronologia real
do processo. Cada ordinal vive numa ficha circular de lavagem verde.

---

## Módulos — opcionais, e invisíveis até existirem

O professor pode agrupar as atividades em módulos (ou unidades, ou semanas). A
decisão de projeto é que **a estrutura não cobra pedágio de quem não a usa**:
com zero módulos criados a tela é a de antes — nenhuma faixa na lista, nenhum
campo no modal, nenhum bloco no painel. O único elemento novo permanente é um
`btn-ghost btn-sm` "Novo módulo" na barra, o mais fraco da hierarquia, ao lado
da ação de tamanho cheio.

### Dado

`state.modules` é `[{id, name}]`, e a ordem do array é a ordem na tela. Cada
atividade ganha `moduleId` — o id de um módulo ou `null`. `state.activities`
continua sendo **um array plano**: a ordem dentro do grupo é a ordem do array
filtrado, então arrastar, as setas e a reordenação seguem operando sobre a mesma
estrutura de antes.

`moduleId` que não corresponde a módulo nenhum (arquivo editado à mão, módulo
removido) é lido como "sem módulo". A regra é a mesma do gráfico de equilíbrio:
**nunca some tempo que já está somado no total**.

### Onde aparece

| Superfície | Como veste |
|---|---|
| **Lista** | uma faixa de 43px por grupo, em `--surface-quiet` — a mesma linguagem das faixas de seção. Nome à esquerda, subtotal e % à direita, três `icon-btn` de 26px (subir, descer, remover) |
| **Faixa "Sem módulo"** | idêntica, sem controles, nome em `--muted` (5.2:1 sobre a faixa); só existe quando há pelo menos um módulo |
| **Módulo vazio** | uma linha de convite em `--muted-2`, que é também o alvo de soltar |
| **Modal** | um `select` "Módulo" junto de Repetições e Nome, com `+ Novo módulo…` no fim — renderizado só quando há módulos |
| **Painel** | um `.result-block` "Equilíbrio por módulo", oculto sem módulos |

Não há trilho colorido na faixa nem card por módulo: agrupar é uma mudança de
fundo e um fio, como toda seção da página.

### O nome se edita na própria faixa

Não há diálogo de renomear. O nome é um `input` sem contorno que ganha moldura
no hover e no foco. Editar **não repinta a lista** — o foco se perderia —,
repinta só o painel. Nome apagado volta ao padrão `Módulo N` ao sair do campo.

### Equilíbrio: barras de 100% empilhadas

O equilíbrio por tipo é uma única barra de 100% empilhada, seguida por uma
legenda compacta com nome, duração e percentual. Tipos com zero minuto não
aparecem: não alteram a leitura e só aumentariam a altura do painel.

Repetir esse gráfico por módulo custaria muitas linhas e afogaria a leitura
principal. Cada módulo também é **uma barra 100% empilhada**, na grade `.bal-row`
(rótulo / trilho / valor), com os segmentos nas cores das famílias.

É um desvio consciente da regra "cada barra carrega rótulo direto": o gráfico
por tipo fica **imediatamente acima, no mesmo painel**, e serve de legenda —
a taxonomia de cor foi lida duas linhas antes. Para quem não lê a cor, cada
barra leva a decomposição em texto no `aria-label` e no `title` ("Aquisição
40%, Prática 25%…"), e o valor da linha continua escrito ao lado.

### Movimento entre módulos

| Gesto | O que faz |
|---|---|
| Arrastar sobre uma **linha** | herda o módulo dela e entra na posição |
| Arrastar sobre a **faixa** (ou o vazio do módulo) | vai para o fim daquele módulo |
| Setas ↑ ↓ | reordenam **dentro** do módulo; na borda do grupo ficam desabilitadas |
| `select` do modal | troca o módulo da atividade — o caminho de toque, onde arrastar não existe |

### Os exemplos já vêm modularizados — e são MOOC de verdade

Carregar um exemplo entrega o curso dividido, com os módulos numerados:
**Módulo 1, Módulo 2, …**. Nome numerado não afirma pedagogia nenhuma sobre um
curso que não existe — o professor renomeia na própria faixa assim que souber do
que trata cada um.

Os exemplos usam **só as quatro tarefas que o estudante faz sozinho**: leitura,
vídeo/áudio, questionário e atividade interativa (H5P). Nada de escrita,
discussão ou investigação — as três pressupõem alguém do outro lado corrigindo
ou respondendo, que é justamente o que um MOOC autoinstrucional não tem. Antes
os exemplos as usavam, e isso ensinava um MOOC que o Cefor não entrega.

| Exemplo | Módulos | Atividades | Peso de cada módulo | Estimativa |
|---|---|---|---|---|
| 20h | 3 | 13 | 34% · 32% · 34% | 20h 14min — dentro do esperado |
| 40h | 4 | 18 | 24% · 25% · 25% · 25% | 40h 03min — dentro do esperado |
| 60h | 5 | 22 | 20% cada | 59h 59min — dentro do esperado |

Cada módulo mistura **aquisição e prática** em vez de empilhar toda a leitura no
primeiro: é o arranjo que o gráfico por módulo existe para revelar. O equilíbrio
resultante fica perto de 48% aquisição / 52% prática, e os três tipos que o
exemplo não usa aparecem no gráfico zerados — o vazio também é leitura.

Os três exemplos agora **pousam na meta** (100%, 100%, 100%), com o estado em
"dentro do esperado". Antes ficavam 1 a 13% abaixo, o que fazia o exemplo
carregar um aviso amarelo que não era sobre nada.

Carregar um exemplo **substitui a estrutura inteira** — atividades e módulos —,
e o aviso diz em quantos módulos ele vem.

### O que módulo não faz

Não tem carga horária própria nem meta por módulo: a meta continua sendo do
curso. Remover um módulo nunca apaga atividade — elas voltam para "sem módulo",
e o aviso diz isso; módulo vazio sai sem diálogo.

**"Limpar" leva os módulos junto.** Módulo é estrutura do curso, como a
atividade — o que sobrevive é só o que o professor digitou no cabeçalho: nome e
carga pretendida. O aviso nomeia as duas quantidades ("As 15 atividades e os 4
módulos deste curso serão removidos") e o rótulo da ação muda para "Limpar tudo"
quando há módulo em jogo.

---

## Contador de palavras no cadastro de leitura

O campo `Número de palavras` continua sendo a fonte do cálculo. Quando o professor
já tem o texto, o atalho pequeno **“Tenho o texto. Abrir contador de palavras”**
abre um diálogo sobre o cadastro, sem criar uma etapa obrigatória para quem prefere
digitar a quantidade ou estimá-la pelo número de páginas.

O diálogo tem uma única tarefa: receber o texto, contar tokens separados por espaço
que contenham ao menos uma letra ou número e devolver a quantidade ao campo da
atividade. A contagem atualiza a cada edição; o botão começa desabilitado e passa a
nomear o valor que será usado, por exemplo `Usar 1.248 palavras`.

O conteúdo colado vive somente no `textarea` do diálogo. Ele não entra em `draft`,
`state`, `localStorage` ou no arquivo salvo. Ao confirmar, apenas `draft.params.words`
é atualizado. Cancelar, clicar fora ou pressionar `Esc` descarta o texto e preserva
o valor que já estava no cadastro. `Esc` fecha primeiro o contador, sem fechar o
modal de atividade que está abaixo.

O botão **“Selecionar PDF”** aceita PDFs de até 30 MB e extrai o texto localmente
no navegador com PDF.js, sem enviar ou persistir o arquivo. O texto selecionável é
colocado no mesmo campo temporário e segue a mesma contagem; PDFs digitalizados,
protegidos por senha, inválidos ou sem texto extraível recebem uma mensagem clara
para o usuário. O descarte usa o `loadingTask` do PDF.js, inclusive ao cancelar ou
fechar o diálogo, para liberar a leitura sem apagar uma contagem já confirmada.
Para permitir o uso mesmo quando o HTML é aberto diretamente pelo computador,
o projeto também carrega uma cópia clássica compatível do PDF.js e usa um worker
local correspondente; quando há servidor web, mantém o worker em módulo.

Visualmente, o resultado usa a mesma lavagem verde e a mesma moldura do painel de
leitura. Não há nova cor, sombra ou família de raio. Em telas estreitas, rótulo e
valor empilham, o diálogo mantém 16px de margem lateral e o documento não ganha
rolagem horizontal.

## Salvamento e confirmações

### Dois lugares, não três

| O quê | Onde vive | Quem escreve |
|---|---|---|
| **Rascunho** | `localStorage`, chave `estimador-carga-horaria:v1` | gravado sozinho a cada mudança, sempre |
| **Arquivo** | um `.json` que o professor guarda onde quiser | os botões **Salvar** e **Restaurar** |

Os dois guardam o estado inteiro, módulos incluídos. Arquivo salvo antes dos
módulos abre sem eles; arquivo com módulos aberto numa versão anterior só ignora
os campos que não conhece. Na leitura, módulo sem `id` é descartado e atividade
que aponta para módulo inexistente entra como "sem módulo" — a atividade fica.

Nada exige ação para não se perder: o rascunho é gravado a cada tecla. Os três
botões cuidam de levar o curso para fora deste navegador e de trazê-lo de volta.

| Botão | O que faz |
|---|---|
| **Salvar** | baixa `estimador-<nome-do-curso>-AAAAMMDD.json` |
| **Restaurar** | abre o seletor de arquivos e lê um desses `.json` |
| **Limpar** | zera a estrutura do curso — atividades **e** módulos; desabilitado só quando não há nem uma coisa nem outra |

Nenhum texto fixo de salvamento ocupa a barra: aviso de ação é um **toast** que
aparece só quando há o que dizer e some sozinho (5s; 9s quando é erro).

Restaurar pede confirmação só quando já existe curso montado — com a lista
vazia, aplica direto. O arquivo é editável à mão, então a leitura descarta
atividades cujo tipo e tarefa a ferramenta não conhece, devolve `id` a quem
tiver perdido o seu, e diz na linha de estado quantas foram descartadas.

### O download não pode partir da página

Dentro do artifact o sandbox **inutiliza qualquer download que a própria página
inicie** — `<a download>`, `blob:` e `data:` incluídos. Quem entrega o arquivo
é a capability `downloads` do visualizador, declarada no publish
(`capabilities: {downloads: true}`) e obtida com `await claude.use("downloads")`,
que mostra ao professor uma confirmação com nome e tamanho antes de salvar.

O código trata os três desfechos: `declined` (o professor recusou — nada de
retry automático), `rate_limited` e `too_large` viram aviso na linha de estado.
Quando `use()` devolve `null` — o HTML aberto direto do disco, fora do
visualizador — cai no caminho comum do `<a download>`, que ali funciona.

### Nenhum diálogo nativo

`window.confirm` e `window.alert` **não funcionam dentro do iframe do
artifact** — o sandbox não traz `allow-modals`, então devolvem `false` sem
aviso nenhum e a ação morre em silêncio. Era exatamente o que impedia "Carregar
um curso de exemplo" de substituir uma lista já montada, e o que fazia o toggle
de MOOC e o limpar-tudo não responderem.

Todo aviso passa por `askConfirm()`, um diálogo na própria página com título,
frase que nomeia a consequência, rótulo de ação que diz o que vai acontecer
("Substituir pelo exemplo", "Limpar atividades") e variante destrutiva sólida.
Erro de leitura de arquivo virou aviso na linha de estado da barra de ações, com
validação de formato que antes não existia.

---

## Movimento

**Um** momento autoral: o preenchimento do medidor percorrendo até a nova
leitura, em `cubic-bezier(0.16, 1, 0.3, 1)` por 450ms.

Implementado com `clip-path: inset(...)` em vez de `width` — anima no
compositor, sem refluxo, e preserva o canto arredondado da ponta (que `scaleX`
distorceria). Tudo mais é mudança de estado, não entrada.

`prefers-reduced-motion: reduce` zera animações e transições globalmente.

---

## Marcas de dado

- Barra ancorada na linha de base: `border-radius: 0 3px 3px 0` — canto reto na
  origem, arredondado só na ponta de dado.
- `min-width: 3px` garante que um valor pequeno continue visível, mas é anulado
  quando o valor é **zero**: com os exemplos MOOC três tipos ficam zerados, e um
  traço de 3px ali leria como "tem alguma coisa".
- Trilho de série na `-soft` da própria série; trilho do medidor em `--well`
  neutro, porque ali a cor codifica **estado**, não série.
- Marcador de meta: tique de 2px em `--ink`, mais alto que o trilho.
- A barra empilhada por tipo tem uma legenda compacta logo abaixo; as barras por
  módulo reutilizam essa taxonomia de cor. Todas levam a decomposição em texto no
  `aria-label`.

---

## Verificação executada

| Checagem | Resultado |
|---|---|
| Contraste computado, home (129 elementos de texto, Quadro 2 com 57 células) | 0 reprovações em AA |
| Contraste computado, ferramenta + modal (116 elementos, 16 fichas, 7 cards) | 0 reprovações em AA |
| Contraste computado, diálogo de confirmação | 0 reprovações em AA |
| Teste funcional ponta a ponta (29 asserções: salvar em arquivo, restaurar válido/inválido/misto, cancelamento, limpar, persistência, tipografia, ênfase em serifa verde, campo do nome, hierarquia do botão) | 29/29 |
| Teste funcional anterior (25 asserções: exemplos, toggle MOOC, alinhamento, tipografia) | 25/25 |
| Teste funcional de módulos (68 asserções: exemplos modularizados e restritos às tarefas autoinstrucionais, criar, renomear, mover pelo modal, subtotais, reordenar módulo, alvo de clique da linha, persistir, remover com e sem atividades, limpar) | 68/68 |
| Arrastar entre módulos (11 asserções: soltar na faixa, soltar sobre linha, voltar ao módulo de origem, total invariante, arrastar não abre a edição) | 11/11 |
| Módulo órfão depois de recarregar (4 asserções) | 4/4 |
| Restaurar de arquivo com módulos (13 asserções: módulo sem id, atividade órfã, arquivo anterior aos módulos, toggle MOOC) | 13/13 |
| Layout com módulos em 1440px, 768px e 390px (6 asserções cada) | 18/18 |
| Contraste computado, ferramenta com módulos (117 elementos de texto) | 0 reprovações em AA |
| Contador de palavras (fluxo completo) | 14 palavras contadas, aplicadas ao campo e registradas na lista |
| Contador de palavras (cancelamento) | `Esc` fecha só o contador e preserva a quantidade anterior |
| Contador de palavras (PDF com texto) | PDF de teste lido localmente, 13 palavras aplicadas ao campo e registradas na lista |
| Contador de palavras (PDF digitalizado) | Mensagem de ausência de texto extraível; quantidade anterior preservada ao cancelar |
| Contador de palavras (compatibilidade local) | Biblioteca clássica e fake worker local compatíveis; leitura validada sem dependência do módulo ES |
| Contador de palavras (layout) | conferido em 1280×900 e 390×844; sem rolagem horizontal |
| Console do navegador durante o fluxo | 0 erros |
| Placeholder | 5.23:1 |
| `-ink` sobre o próprio `-soft`, 7 famílias | 4.64 a 6.37 |
| `scrollWidth` vs viewport em 390px, 768px e 1440px | igual, 0 elementos fora |
| Detector mecânico de design | limpo |
| Erros de JS no carregamento | nenhum |
| Paleta categórica (validador da skill dataviz) | todas as checagens passam |

Feito com Chrome headless em 1440px, 1200px, 768px e 390px, nas duas telas.

---

## Um aviso conhecido, aceito de propósito

O detector mecânico marca `overused-font` para Inter — está na lista de faces
que aparecem em toda leva de interface gerada. A face foi **fixada pelo cliente**,
com peso e estilo explícitos, e brief pinado vence aviso de padrão saturado.
O que tira o conjunto do lugar-comum é o tratamento descrito acima, não a troca
da família. Registrado aqui para que ninguém "conserte" isso sem falar com quem
pediu.

---

## Fora de escopo nesta versão

- Não há alternância de tema. Reintroduzir modo escuro exigiria repassar a
  escada de fundos, as sete famílias e os quatro pares de estado contra a
  superfície escura — não é uma inversão automática.
- Tabela do Quadro 2 rola horizontalmente dentro do próprio container abaixo de
  640px; o corpo da página nunca rola de lado.
- Módulo não tem meta própria: a leitura de "dentro do esperado" continua sendo
  do curso inteiro. É decisão de escopo, não limitação do modelo — `state.modules`
  comporta um campo de meta sem mudança estrutural.
