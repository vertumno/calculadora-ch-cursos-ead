# Arquivo — material preservado (não em uso)

> Trabalho concluído e preservado para retomada futura. Decisão: *"salvar, mas não usar agora"*.
> Nada aqui é publicado no GitHub Pages — o Pages serve a raiz do repositório, e esta pasta está fora do fluxo.

## Conteúdo

| Arquivo | O que é |
|---|---|
| `estimador-carga-horaria-a-2026-09-22.html` | **Opção A como estava na rodada de testes de 22/09/2026** (Aline, Rutinelli, Mariella e Bruno), salva antes dos ajustes do plano `docs/2026-09-22-ANALISE-CONTRIBUICOES-E-PLANO.md`. Cópia fiel, só com os caminhos de `assets/` trocados por `../assets/` para abrir desta pasta. Usa a mesma chave de rascunho no navegador que os estimadores da raiz. |
| `index-gateway.html` | **Porta de entrada (gateway)** criada em 2026-08-26: nomeava a ferramenta e levava, com um único botão, à calculadora guiada. Era o `index.html` da raiz. **Aposentado em 2026-09-02**, quando os estimadores oficiais passaram a ser abertos diretamente. O link interno aponta para `index-cefor-v2.html`, que está nesta mesma pasta — continua funcionando. |
| `index-cefor-v2.html` | **Calculadora guiada em 3 etapas** (Configurar → Atividades → Calibrar): onboarding, painel-resumo sempre visível, catálogo em modal, exemplo pronto, salvamento automático em `localStorage`. Foi a página oficial de 2026-08-26 até 2026-09-02, quando os `estimador-carga-horaria*.html` assumiram. Motor de cálculo do Quadro 2 (validado). |
| `index-cefor.html` | **Calculadora MOOC fiel ao Quadro 2** (blocos fixos por tipo de aprendizagem, lógica por tópico). Foi a versão ativa até **2026-08-26**. Motor de cálculo idêntico ao da v2 (mesmas taxas do Quadro 2). |
| `calculadora-workload-estimator.html` | **v1 — porte fiel do Course Workload Estimator** (Wake Forest/Rice), traduzido e com a cara do CEFOR. **Arquivada em 2026-06-30**: as métricas são as do exemplo original, não as do Quadro 2 da pesquisa. Fica só como referência. |
| `ANALISE-UX-UI.md` | **Análise UX/UI sênior** que fundamentou o redesign guiado: diagnóstico da v1, personas, princípios, arquitetura da informação, percurso e layout. |

## Como retomar

- Para reativar qualquer uma destas páginas, mova o `.html` de volta para a raiz do projeto — é a raiz que o GitHub Pages publica.
- Estas páginas são autocontidas (logo em CSS, sem dependência de `assets/`), então voltar para a raiz basta. Os estimadores oficiais, ao contrário, dependem de `assets/vendor/pdfjs/` e `assets/cefor-horizontal-cor-web.png` e não podem ser movidos sem reajustar esses caminhos.
- A análise (`ANALISE-UX-UI.md`) pode voltar para `docs/`.
- Abrir local: `python -m http.server 8000` na raiz → `http://127.0.0.1:8000/arquivo/index-cefor-v2.html`.

## Versões ativas (fora do arquivo)

- `estimador-carga-horaria-a.html` — **Opção A**, direção visual editorial.
- `estimador-carga-horaria-b.html` — **Opção B**, direção visual brutalista.

Ambas na raiz do repositório e publicadas no GitHub Pages. Ver `README.md` e `docs/ESTADO-E-PROXIMOS-PASSOS.md`.
