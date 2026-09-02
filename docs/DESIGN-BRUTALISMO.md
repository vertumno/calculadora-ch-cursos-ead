# DESIGN-BRUTALISMO.md — Estimador de Carga Horária, proposta B

Sistema visual de `estimador-carga-horaria-b.html`. Arquivo único, sem build.
Proposta alternativa à de `DESIGN.md` (`estimador-carga-horaria-a.html`), que continua
intacta. **O motor é o mesmo**: `TYPES`, `computeMinutes`, `TEMPLATES`, módulos,
contador de palavras (PDF.js) e persistência foram reaproveitados sem alteração —
só a chave do `localStorage` mudou (`estimador-carga-horaria:v2-brutal`), para as
duas versões não disputarem o mesmo rascunho.

---

## Tese

A proposta A lê como **referência de pesquisa**: papel esverdeado, fios finos, uma
cor de sinal, presença vinda do tamanho e não do peso.

Esta proposta assume o oposto declarado: o instrumento vira **maquinário**.
Contorno preto em tudo, sombra sólida deslocada, tipografia expandida em caixa
alta, zero gradiente, zero transparência decorativa. A hierarquia vem de **peso e
contorno**, nunca de tom. É a mesma metodologia, com outra voz.

Referência visual: neo-brutalismo editorial (o layout CleanEnergyX enviado como
principal, e as três demais peças como calibragem de paleta e de moldura).

---

## Cor

### Chão e tinta

| Token | Valor | Onde |
|---|---|---|
| `--paper` | `#EDEDE6` | chão da página — bege-osso, nunca branco |
| `--paper-2` / `--surface-quiet` | `#E2E2D9` | faixas de seção alternadas |
| `--surface` | `#FFFFFF` | todo painel, linha e card |
| `--well` | `#D5D5CB` | poço dos medidores |
| `--ink` | `#0B0B0B` | tinta, contorno e sombra — a mesma cor nos três papéis |
| `--ink-soft` `#2C2C2A` · `--muted` `#55554F` · `--muted-2` `#6A6A63` | | corpo, secundário, legenda |

### Acento

| Token | Valor | Uso |
|---|---|---|
| `--acid` | `#D8F534` | ação primária, leitura principal, estados ativos, ênfase (`em`) |
| `--acid-deep` | `#C0DC1C` | hover do botão primário |
| `--acid-wash` | `#F1FBBE` | faixas de apoio: hover de linha, nota de ajuda, coluna social |

Um único acento na página inteira. Ele não nomeia nada — só aponta.

### Famílias por tipo de atividade

Sete famílias, ordem fixa, jamais ciclada. A mudança em relação à proposta A é
estrutural: **o filete é sempre preto** (`--cat-N-line: #0B0B0B`) e **a tinta é
sempre preta** (`--cat-N-ink`). O contorno é o que separa; a cor apenas nomeia.
É isso que permite sete matizes vivas sem que briguem entre si.

| Slot | marca | lavagem (`-soft`) | Tipo |
|---|---|---|---|
| 1 | `#4A6CF7` | `#DCE3FE` | Aquisição |
| 2 | `#FF6B35` | `#FFE1D3` | Prática |
| 3 | `#00C2D1` | `#CFF3F6` | Produção |
| 4 | `#FFC93C` | `#FFF0CC` | Discussão |
| 5 | `#F45DB0` | `#FCDEEF` | Investigação |
| 6 | `#3DBE5C` | `#D8F2DE` | Colaboração |
| 7 | `#9B6DF3` | `#E8DEFD` | Síncrona ou presencial |

**Regra de legibilidade:** rótulo nunca vai sobre a marca saturada. Onde o tipo
precisa aparecer nomeado, o fundo é a lavagem (`-soft`, preto sobre ela entre
15.3:1 e 17.4:1) e a marca entra como **barra sólida de 11-12px** com filete preto —
na coluna "Tipo de atividade" do Quadro e no seletor de tipo do modal. A marca
cheia só pinta superfície sem texto: barras do gráfico de equilíbrio, faixas da
régua da abertura, amostras da legenda.

### Estado

| Estado | Tinta / barra | Fundo da ficha | Contraste |
|---|---|---|---|
| good | `#15772F` | `#D8F2DE` | 4.76:1 |
| warning | `#8A5D0B` | `#FFF0CC` | 5.09:1 |
| serious | `#B3400E` | `#FFE1D3` | 4.64:1 |
| critical | `#C11B1B` | `#FFDCDC` | 4.80:1 |

O mesmo token pinta a tinta da ficha e o preenchimento do medidor: por isso é
escuro e saturado, e não uma cor clara de aviso. Sempre com ícone + rótulo.

---

## Tipografia

| Papel | Face | Tratamento |
|---|---|---|
| Display | **Archivo** (eixo `wdth`) | caixa alta, `wdth` 106-118, `wght` 800-900, `line-height` 0.92-0.98 |
| Leitura | **Space Grotesk** | 400/500, corpo em 15px, medida em 68ch |
| Máquina | **JetBrains Mono** | micro-rótulos, botões, números, etiquetas — sempre caixa alta com `letter-spacing` 0.06-0.14em |

O contraponto da proposta A era uma serifa itálica verde. Aqui é a **mono**: todo
rótulo de controle, botão e número usa JetBrains Mono em caixa alta, e toda voz
editorial usa Space Grotesk em caixa baixa. A separação entre "o que a máquina
diz" e "o que o texto diz" é tipográfica.

A única palavra colorida da abertura é a do H1 (`ESTIME`): preenchimento ácido com
`-webkit-text-stroke` preto de 2.5px e `paint-order: stroke fill`. O mesmo
tratamento veste o ordinal dos três momentos.

`em` não troca de família: recebe fundo ácido com `box-shadow` de raio zero — um
marca-texto, não um itálico. Aparece três vezes na página inteira.

---

## Estrutura e profundidade

Uma só receita de profundidade, aplicada em três degraus:

| Token | Valor | Onde |
|---|---|---|
| `--sh` | `4px 4px 0` | botões, linhas de módulo, cards de seção |
| `--sh-md` | `6px 6px 0` | painéis grandes: cabeçalho da ferramenta, leitura, Quadro |
| `--sh-lg` | `9px 9px 0` | hover de card e bloco de créditos |
| — | `10px 10px 0` | modal |

Nunca desfoque, nunca halo, nunca sombra colorida. Contornos em três espessuras:
`1.5px` (separador interno), `2px` (padrão) e `3px` (modal e estado vazio).

**Movimento:** um único gesto. O elemento se aproxima ao ser apontado
(`translate(-2px,-2px)` + sombra maior) e afunda ao ser pressionado
(`translate(3px,3px)` + sombra zero). A exceção é o ponteiro do medidor, que
continua viajando por `clip-path` em ease-out exponencial.

**Mobiliário técnico** (cantos em L, cruzes, malhas pontilhadas, estrela de 14
pontas atrás da figura) é decoração assumida da linguagem, mantida fora do fluxo
(`position:absolute`, `z-index:0`) e escondida abaixo de 900px, onde competiria
com o texto.

---

## Abertura

O elemento lateral continua sendo **a medida**, não a interface: uma régua de 20 h
montada por `renderMeasure()` a partir de um template e de `computeMinutes()` — as
mesmas fontes que alimentam a ferramenta.

A fonte mudou: a figura agora desenha `TEMPLATES["hibrido20"]`, um exemplo novo que
**percorre os sete tipos da taxonomia**, em vez do MOOC puro, que por definição só
comporta quatro tarefas autoinstrucionais. Aquisição (44%) e prática (19%) seguem
predominantes; produção (13%), discussão (10%), investigação (7,5%), colaboração
(4%) e o encontro síncrono (2,5%) ocupam o terço restante. O curso fecha em 1200
minutos exatos, então a pilha continua batendo na marca das 20 h declaradas.

Esse exemplo também entra no seletor da ferramenta ("Exemplo · Curso híbrido de 20
horas"), e declara `mooc: false` — carregá-lo desliga o interruptor de MOOC, que
esconderia colaboração e atividades síncronas. A promessa da abertura e o produto
atrás do CTA continuam sendo o mesmo curso.

**A largura passou a codificar o tipo.** Antes eram duas larguras (aquisição cheia,
resto recuado); agora a faixa perde 7,5% a cada posição da taxonomia — aquisição em
100%, síncrona em 55%. O perfil serrilhado da direita separa os sete tipos sem
depender só da cor. A legenda também é montada a partir dos dados: lista só os tipos
que o exemplo usa, na ordem da taxonomia.

O enquadramento é novo — a régua vive dentro de um painel branco com contorno e
sombra, com cabeçalho próprio ("Curso de exemplo · híbrido / 20 h · medidas"), e as
faixas ganharam filete preto de 1px. A estrela ácida entra por trás do painel, no
lugar que a referência dá ao raio de sol.

A faixa inferior ("Feito para quem planeja EaD | Vídeos | Leituras | …") repete a
gramática da barra de logotipos da referência, mas lista os recursos que a
ferramenta sabe medir — não parceiros fictícios.

## O que não mudou

Conteúdo, metodologia, parâmetros do Quadro 2, taxonomia de Laurillard,
autoria e o comportamento inteiro da ferramenta. Trocar de proposta não muda
nenhum número que o professor lê.
