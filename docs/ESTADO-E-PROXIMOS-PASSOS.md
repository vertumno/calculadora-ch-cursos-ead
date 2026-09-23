# Estado do projeto e próximos passos — Calculadora de CH MOOC (CEFOR/IFES)

> Documento de retomada. Resume **o que existe**, **o que foi feito**, **as decisões tomadas** e **o que falta**. Última atualização: **2026-08-26**.

---

## 1. O que é o projeto

Ferramenta web para **estimar e validar a carga horária (CH)** de cursos a distância do IFES/CEFOR. Nasceu como porte do *Course Workload Estimator* (Wake Forest/Rice) e evoluiu para um **estimador nativo de MOOC**, baseado na pesquisa de doutorado de **Aline Pinto Amorim** (orient. Vanessa Battestin, co-orient. Marize Lyra Silva Passos).

- **Dor central:** professores não têm parâmetro para estimar CH; erram muito (em geral **superestimam**, sobrecarregando o aluno). Micro-credenciais/MOOCs exigem CH coerente para certificação.
- **Base teórica da proposta:** *Conversational Framework* de **Laurillard (2012)** + rates de **McInnes et al. (2026)**, Liu & Evans (2020), Beer (2019).
- **Decisão estratégica (reunião 29/06):** começar simples — calculadora **separada** (não acoplada ao mapa de atividades), para MOOC, disponível na base de conhecimento. Refino iterativo com a especialista (Aline) em sessões.
- **Reunião de alinhamento (26/08):** com Aline Amorim e Marcos Vinícius Forecchi Accioly, validou ao vivo o fluxo guiado em 3 etapas (ver §3.5) e confirmou o escopo — a ferramenta é um **estimador de planejamento** (não um analisador de curso pronto), fica **fora** da planilha/mapa de atividades, e o foco desta versão é **MOOC** (não presencial/híbrido genérico). No mesmo dia, esse fluxo (`index-cefor-v2.html`) foi promovido a versão oficial e ganhou uma página de entrada (`index.html`).
- Publicação em artigo prevista — o artigo da Aline já está pronto para submissão, faltando a ferramenta funcionar e o teste de usabilidade (com a Rute). Defesa de doutorado prevista para fevereiro/2026.

---

## 2. Estrutura de arquivos (atual)

> Reorganizado em 2026-09-02: os dois estimadores oficiais passaram a viver na **raiz** (que é o que o GitHub Pages publica), as dependências foram para `assets/` e as páginas antigas saíram da raiz para `arquivo/`.

```
calculadora-ch-cursos-ead/
├── estimador-carga-horaria-a.html    # OPÇÃO A — direção editorial   — publicado no Pages
├── estimador-carga-horaria-b.html    # OPÇÃO B — direção brutalista  — publicado no Pages
├── README.md                         # documentação do repositório
├── PRODUCT.md                        # ficha de produto (plataforma, usuários, positioning, princípios)
├── assets/                           # tudo que as páginas carregam + material de marca
│   ├── vendor/pdfjs/                 # pdf.js embarcado (import do PDF) — dependência real das páginas
│   ├── cefor-horizontal-cor-web.png  # logo usada pelos estimadores (versão web, 2508×597)
│   ├── cefor-horizontal-cor.png      # logo oficial em alta (2835×1135) — referência
│   ├── icone_cefor-horizontal-cor.png# ícone oficial — referência
│   └── hero-proposta-editorial.svg   # arte da proposta editorial
├── arquivo/                          # MATERIAL ARQUIVADO (preservado, não em uso, fora do fluxo)
│   ├── README.md                     # inventário do arquivo
│   ├── index-gateway.html            # ex-`index.html` — porta de entrada de 26/08, aposentada em 02/09
│   ├── index-cefor-v2.html           # calculadora guiada em 3 etapas — antecessora dos estimadores oficiais
│   ├── index-cefor.html              # blocos fixos por Quadro 2 — arquivada em 26/08
│   ├── calculadora-workload-estimator.html  # v1 — porte do Workload Estimator (arquivada 30/06)
│   └── ANALISE-UX-UI.md              # análise UX/UI que fundamentou o redesign guiado
└── docs/
    ├── COMO ESTIMAR A CARGA HORÁRIA…PROPOSTA…IFES.md   # A PROPOSTA (Quadro 2 + Laurillard)
    ├── COMPARATIVO_calculadora-atual-vs-proposta-cefor.md  # comparativo v1 × proposta (histórico)
    ├── DESIGN.md / DESIGN-BRUTALISMO.md                 # racional das direções visuais
    ├── design-logo-cefor.md                             # notas de identidade visual
    ├── ESTADO-E-PROXIMOS-PASSOS.md                      # ESTE arquivo
    ├── Revisão e ajustes da calculadora de carga horária.md  # feedback formal da Aline (30/06)
    ├── transcrição 2026-06-29 - Reuniao MOOC…txt         # racional das decisões da 1ª reunião
    ├── transcricao 2026-08-26 - Reunião…Aline Amorim Marquito e Elton.txt   # reunião de alinhamento (§3.5)
    └── source/                  # código original R/Shiny (server.R, ui.R) — referência
```

> **Nota de versões:** as duas versões ativas são `estimador-carga-horaria-a.html` (**Opção A**, editorial) e `estimador-carga-horaria-b.html` (**Opção B**, brutalista), ambas na raiz e ambas publicadas. Os sufixos `-a`/`-b` são deliberadamente neutros: as duas são direções paralelas em avaliação pela Aline, não versões sucessivas — nomes como `v1`/`v2` enviesariam a escolha. As chaves de `localStorage` internas (`:v1` e `:v2-brutal`) foram mantidas como estavam. Toda a linhagem anterior — a porta de entrada `index.html`, a calculadora guiada `index-cefor-v2.html`, os blocos fixos `index-cefor.html` e a v1 `calculadora-workload-estimator.html` — está em `arquivo/`, fora do site publicado. Para retomar qualquer versão arquivada, ver `arquivo/README.md`.

> **Nota de caminhos:** os estimadores carregam `./assets/vendor/pdfjs/…` e `assets/cefor-horizontal-cor-web.png`. Se algum dos dois for movido de diretório, esses caminhos precisam ser reajustados juntos.

---

## 3. O que foi feito

### 3.1 Comparativo v1 × proposta
`docs/COMPARATIVO_calculadora-atual-vs-proposta-cefor.md` — lista **todas** as diferenças classificadas em **[+] acrescentadas (8)**, **[~] modificadas (9)** e **[–] retiradas (8)**, mais implicações de implementação e lacunas a resolver. *(Histórico: compara a v1 arquivada com a proposta; hoje a versão ativa não é mais a v1.)*

### 3.2 `index-cefor.html` — calculadora fiel ao Quadro 2 (arquivada em 26/08)
Página única autocontida (HTML+CSS+JS, sem build/back-end), reaproveitando 100% da identidade visual IFES/CEFOR da v1. **Fiel ao Quadro 2**, em blocos fixos por tipo de aprendizagem.

**Modelo de cálculo (tudo em horas, somado na CH total do curso) — o mesmo motor usado hoje em `index-cefor-v2.html`:**

| Bloco (tipo Laurillard) | Entrada | Taxa do Quadro 2 |
|---|---|---|
| §01 Leitura *(Aquisição)* | palavras | 300 / 130 / 70 **palavras/min** (baixa/média/alta) |
| §02 Vídeo/Áudio *(Aquisição)* | minutos de mídia | **2×** (baixa) / **3×** (alta) a duração |
| §03 Investigação | horas | definido pelo professor |
| §04 Questionário *(Prática)* | nº questões | **2** (baixa) / **5** (alta) min/questão |
| §05 Atividade interativa *(Prática)* | quantidade | **15** (baixa) / **30** (alta) min |
| §06 Produção escrita *(Produção)* | palavras | 250 / 125 / 60 **palavras/hora** |
| §07 Artefatos *(Produção)* | horas | definido pelo professor |
| §08 Discussão | nº participações | **30 min** (baixa) / **1,5 h** (alta) |
| §09 Colaboração `*` | horas de produção equiv. | **×2** (sempre alta) |
| §10 Síncrono/Presencial `*` | nº encontros × duração | duração do evento |

**Funcionalidades da época:** itens dinâmicos por bloco, toggle de contexto (MOOC padrão × Híbrido/pesquisa), saídas de CH total + macro Individual/Social/Síncrono + equilíbrio por tipo de aprendizagem, calibração declarada × estimada (±15%), duração em tópicos opcional, limpar tudo/imprimir-PDF, acessibilidade (`prefers-reduced-motion`).

### 3.4 Ajustes da Aline aplicados (revisão 2026-06-30)
Feedback formal da Aline (arquivo `Revisão e ajustes da calculadora de carga horária.md`) confirmou que o **motor já estava fiel ao Quadro 2**. Ajustes pontuais aplicados: mudança conceitual de semana → tópico/módulo, texto do hero, helper e colophon de autoria/fonte com link "Saiba mais".

### 3.3 Verificações executadas na época (tudo passou)
Sintaxe JS validada via `vm.Script` (Node); fidelidade ao Quadro 2 — 16/16 testes numéricos conferidos.

### 3.5 Sessão 2026-08-26 — reunião de alinhamento + promoção da v2

**Reunião com Aline Amorim e Marcos Vinícius Forecchi Accioly** (61 min; transcrição completa em `docs/transcricao 2026-08-26…txt`):

- Parâmetros do Quadro 2 seguem **fechados**; nenhuma alteração desde a comissão anterior. O artigo-fonte dos parâmetros não disponibiliza ferramenta, só os números — daí a necessidade de construir do zero.
- Confirmado: é um **estimador**, não um **analisador**. Uso principal na etapa de planejamento/design do curso; pode ser reaplicado no fim para conferência, mas não é o foco desta fase.
- Confirmado: a ferramenta **não** entra na planilha/mapa de atividades (decisão já validada com a Vanessa) — fica separada, na base de conhecimento, de uso **opcional**, servindo tanto quem produz MOOC quanto disciplinas fora desse fluxo.
- Escopo desta versão é **MOOC**; generalizar para presencial/híbrido fica para depois (decisão deliberada de "começar do específico, generalizar depois").
- **Três momentos de uso mapeados:** (1) preenchimento do formulário do processo (só declara faixa de CH), (2) planejamento/produção do curso — uso principal, e (3) curso pronto, para conferência final.
- Dois protótipos de fluxo avaliados ao vivo: um formulário simples tipo lista (**rejeitado**, considerado UX ruim) e o fluxo guiado em **3 etapas** (Configurar → Atividades → Calibrar) com modal "Adicionar atividade" estilo Moodle (**aprovado por todos**) — é o modelo que `index-cefor-v2.html` já implementa.
- **Ponto em aberto sem solução de design definida:** como o professor declara um questionário que mistura questões de baixa e alta complexidade, já que o parâmetro do Quadro 2 é por questão individual. Ver §5.1.
- Ideias de evolução futura trazidas por Marcos (não iniciadas): biblioteca de modelos/templates de curso publicados pela coordenação; fluxo invertido (definir % de mídia desejada → a ferramenta sugere quantidade de itens a produzir); ferramenta de análise lendo o Moodle, dentro de um sistema de design integrado maior (dependente de um orientando de Computação).
- Combinados: Elton envia o link da v2 para a Aline testar e detalhar feedback de visual/nomenclatura/interação; Aline + Rute conduzem o teste de usabilidade; Aline disponibiliza o link do artigo/parâmetros como material de apoio dentro da ferramenta.

**Trabalho de código no mesmo dia:**

- `index-cefor-v2.html` (redesign guiado, arquivado desde 2026-06-29) foi **promovido a versão oficial**, substituindo `index-cefor.html` (blocos fixos), que foi movido para `arquivo/`.
- `index.html` criado como **página de entrada/gateway** — lacuna já registrada em `PRODUCT.md` ("Falta atualmente uma página inicial/gateway…"). Herda a identidade visual da calculadora, tem um único CTA ("Iniciar calculadora") para `index-cefor-v2.html`, e detecta via `localStorage` se já existe um curso salvo para avisar o usuário.
- Confirmado por leitura de código que `index-cefor-v2.html` **já cobre** vários pontos discutidos na reunião: fluxo em 3 etapas com modal de atividade, gráfico "equilíbrio por tipo de aprendizagem" (o mesmo tipo de gráfico que a Aline está construindo no mapa de aprendizagem), exportar/importar plano em **JSON** + salvamento automático em `localStorage`, botão **"Carregar curso de exemplo"** (hoje um exemplo único fixo, não uma biblioteca por coordenação), toggle de contexto **MOOC padrão × Híbrido/pesquisa** (oculta Colaboração e Síncrono no modo padrão), e link **"Leia a proposta de pesquisa completa"** no rodapé apontando para o mesmo Google Doc que a Aline compartilhou na reunião.

---

## 4. Decisões tomadas (e por quê)

| # | Decisão | Justificativa |
|---|---|---|
| D1 | **CH total** como saída principal (não "h/semana") | MOOC é autoinstrucional/assíncrono; o que se valida é a CH declarada para certificação |
| D2 | **Tópicos = campo opcional** *(revisado 2026-06-30)* | MOOC usa lógica de tópico/módulo, não semanal; só mostra equivalente por tópico, não é o eixo do modelo |
| D3 | **Sem nível "Média"** onde o Quadro 2 não tem (vídeo, quiz, interativa, discussão) | Lei "No Invention" — só leitura e escrita têm 3 níveis na fonte |
| D4 | **Organização por tipo de aprendizagem (Laurillard)** | é o framework da pesquisa; permite o gráfico de equilíbrio |
| D5 | **Itens dinâmicos** por bloco/atividade | reflete "montar o curso" real (≈ mapa de atividades) |
| D6 | **Manter versões antigas arquivadas** ao trocar a ativa | comparação auditável, retomada fácil (ver `arquivo/`) |
| D7 | **Calibração mantida** (declarada × estimada, ±15%) | é a dor central da pesquisa; diferencial da ferramenta |
| D8 | Ferramenta é **estimador**, não analisador, nesta fase | uso pretendido é durante o planejamento/design, antes do curso existir; comparar com curso pronto é evolução futura |
| D9 | Ferramenta fica **fora da planilha/mapa de atividades** | já validado com a Vanessa: não é documento obrigatório, e precisa servir também quem produz fora do fluxo MOOC padrão |
| D10 | Escopo desta versão é **MOOC**, não genérico para presencial/híbrido | mais fácil validar um nicho específico e generalizar depois (consenso Elton/Marcos, reunião 26/08) |
| D11 | Colaboração é sempre **alta complexidade** (sem opção baixa) | literatura: atividade colaborativa tem carga cognitiva alta pela negociação entre pessoas, independente da complexidade da tarefa |
| D12 | `index-cefor-v2.html` (fluxo guiado, 3 etapas) promovido a versão oficial; `index-cefor.html` (blocos fixos) arquivado | validado ao vivo com Aline/Marcos em 26/08 — o formulário simples alternativo foi rejeitado por UX ruim |

---

## 5. Pendências / próximos passos

### 5.1 Sem solução de design ainda (trazido pela Aline em 26/08)
**Questionário misto** — quando um questionário mistura questões de baixa e alta complexidade, o parâmetro do Quadro 2 (por questão individual) não tem hoje uma forma natural de ser declarado na interface sem forçar o professor a lançar dois itens separados. Precisa virar decisão de produto antes de implementar.

### 5.2 Combinados pendentes de execução

> **2026-09-22 — a rodada de testes aconteceu** (Aline, Rutinelli, Mariella e Bruno, sobre a Opção A). As 32 contribuições, o plano de ajustes em 5 fases e as 17 dúvidas para a reunião estão em `2026-09-22-ANALISE-CONTRIBUICOES-E-PLANO.md`. Isso cumpre os itens 1 e 2 abaixo — o link enviado foi o dos estimadores A e B (§5.5), não o da v2.
>
> **2026-09-23 — Fase 1 do plano aplicada na Opção A** (C1, C2, D1, D2): digitação no modal sem perder o foco, campos numéricos sem setas e com vírgula decimal, quantidade zero bloqueada com aviso, veredito crítico corrigido e nova cor de Prática. A versão anterior está em `arquivo/estimador-carga-horaria-a-2026-09-22.html`.
>
> **2026-09-23 — Fase 2 do plano aplicada na Opção A** (B1 a B6): a Opção A passa a seguir o **Quadro 3**. Tarefas novas "Outros materiais" (Aquisição, tempo do professor), "Enquete ou escolha" (Prática, 15 min) e "Outras práticas" (Prática, tempo do professor); tabela da página inicial com a nota de rodapé e os asteriscos do Quadro 3; interruptor "Curso MOOC" removido — os sete tipos ficam sempre disponíveis, com aviso no modal para discussão, colaboração e síncrona; dicas de vídeo e de atividade interativa, que o Quadro não tem, retiradas; o modal mostra a fonte de cada tempo. As dúvidas da reunião que tocam a fase 2 (B2, B5, B6, H5P) seguiram a proposta do plano e precisam ser confirmadas com a Aline.

1. Enviar o link de `index-cefor-v2.html` para a Aline testar e detalhar feedback (visual, nomenclatura, interação) — combinado em 26/08, ainda não enviado.
2. Aline + Rute vão rodar o teste de usabilidade assim que o link for enviado.
3. Confirmar com a Aline os pontos herdados da sessão anterior: nível "Média" ausente em vídeo/quiz/interativa/discussão (D3) e conversão palavra ↔ página.

### 5.3 Evoluções mapeadas (backlog, não iniciadas)
- Biblioteca de modelos/templates de curso publicados por coordenação (ideia do Marcos, 26/08).
- Fluxo invertido: definir % de mídia desejada → ferramenta sugere quantidade de itens a produzir.
- Ferramenta de análise (ler Moodle, comparar carga estimada × real) — parte de um sistema de design integrado maior, depende de um orientando de Computação.
- Presets adicionais, empacotar fontes em base64 (100% offline), publicar (GitHub Pages) + `<iframe>` no Moodle.

### 5.4 Limpeza de documentação — RESOLVIDA em 2026-09-02
- `README.md` reescrito para descrever os estimadores oficiais como fluxo atual (a descrição do modelo de cálculo da v1 ficou marcada como histórico).
- Duplicata de `COMO ESTIMAR A CARGA HORÁRIA…IFES.md` entre raiz e `docs/`: a cópia da raiz foi removida (era idêntica, só diferia em fim de linha); `docs/` é o local único.
- Reorganização do repositório: estimadores oficiais na raiz, dependências em `assets/`, páginas antigas em `arquivo/`, raiz reduzida ao essencial.

### 5.5 Git e publicação — CONCLUÍDO em 2026-09-02
Reorganização commitada e publicada (`a2c8201`, `origin/main`). No ar e verificado no navegador:

- **Opção A** — https://vertumno.github.io/calculadora-ch-cursos-ead/estimador-carga-horaria-a.html
- **Opção B** — https://vertumno.github.io/calculadora-ch-cursos-ead/estimador-carga-horaria-b.html

Nas duas: logo carrega, pdf.js carrega no `<script>` clássico e no `import()` ESM. Único erro de console é `favicon.ico` 404 (o repositório não tem favicon) — cosmético.

`index.html`, `index-cefor-v2.html` e `calculadora-workload-estimator.html` saíram do site publicado (404, confirmado).

**A raiz do Pages não ficou 404:** sem `index.html`, o Jekyll do GitHub Pages renderiza o `README.md` como página inicial — e ela já traz a tabela com os dois links. Ou seja, https://vertumno.github.io/calculadora-ch-cursos-ead/ funciona como índice sem precisar de página extra. Consequência prática: **o README é uma página pública**, não só documentação interna — escrever pensando nisso.

Links enviados à Aline para escolha entre as duas direções visuais.

---

## 6. Como retomar (resumo de 30s)

1. A **proposta** está em `docs/COMO ESTIMAR…IFES.md` (Quadro 2 = fonte da verdade dos valores).
2. A **calculadora ativa** é `index-cefor-v2.html` (fluxo guiado, 3 etapas); a porta de entrada é `index.html`.
3. A reunião de 26/08 com Aline e Marcos validou esse fluxo ao vivo e fechou o escopo (estimador, MOOC-first, fora da planilha) — ver `docs/transcricao 2026-08-26…txt` e §3.5/§4 acima.
4. **Falta:** resolver o design do questionário misto (§5.1), enviar o link para a Aline testar (§5.2) e, quando sobrar tempo, arrumar a documentação desatualizada (§5.4).
5. Tudo o que não é a versão ativa está em `arquivo/` (v1 e os blocos fixos do Quadro 2) — ver `arquivo/README.md`.
