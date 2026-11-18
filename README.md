# Estimador de Carga Horária de Cursos EaD — IFES / CEFOR

Ferramenta web que estima **quanto tempo um curso a distância realmente exige do estudante** a partir das atividades planejadas, e ajuda a **validar se a carga horária declarada é realista**. Uso interno de design instrucional do CEFOR (Centro de Referência em Formação e em Educação a Distância — IFES).

## Versões publicadas

**Link oficial: <https://links.ifes.edu.br/estimador-cefor>** — leva à Opção A. É o link a divulgar.

Duas versões oficiais, ambas na raiz do repositório e ambas publicadas no GitHub Pages:

| Arquivo | O que é | URL |
|---|---|---|
| **Opção A** — `estimador-carga-horaria-a.html` | Direção visual editorial | [/estimador-carga-horaria-a.html](https://vertumno.github.io/calculadora-ch-cursos-ead/estimador-carga-horaria-a.html) |
| **Opção B** — `estimador-carga-horaria-b.html` | Direção visual brutalista | [/estimador-carga-horaria-b.html](https://vertumno.github.io/calculadora-ch-cursos-ead/estimador-carga-horaria-b.html) |

> A raiz do Pages não tem `index.html` — use as URLs acima. Toda a linhagem anterior (a porta de entrada `index.html`, a calculadora guiada `index-cefor-v2.html`, os blocos fixos `index-cefor.html` e a v1 `calculadora-workload-estimator.html`) está preservada em `arquivo/` e **não** é publicada.

Para o estado atual do projeto e os próximos passos, ver **`docs/ESTADO-E-PROXIMOS-PASSOS.md`**.

## Novidades da Opção A — ajustes da rodada de testes (setembro de 2026)

A **Opção A** recebeu os ajustes pedidos na rodada de testes de 22/09/2026 (Aline, Rutinelli, Mariella e Bruno) e passou a seguir o **Quadro 3**. A **Opção B** continua como estava em 02/09. O plano completo, com as 32 contribuições, está em `docs/2026-09-22-ANALISE-CONTRIBUICOES-E-PLANO.md`.

**O que mudou:**

- **Correções:** os campos de quantidade aceitam a digitação inteira (antes, "1200" virava "1") e vírgula decimal ("7,5"). A atividade só pode ser adicionada com quantidade maior que zero. O veredito agora fala da carga declarada: abaixo da meta, "superestimada"; acima, "subestimada". Prática ganhou cor própria.
- **Quadro 3:** tarefas novas "Outros materiais" (Aquisição), "Enquete ou escolha" (Prática, 15 min) e "Outras práticas" (Prática). O interruptor "Curso MOOC" saiu: os sete tipos ficam sempre disponíveis, com aviso no modal para discussão, colaboração e síncrona. O modal mostra a fonte de cada tempo.
- **Textos:** página inicial com os textos revisados, metodologia em uma seção só, crédito do desenvolvimento técnico e o bloco "Uma estimativa, não uma medida exata".
- **Orientação:** o quadro "Ainda não tenho o material pronto" fica no topo da lista, com itens sobre materiais mistos e materiais complementares.
- **Recursos novos:** alerta (que não bloqueia) para mídia acima de 20 min e leitura acima de 1 h, lista das cinco atividades que mais pesam, aviso quando a meta passa de 60 h e botão **PDF** com a versão de impressão da análise.

**A confirmar com a equipe:** onde havia dúvida, valeu a proposta do plano (§5): enquete com 15 min fixos, síncrona liberada com aviso, vídeo e atividade interativa só com "Baixa" e "Alta", critério do H5P, local do bloco da estimativa, campo de meta livre com aviso acima de 60 h, e só a lista no lugar do gráfico individual × social.

**Ainda não feito, por depender de insumo da equipe:** separar o tempo em conteúdo, prática e avaliação (falta definir o que conta como avaliação); trocar os cursos de exemplo, montados no desenvolvimento, por um curso real (faltam os dados); e o formulário "Dúvidas e dificuldades" (falta criar o formulário e definir o e-mail que recebe as respostas).

---

## 1. O que é / para quem

| | |
|---|---|
| **Público** | Equipe / designers instrucionais e professores do CEFOR |
| **Objetivo** | Dimensionar e calibrar a carga horária de cursos EAD/MOOC |
| **Pergunta que responde** | "Quanto tempo o meu curso *realmente* exige do aluno por semana — e a carga declarada bate com isso?" |

---

## 2. Como usar

1. Abra um dos dois estimadores (link acima) ou, localmente, o `.html` correspondente. Para uso local, prefira servir por HTTP (seção 7) — a importação de PDF depende de arquivos em `assets/` e não funciona bem via `file://`.
2. Descreva as atividades do curso. Cada uma mostra sua contribuição ao vivo em horas.
3. Leia o resultado: carga total, divisão entre estudo autônomo e tempo de contato, e a composição por tipo de atividade.
4. Informe a **carga declarada** para receber o veredito de calibração.

---

## 3. Como funciona (modelo de cálculo) — descrição da v1, histórico

> As seções 3 a 6 descrevem a **v1 arquivada** (`arquivo/calculadora-workload-estimator.html`). O motor de cálculo dos estimadores oficiais deriva da proposta em `docs/COMO ESTIMAR A CARGA HORÁRIA…IFES.md` (Quadro 2), não desta modelagem por blocos. Mantidas como referência da origem das taxas.

A ferramenta soma a carga de **8 categorias de atividade** e gera três totais semanais, além da carga total do curso.

**Blocos de entrada:**

| Bloco | Entradas principais |
|---|---|
| §01 Curso | Duração em semanas (rege toda a distribuição) |
| §02 Leitura | Páginas/semana, densidade, nível conceitual, objetivo |
| §03 Escrita | Páginas no curso, densidade, gênero, nível de elaboração |
| §04 Vídeo/Áudio | Horas/semana |
| §05 Fóruns | Postagens/semana, formato (texto ou áudio/vídeo), tamanho |
| §06 Avaliações | Provas, horas de estudo, prova cronometrada |
| §07 Outras atividades | Quantidade, horas, se é mediada (tutoria) |
| §08 Síncrono | Encontros/semana, duração |

**Saídas:**

- **Total / semana** — tempo total do estudante.
- **Autônomo / semana** — estudo independente.
- **Contato / semana** — tempo mediado (tutoria, fóruns, síncrono).
- **Carga horária total do curso (h)** = total semanal × nº de semanas *(adaptação para o contexto brasileiro)*.
- **Composição da carga** — barra + legenda mostrando o peso de cada categoria.
- **Calibração** — compara o estimado com a carga declarada (tolerância ±15%).

---

## 4. Base de cálculo e fidelidade

As **taxas e fórmulas são derivadas do _Course Workload Estimator_** de **Betsy Barre, Allen Brown e Justin Esarey** (Wake Forest University / Rice University), licenciado sob **CC BY-NC-SA 4.0**.

- As duas matrizes de pesquisa (ritmo de **leitura** 3×3×3 e **escrita** 2×3×3) foram **portadas fielmente** do `docs/source/server.R` original (em R/Shiny) para JavaScript e validadas célula a célula.
- A lógica garante `Autônomo + Contato = Total` (para fóruns de texto).
- **Quirk preservado do original:** para fóruns em **áudio/vídeo**, o *Total* usa `0,18·X + X/6` enquanto *Contato* e o valor exibido usam `X/3` (X = minutos × postagens). Mantido por fidelidade à pesquisa; candidato a unificação futura.

O código-fonte original em R/Shiny está preservado em **`docs/source/`** (`server.R`, `ui.R`) para referência.

---

## 5. Stack técnica

- **Página única autocontida** — HTML + CSS + JavaScript puro, sem build, sem framework, sem backend. Todo o cálculo roda no navegador.
- **Sem dependência de imagens** — o logo IFES/CEFOR é **recriado 100% em CSS** (não depende de arquivo).
- **Única dependência externa:** fontes via Google Fonts CDN (Archivo, Hanken Grotesk, JetBrains Mono). Sem internet, recai em fontes do sistema sem quebrar.

---

## 6. Identidade visual e UX

**Marca IFES/CEFOR:**
- Símbolo IF recriado em CSS (grade 3×4 de quadrados verdes + 1 círculo vermelho, no padrão oficial) e lockup "INSTITUTO FEDERAL / Espírito Santo / Centro de Referência em Formação e em Educação a Distância".
- Paleta oficial: verde IF `#3da63d` (+ tons profundos), vermelho IF `#e2211c` usado **só para alerta/veredito** (espelhando o único ponto vermelho do logo), preto e branco.
- Tipografia: **Archivo** (títulos/números), **Hanken Grotesk** (corpo), **JetBrains Mono** (leituras numéricas).
- Motivo recorrente: grade de pixels da marca, reinterpretada como "grade de medição".

**UX inteligente dos blocos:**
- Cada bloco mostra sua **contribuição ao vivo** (`X h/sem`) e **acende em verde** quando ativo.
- Estado **"incompleto" (âmbar)**: bloco com quantidade definida mas sem horas → aviso explicando o que falta (evita resultado errado silencioso).
- **Barra de composição** da carga semanal, com legenda ordenada da maior para a menor contribuição.
- **Calibração** com veredito visual: Realista (verde) / Subdimensionada (vermelho) / Superdimensionada (âmbar).
- **Acessibilidade:** respeita `prefers-reduced-motion` sem esconder conteúdo (estados de repouso são sempre visíveis; animação só enriquece).

---

## 7. Rodar / hospedar

**Servidor local** (recomendado — a importação de PDF precisa disso):
```bash
python -m http.server 8000
# http://localhost:8000/estimador-carga-horaria-a.html
# http://localhost:8000/estimador-carga-horaria-b.html
```

**Publicação:** o GitHub Pages serve a **raiz do branch `main`**. Qualquer arquivo commitado na raiz vira público — por isso os estimadores ficam lá e as versões aposentadas ficam em `arquivo/`. Para incorporar no Moodle/AVA, usar um `<iframe>` apontando para a URL publicada.

**Caminhos:** os estimadores carregam `./assets/vendor/pdfjs/…` e `assets/cefor-horizontal-cor-web.png`. Se um `.html` for movido de diretório, esses caminhos precisam ser reajustados junto.

---

## 8. Estrutura de arquivos

```
calculadora-ch-cursos-ead/
├── estimador-carga-horaria-a.html    # Opção A — direção editorial   (publicado)
├── estimador-carga-horaria-b.html    # Opção B — direção brutalista  (publicado)
├── README.md                         # este documento
├── PRODUCT.md                        # ficha de produto
├── assets/                           # o que as páginas carregam + material de marca
│   ├── vendor/pdfjs/                 # pdf.js embarcado (importação de PDF)
│   ├── cefor-horizontal-cor-web.png  # logo usada pelos estimadores
│   ├── cefor-horizontal-cor.png      # logo oficial em alta — referência
│   ├── icone_cefor-horizontal-cor.png# ícone oficial — referência
│   └── hero-proposta-editorial.svg
├── arquivo/                          # versões aposentadas (preservadas, não publicadas em uso)
│   ├── README.md                     # inventário do arquivo
│   ├── index-gateway.html            # ex-index.html — porta de entrada aposentada
│   ├── index-cefor-v2.html           # calculadora guiada em 3 etapas
│   ├── index-cefor.html              # blocos fixos por Quadro 2
│   ├── calculadora-workload-estimator.html   # v1 — porte do Workload Estimator
│   └── ANALISE-UX-UI.md
└── docs/                             # proposta, transcrições, design, estado do projeto
    └── source/                       # código original R/Shiny (server.R, ui.R)
```

---

## 9. Histórico do que já foi feito

1. **Análise do sistema original** (`docs/source/ui.R` + `docs/source/server.R`) — _Course Workload Estimator_ em R/Shiny.
2. **Reescrita** como página única HTML/CSS/JS, em português, adaptada ao contexto EAD/MOOC brasileiro, mantendo as taxas de pesquisa originais (validadas).
3. **Adaptações próprias:** cálculo da carga horária total do curso e comparador estimado × declarado.
4. **Identidade visual IFES/CEFOR** aplicada (cores, tipografia, símbolo da marca).
5. **UX inteligente dos blocos:** contribuição ao vivo, estados aceso/vazio/incompleto, barra de composição da carga.
6. **Correção de acessibilidade** (`prefers-reduced-motion` não esconde mais logo/blocos).
7. **Logo recriado 100% em CSS** (HTML autocontido), com o símbolo no padrão oficial e o lockup em duas linhas na descrição.
8. **Migração** do projeto para este repositório (`vertumno/calculadora-ch-cursos-ead`).

---

## 10. Próximos passos sugeridos

- [ ] Confirmar a Opção A como versão única e arquivar a Opção B.
- [x] Rodada de testes com a equipe (22/09/2026) e ajustes na Opção A.
- [ ] Confirmar as propostas adotadas e trazer os insumos que faltam (curso real, critério de avaliação, formulário).
- [ ] Empacotar fontes para funcionamento 100% offline.
- [ ] Gerar `<iframe>` para o Moodle/AVA a partir da URL publicada.

Backlog detalhado em `docs/ESTADO-E-PROXIMOS-PASSOS.md` §5.

---

## Créditos e licença

Lógica e taxas baseadas no **Course Workload Estimator** de Betsy Barre, Allen Brown e Justin Esarey (Wake Forest / Rice University), sob **[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)**. Versão em português adaptada ao contexto EAD/MOOC — IFES / CEFOR, uso interno de design instrucional.
