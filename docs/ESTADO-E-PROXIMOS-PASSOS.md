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

```
calculadora-ch-cursos-ead/
├── index.html                   # PORTA DE ENTRADA (gateway) → leva a index-cefor-v2.html — criado 2026-08-26
├── index-cefor-v2.html          # CALCULADORA ATIVA — construtor de atividades guiado (3 etapas) ← ÚNICA VERSÃO ATIVA
├── calculadora-workload-estimator.html   # STUB de redirect → arquivo/ (preserva a URL pública antiga da v1)
├── README.md                   # doc da v1 — DESATUALIZADO, ver nota de limpeza em §5.4
├── PRODUCT.md                  # ficha de produto (plataforma, usuários, positioning, princípios)
├── design-logo-cefor.md        # notas de identidade visual
├── cefor-horizontal-cor.png / icone_cefor-horizontal-cor.png   # logos de referência (não usados pelo HTML; logo é CSS)
├── COMO ESTIMAR A CARGA HORÁRIA…IFES.md   # cópia na raiz — duplicata do arquivo em docs/, ver §5.4
├── Revisão e ajustes da calculadora de carga horária.md   # feedback formal da Aline (revisão 2026-06-30)
├── assets/                      # logos de referência (não usados; logo é CSS)
├── arquivo/                     # MATERIAL ARQUIVADO (preservado, não em uso)
│   ├── README.md                # inventário do arquivo (atualizado em 2026-08-26)
│   ├── calculadora-workload-estimator.html  # v1 — porte do Workload Estimator (arquivada 2026-06-30)
│   ├── index-cefor.html         # blocos fixos por Quadro 2 — arquivada 2026-08-26 (v2 assumiu como oficial)
│   └── ANALISE-UX-UI.md         # análise UX/UI que fundamentou o redesign guiado
└── docs/
    ├── COMO ESTIMAR A CARGA HORÁRIA…PROPOSTA…IFES.md   # A PROPOSTA (Quadro 2 + Laurillard)
    ├── COMPARATIVO_calculadora-atual-vs-proposta-cefor.md  # comparativo v1 × proposta (histórico)
    ├── ESTADO-E-PROXIMOS-PASSOS.md                      # ESTE arquivo
    ├── transcrição 2026-06-29 - Reuniao MOOC…txt         # racional das decisões da 1ª reunião
    ├── transcricao 2026-08-26 - Reunião…Aline Amorim Marquito e Elton.txt   # reunião de alinhamento (§3.5)
    └── source/                  # código original R/Shiny (server.R, ui.R) — referência
```

> **Nota de versões:** a **porta de entrada** é `index.html` (novo, 2026-08-26), que leva à **única calculadora ativa**, `index-cefor-v2.html` — construtor de atividades guiado em 3 etapas (Configurar → Atividades → Calibrar), **promovido a versão oficial em 2026-08-26**. O antigo `index-cefor.html` (fiel ao Quadro 2 em blocos fixos, que era a versão ativa desde 06/2026) foi **arquivado na mesma data** — o motor de cálculo é idêntico entre as duas, só a interface mudou. A v1 (`calculadora-workload-estimator.html`, porte do Workload Estimator) segue arquivada desde 2026-06-30; a URL pública antiga na raiz continua um **stub de redirect**. Para retomar qualquer versão arquivada, ver `arquivo/README.md`.

> **Pendência de limpeza (não bloqueante):** `README.md` na raiz ainda descreve majoritariamente a v1 arquivada (mesmo com o aviso no topo apontando para este documento), e há uma cópia duplicada de `COMO ESTIMAR A CARGA HORÁRIA…IFES.md` entre a raiz e `docs/`. Ver §5.4.

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
1. Enviar o link de `index-cefor-v2.html` para a Aline testar e detalhar feedback (visual, nomenclatura, interação) — combinado em 26/08, ainda não enviado.
2. Aline + Rute vão rodar o teste de usabilidade assim que o link for enviado.
3. Confirmar com a Aline os pontos herdados da sessão anterior: nível "Média" ausente em vídeo/quiz/interativa/discussão (D3) e conversão palavra ↔ página.

### 5.3 Evoluções mapeadas (backlog, não iniciadas)
- Biblioteca de modelos/templates de curso publicados por coordenação (ideia do Marcos, 26/08).
- Fluxo invertido: definir % de mídia desejada → ferramenta sugere quantidade de itens a produzir.
- Ferramenta de análise (ler Moodle, comparar carga estimada × real) — parte de um sistema de design integrado maior, depende de um orientando de Computação.
- Presets adicionais, empacotar fontes em base64 (100% offline), publicar (GitHub Pages) + `<iframe>` no Moodle.

### 5.4 Limpeza de documentação (dívida, não bloqueante)
- `README.md` na raiz ainda descreve principalmente a v1 arquivada — reescrever para refletir `index.html` → `index-cefor-v2.html` como fluxo atual.
- Duplicata de `COMO ESTIMAR A CARGA HORÁRIA…IFES.md` entre a raiz e `docs/` — unificar em um único local.

### 5.5 Git
`index.html` (novo) e `index-cefor-v2.html` (modificado) estão **untracked/não commitados**, junto com vários documentos novos (`PRODUCT.md`, as duas transcrições, imagens de logo, este arquivo). Há também um arquivo antigo, `docs/transcrição da Reuniao MOOC 29-06-2026…txt`, marcado como **deletado** no working tree — confirmar se é intencional (parece ter sido substituído por `docs/transcrição 2026-06-29…txt`, que já está no repositório) antes de commitar. Quando autorizado: revisar `git status` com atenção e commitar; *push é exclusivo do @devops*.

---

## 6. Como retomar (resumo de 30s)

1. A **proposta** está em `docs/COMO ESTIMAR…IFES.md` (Quadro 2 = fonte da verdade dos valores).
2. A **calculadora ativa** é `index-cefor-v2.html` (fluxo guiado, 3 etapas); a porta de entrada é `index.html`.
3. A reunião de 26/08 com Aline e Marcos validou esse fluxo ao vivo e fechou o escopo (estimador, MOOC-first, fora da planilha) — ver `docs/transcricao 2026-08-26…txt` e §3.5/§4 acima.
4. **Falta:** resolver o design do questionário misto (§5.1), enviar o link para a Aline testar (§5.2) e, quando sobrar tempo, arrumar a documentação desatualizada (§5.4).
5. Tudo o que não é a versão ativa está em `arquivo/` (v1 e os blocos fixos do Quadro 2) — ver `arquivo/README.md`.
