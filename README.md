# Estimador de Carga Horária de Curso MOOC EaD

Ferramenta web do **Ifes / Cefor** que estima, atividade por atividade, quanto tempo um curso a distância demanda do estudante. Ela ajuda a verificar, ainda no planejamento, se a carga horária declarada do curso é realista.

**Acesse:** <https://links.ifes.edu.br/estimador-cefor>

## O que a ferramenta faz

- Você define a carga horária pretendida do curso (20, 40, 60 h ou outro valor).
- Cadastra as atividades por **tipo de aprendizagem** (aquisição, prática, produção, discussão, investigação, colaboração e síncrona/presencial), tarefa e complexidade. O tempo de cada uma é calculado automaticamente.
- Acompanha em tempo real a carga estimada, o desvio em relação à meta, o equilíbrio por tipo e por módulo e as atividades que mais pesam.
- Salva e restaura o planejamento em arquivo `.json` e exporta a análise em PDF.

Tudo roda no navegador: nenhum dado do planejamento é enviado a servidores.

## Metodologia

Os tipos de aprendizagem seguem o Conversational Framework de Laurillard (2012). Os parâmetros de tempo vêm da pesquisa de doutorado de Aline Pinto Amorim em Design de Aprendizagem de MOOCs, a partir de McInnes et al. (2026), Liu e Evans (2020) e Beer (2019), adaptados ao contexto dos MOOCs do Ifes. A página inicial da ferramenta traz a tabela completa de parâmetros.

O resultado é um **tempo médio esperado**, não uma medida exata do tempo de cada estudante.

## Autoria

- **Pesquisa e concepção:** Aline Pinto Amorim, Vanessa Battestin e Marize Lyra Silva Passos.
- **Desenvolvimento:** Elton Vinicius Silva e Marcos Vinicius Forecchi Accioly.
- **Instituição:** Instituto Federal do Espírito Santo (Ifes) · Centro de Referência em Formação e em Educação a Distância (Cefor).

Dúvidas ou dificuldades no uso: [formulário de dúvidas e dificuldades](https://forms.gle/39MT6RAxNJnEZCSU7).

## Licença

[Creative Commons Atribuição-NãoComercial 4.0 Internacional (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/deed.pt-br). Detalhes e exceções (componentes de terceiros e marcas) em [LICENSE.md](LICENSE.md).

## Como citar

AMORIM, Aline Pinto; BATTESTIN, Vanessa; PASSOS, Marize Lyra Silva; SILVA, Elton Vinicius; ACCIOLY, Marcos Vinicius Forecchi. **Estimador de carga horária de curso MOOC EaD**. Vitória: Ifes/Cefor, 2026. Licenciado sob CC BY-NC 4.0. Disponível em: https://links.ifes.edu.br/estimador-cefor. Acesso em: dia mês ano.

## Rodar localmente

A ferramenta é uma página HTML única, sem instalação nem etapa de compilação. Para que a contagem de palavras de arquivos PDF funcione, sirva a pasta por HTTP:

```bash
python -m http.server 8000
# abra http://localhost:8000/estimador-carga-horaria-a.html
```

## Estrutura

```
estimador-carga-horaria-a.html   # a ferramenta (HTML, CSS e JavaScript em um arquivo)
index.html                       # leva à ferramenta
assets/
  cefor-horizontal-cor-web.png   # logo do Cefor
  og-estimador.png               # imagem de prévia ao compartilhar o link
  vendor/pdfjs/                  # pdf.js, para ler o texto de arquivos PDF
LICENSE.md
```

O nome `estimador-carga-horaria-a.html` deve ser mantido: o link oficial do Ifes aponta para ele.

## Componentes de terceiros

- [pdf.js](https://mozilla.github.io/pdf.js/) (Mozilla), sob Apache-2.0, em `assets/vendor/pdfjs/`.
- Fonte Inter Tight, via Google Fonts, sob SIL Open Font License.
- O tutorial em vídeo é exibido pelo YouTube, carregado só quando o usuário o abre.
