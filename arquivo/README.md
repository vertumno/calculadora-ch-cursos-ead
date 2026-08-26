# Arquivo — material preservado (não em uso)

> Trabalho concluído e preservado para retomada futura. Decisão: *"salvar, mas não usar agora"*.

## Conteúdo

| Arquivo | O que é |
|---|---|
| `calculadora-workload-estimator.html` | **v1 — porte fiel do Course Workload Estimator** (Wake Forest/Rice), traduzido e com a cara do CEFOR. **Arquivada em 2026-06-30** (decisão: não será mais usada; fica só como referência — as métricas são as do exemplo, não as do Quadro 2 da pesquisa). A URL pública antiga na raiz (`calculadora-workload-estimator.html`) é um **stub de redirect** que aponta para cá. |
| `index-cefor.html` | **Calculadora MOOC fiel ao Quadro 2** (blocos fixos por tipo de aprendizagem, lógica por tópico). Foi a versão ativa até **2026-08-26**, quando o redesign de UX (`index-cefor-v2.html`) assumiu como página oficial. Motor de cálculo idêntico à v2 (mesmas taxas do Quadro 2). |
| `ANALISE-UX-UI.md` | **Análise UX/UI sênior** que fundamentou o redesign guiado: diagnóstico da v1, personas, princípios, arquitetura da informação, percurso e layout. |

## Como retomar
- Para reativar esta versão (blocos fixos por Quadro 2): mova `index-cefor.html` de volta para a raiz do projeto.
- A análise (`ANALISE-UX-UI.md`) pode voltar para `docs/`.
- Para reativar a v1 (porte Wake Forest): mova `calculadora-workload-estimator.html` de volta para a raiz (substituindo o stub).
- Abrir local: `python -m http.server 8000` na raiz → `http://127.0.0.1:8000/arquivo/index-cefor.html`.

## Versão ativa (fora do arquivo)
- `index-cefor-v2.html` — construtor de atividades guiado (etapas, onboarding, painel-resumo sempre visível, catálogo em modal, exemplo pronto, salvamento automático em localStorage). Motor de cálculo idêntico ao Quadro 2 (validado). **Página oficial do sistema desde 2026-08-26.**
