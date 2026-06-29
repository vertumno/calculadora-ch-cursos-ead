# Calculadora de Carga Horária de Cursos EAD — IFES / CEFOR

Ferramenta web que estima **quantas horas por semana** um curso a distância exige do estudante a partir das atividades planejadas, e ajuda a **validar se a carga horária declarada é realista**. Uso interno de design instrucional do CEFOR (Centro de Referência em Formação e em Educação a Distância — IFES).

> **Status:** funcional. Página única autocontida (`calculadora-workload-estimator.html`), pronta para abrir no navegador ou hospedar.

---

## 1. O que é / para quem

| | |
|---|---|
| **Público** | Equipe / designers instrucionais e professores do CEFOR |
| **Objetivo** | Dimensionar e calibrar a carga horária de cursos EAD/MOOC |
| **Pergunta que responde** | "Quanto tempo o meu curso *realmente* exige do aluno por semana — e a carga declarada bate com isso?" |

---

## 2. Como usar

1. Abra **`calculadora-workload-estimator.html`** em qualquer navegador moderno (duplo clique já funciona).
2. Preencha apenas os blocos de atividade que existem no seu curso. Cada bloco **acende** e mostra sua contribuição em `h/semana`.
3. Leia o resultado: **carga total do curso (h)**, dedicação **por semana**, divisão **Autônomo × Contato** e a **composição** da carga por tipo de atividade.
4. Informe a **carga declarada** do curso para receber o veredito de calibração (Realista / Subdimensionada / Superdimensionada).

> Para hospedar ou incorporar no Moodle/AVA, basta servir o `calculadora-workload-estimator.html` (ver seção 7).

---

## 3. Como funciona (modelo de cálculo)

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

- As duas matrizes de pesquisa (ritmo de **leitura** 3×3×3 e **escrita** 2×3×3) foram **portadas fielmente** do `source/server.R` original (em R/Shiny) para JavaScript e validadas célula a célula.
- A lógica garante `Autônomo + Contato = Total` (para fóruns de texto).
- **Quirk preservado do original:** para fóruns em **áudio/vídeo**, o *Total* usa `0,18·X + X/6` enquanto *Contato* e o valor exibido usam `X/3` (X = minutos × postagens). Mantido por fidelidade à pesquisa; candidato a unificação futura.

O código-fonte original em R/Shiny está preservado em **`source/`** (`server.R`, `ui.R`) e em **`source.zip`** para referência.

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

**Local (simples):** abra `calculadora-workload-estimator.html` no navegador.

**Servidor local (para testar como será servido):**
```bash
python -m http.server 8000
# acesse http://localhost:8000/calculadora-workload-estimator.html
```

**Hospedagem gratuita:** GitHub Pages, Netlify ou similar — basta publicar o `calculadora-workload-estimator.html`. Para incorporar no Moodle/AVA, usar um `<iframe>` apontando para a URL hospedada.

---

## 8. Estrutura de arquivos

```
calculadora-ch-cursos-ead/
├── calculadora-workload-estimator.html                      # A calculadora (página única autocontida)
├── README.md                       # Este documento
├── source/                         # Código-fonte original (R/Shiny) — referência
│   ├── server.R                    # Lógica e matrizes de pesquisa originais
│   └── ui.R                        # Interface original
├── source.zip                      # Pacote original do estimador
├── cefor-horizontal-cor.png        # Logo oficial (referência; NAO usado pelo HTML)
├── icone_cefor-horizontal-cor.png  # Ícone oficial (referência do padrão do símbolo)
└── Meeting Transcription (1).txt   # Transcrição de reunião (insumo/contexto)
```

> Os arquivos `.png` ficam como **referência da marca**; o `calculadora-workload-estimator.html` não depende deles (logo em CSS).

---

## 9. Histórico do que já foi feito

1. **Análise do sistema original** (`source/ui.R` + `source/server.R`) — _Course Workload Estimator_ em R/Shiny.
2. **Reescrita** como página única HTML/CSS/JS, em português, adaptada ao contexto EAD/MOOC brasileiro, mantendo as taxas de pesquisa originais (validadas).
3. **Adaptações próprias:** cálculo da carga horária total do curso e comparador estimado × declarado.
4. **Identidade visual IFES/CEFOR** aplicada (cores, tipografia, símbolo da marca).
5. **UX inteligente dos blocos:** contribuição ao vivo, estados aceso/vazio/incompleto, barra de composição da carga.
6. **Correção de acessibilidade** (`prefers-reduced-motion` não esconde mais logo/blocos).
7. **Logo recriado 100% em CSS** (HTML autocontido), com o símbolo no padrão oficial e o lockup em duas linhas na descrição.
8. **Migração** do projeto para este repositório (`vertumno/calculadora-ch-cursos-ead`).

---

## 10. Próximos passos sugeridos

- [ ] Commit + push dos arquivos migrados (atualmente *untracked*).
- [ ] Presets ("MOOC típico", "Disciplina semestral") para acelerar o preenchimento.
- [ ] Empacotar fontes em base64 para funcionamento 100% offline.
- [ ] Publicar (GitHub Pages) e gerar `<iframe>` para o Moodle/AVA.

---

## Créditos e licença

Lógica e taxas baseadas no **Course Workload Estimator** de Betsy Barre, Allen Brown e Justin Esarey (Wake Forest / Rice University), sob **[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)**. Versão em português adaptada ao contexto EAD/MOOC — IFES / CEFOR, uso interno de design instrucional.
