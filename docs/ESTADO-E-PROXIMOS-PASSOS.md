# Estado do projeto e próximos passos — Calculadora de CH MOOC (CEFOR/IFES)

> Documento de retomada. Resume **o que existe**, **o que foi feito**, **as decisões tomadas** e **o que falta**. Última atualização: **2026-06-29**.

---

## 1. O que é o projeto

Ferramenta web para **estimar e validar a carga horária (CH)** de cursos a distância do IFES/CEFOR. Nasceu como porte do *Course Workload Estimator* (Wake Forest/Rice) e está evoluindo para uma **calculadora nativa de MOOC**, baseada na pesquisa de doutorado de **Aline Pinto Amorim** (orient. Vanessa Battestin, co-orient. Marize Lyra Silva Passos).

- **Dor central:** professores não têm parâmetro para estimar CH; erram muito (em geral **superestimam**, sobrecarregando o aluno). Micro-credenciais/MOOCs exigem CH coerente para certificação.
- **Base teórica da proposta:** *Conversational Framework* de **Laurillard (2012)** + rates de **McInnes et al. (2026)**, Liu & Evans (2020), Beer (2019).
- **Decisão estratégica (reunião 29/06):** começar simples — calculadora **separada** (não acoplada ao mapa de atividades), para MOOC, disponível na base de conhecimento. Refino iterativo com a especialista (Aline) em sessões. Publicação em artigo no 2º semestre/2026.

---

## 2. Estrutura de arquivos (atual)

```
calculadora-ch-cursos-ead/
├── index.html                  # v1 — calculadora ATUAL (porte fiel do Workload Estimator)
├── index-mooc.html             # v2 — NOVA calculadora MOOC (proposta CEFOR) ← criada nesta sessão
├── README.md                   # doc da v1
├── docs/
│   ├── COMO ESTIMAR A CARGA HORÁRIA…PROPOSTA…IFES.md   # A PROPOSTA (Quadro 2 + Laurillard)
│   ├── COMPARATIVO_calculadora-atual-vs-proposta-cefor.md  # comparativo v1 × proposta ← criado nesta sessão
│   ├── ESTADO-E-PROXIMOS-PASSOS.md                      # ESTE arquivo
│   ├── transcrição da Reuniao MOOC 29-06-2026….txt     # racional das decisões
│   └── source/                 # código original R/Shiny (server.R, ui.R) — referência
└── assets/                     # logos de referência (não usados; logo é CSS)
```

---

## 3. O que foi feito nesta sessão

### 3.1 Comparativo v1 × proposta
`docs/COMPARATIVO_calculadora-atual-vs-proposta-cefor.md` — lista **todas** as diferenças classificadas em **[+] acrescentadas (8)**, **[~] modificadas (9)** e **[–] retiradas (8)**, mais implicações de implementação e lacunas a resolver.

### 3.2 `index-mooc.html` — nova calculadora (v2)
Página única autocontida (HTML+CSS+JS, sem build/back-end), reaproveitando 100% da identidade visual IFES/CEFOR da v1. **Fiel ao Quadro 2.**

**Modelo de cálculo (tudo em horas, somado na CH total do curso):**

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

**Funcionalidades:**
- **Itens dinâmicos:** o professor adiciona N atividades por bloco (nome opcional + parâmetros + complexidade); cada item mostra seu tempo; o bloco acende e soma.
- **Toggle de contexto:** *MOOC padrão (assíncrono)* esconde/exclui Colaboração e Síncrono (`*`); *Híbrido/pesquisa* os habilita.
- **Saídas:** CH total do curso; macro **Individual × Social × Síncrono**; **equilíbrio por tipo de aprendizagem** (barra + legenda + "N/7 tipos explorados") — atende ao objetivo da pesquisa de mostrar o balanço de Laurillard.
- **Calibração declarada × estimada** mantida (±15% → Realista / Subdimensionada / Superdimensionada).
- **Duração em semanas opcional** (só para mostrar equivalente semanal; o foco é a CH total).
- Limpar tudo / Imprimir-PDF; acessível (`prefers-reduced-motion`); responsivo.

### 3.3 Verificações executadas (tudo passou)
- **Sintaxe JS:** validada via `vm.Script` (Node) — OK.
- **Fidelidade ao Quadro 2:** 16/16 testes numéricos conferidos contra os valores da tabela (leitura, vídeo, quiz, interativa, escrita, discussão, colaboração, síncrono).
- **Não verificado ainda:** render visual em navegador (abrir o arquivo) — ver pendência 5.1.

---

## 4. Decisões tomadas (e por quê)

| # | Decisão | Justificativa |
|---|---|---|
| D1 | **CH total** como saída principal (não "h/semana") | MOOC é autoinstrucional/assíncrono; o que se valida é a CH declarada para certificação |
| D2 | **Semanas = campo opcional** | só serve para mostrar equivalente semanal; não é o eixo do modelo |
| D3 | **Sem nível "Média"** onde o Quadro 2 não tem (vídeo, quiz, interativa, discussão) | Lei "No Invention" — só leitura e escrita têm 3 níveis na fonte |
| D4 | **Organização por tipo de aprendizagem (Laurillard)** | é o framework da pesquisa; permite o gráfico de equilíbrio |
| D5 | **Itens dinâmicos** por bloco | reflete "montar o curso" real (≈ mapa de atividades) |
| D6 | **Manter v1 intacta** e criar v2 separada (`index-mooc.html`) | comparação auditável lado a lado (pedido na reunião) |
| D7 | **Calibração mantida** | é a dor central; não está no Quadro 2, mas é o diferencial da ferramenta |

---

## 5. Pendências / próximos passos

### 5.1 Validar visualmente (rápido)
Abrir `index-mooc.html` no navegador e conferir layout, toggle de contexto, adicionar/remover itens, composição e calibração. *(Não foi possível abrir navegador nesta sessão.)*

### 5.2 Decisões a confirmar com Aline/Vanessa
1. **CH total × h/semana** — confirmar que o foco é a CH total (D1).
2. **Nível "Média" ausente** em vídeo/quiz/interativa/discussão — confirmar que é intencional (D3).
3. **Conversão palavra ↔ página** — oferecer ajuda para quem ainda pensa em páginas?
4. **Contagem de palavras/duração** hoje é manual — automatizar no futuro (mapa de atividades / sala do MOOC).
5. **Calibração "reversa"** (entrar com a CH e a ferramenta sugerir atividades) — evolução futura citada na reunião.

### 5.3 Evoluções já mapeadas (backlog, pós-validação)
- Presets ("MOOC típico"); exportar/compartilhar plano; persistência (localStorage).
- Empacotar fontes em base64 (100% offline); publicar (GitHub Pages) + `<iframe>` p/ Moodle.
- Versões derivadas: outros tipos de curso EAD (não-MOOC), calculadora reversa, integração com mapa.

### 5.4 Git
Arquivos **untracked / não commitados**. Quando autorizado: commitar `index-mooc.html`, o comparativo e este doc. *(push é exclusivo do @devops.)*

---

## 6. Como retomar (resumo de 30s)

1. A **proposta** está em `docs/COMO ESTIMAR…IFES.md` (Quadro 2 = fonte da verdade dos valores).
2. A **nova calculadora** é `index-mooc.html` — fiel ao Quadro 2, validada (16/16).
3. As **diferenças** v1 × proposta estão em `docs/COMPARATIVO_…md`.
4. **Falta:** validar visualmente no navegador e confirmar as 5 decisões (seção 5.2) com a Aline.
5. A **v1** (`index.html`) segue intacta para comparação.
