# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users

Designers instrucionais e professores do CEFOR (Centro de Referência em Formação e em Educação a Distância — IFES) que precisam dimensionar a carga horária de cursos MOOC antes de submetê-los para certificação.

## Product Purpose

Estimar quantas horas um curso MOOC realmente demanda do estudante, a partir das atividades planejadas (organizadas pelos tipos do *Conversational Framework* de Laurillard), e calibrar essa estimativa contra a carga horária declarada do curso — evitando super/subestimar o esforço exigido do aluno.

## Positioning

Fiel ao "Quadro 2" da proposta de pesquisa (Aline Amorim et al.), com taxas específicas por tipo de atividade (leitura, vídeo, questionário, produção escrita, discussão etc.) e organização pelos tipos de aprendizagem de Laurillard — não é uma calculadora genérica de carga horária semanal, é desenhada para a lógica de tópico/módulo de um MOOC.

## Operating Context

Página única HTML/CSS/JS autocontida (`index-cefor.html`), sem build/back-end, usada localmente (duplo clique) ou via servidor simples; planejada para publicação futura (GitHub Pages) e incorporação via `<iframe>` no Moodle/AVA. Uso interno de design instrucional, em sessões de refino iterativo com a pesquisadora (Aline).

## Capabilities and Constraints

- Sem framework/build; todo cálculo roda no navegador.
- Única dependência externa: Google Fonts (Archivo, Hanken Grotesk, JetBrains Mono), com fallback gracioso para fontes de sistema se offline.
- Logo IFES recriado 100% em CSS (não depende de arquivo de imagem).
- Falta atualmente uma página inicial/gateway antes de entrar na calculadora — é o objeto deste trabalho.

## Brand Commitments

Identidade visual oficial IFES/CEFOR: símbolo IF (grade 3×4 de quadrados verdes + 1 círculo vermelho) recriado em CSS; paleta verde IF `#3da63d` (+ tons), vermelho IF `#e2211c` reservado para alerta/veredito; tipografia Archivo (títulos/números), Hanken Grotesk (corpo), JetBrains Mono (leituras numéricas). Lockup de marca: "INSTITUTO FEDERAL / Espírito Santo / Centro de Referência em Formação e em Educação a Distância".

## Evidence on Hand

Base teórica documentada em `docs/COMO ESTIMAR A CARGA HORÁRIA…IFES.md` (Quadro 2 + Laurillard 2012) e `docs/ESTADO-E-PROXIMOS-PASSOS.md`. Pesquisa e design: Aline Amorim, Vanessa Battestin, Marize Passos, Elton Silva e Marcos Accioly, com base em McInnes et al. (2026), Liu e Evans (2020) e Beer (2019). Nenhuma imagem de produto/depoimento real disponível para a home — não fabricar.

## Product Principles

- Fidelidade ao Quadro 2 da pesquisa acima de convenções genéricas de UX (Lei "No Invention").
- Ferramenta de uso interno e pontual — a home deve ser uma porta de entrada rápida, não uma landing page de marketing.
- Identidade visual IFES/CEFOR é não-negociável e já está resolvida na calculadora; a home reaproveita, não reinventa.
- Sem build/back-end: qualquer nova página segue o mesmo padrão HTML/CSS/JS autocontido.
