# Arquivo — material preservado (não em uso)

> Trabalho concluído e **arquivado em 2026-06-29**. Não está em uso ativo, mas foi preservado para retomada futura. Decisão: *"salvar, mas não usar agora"*.

## Conteúdo

| Arquivo | O que é |
|---|---|
| `calculadora-workload-estimator.html` | **v1 — porte fiel do Course Workload Estimator** (Wake Forest/Rice), traduzido e com a cara do CEFOR. **Arquivada em 2026-06-30** (decisão: não será mais usada; fica só como referência — as métricas são as do exemplo, não as do Quadro 2 da pesquisa). A URL pública antiga na raiz (`calculadora-workload-estimator.html`) é um **stub de redirect** que aponta para cá. |
| `index-cefor-v2.html` | **Redesign de UX** da calculadora — versão guiada com construtor de atividades + painel-resumo sempre visível, etapas, onboarding, exemplo pronto e salvamento automático (localStorage). Motor de cálculo idêntico ao Quadro 2 (validado). Nome aplicado: "Calculadora de Carga Horária para cursos EaD". |
| `ANALISE-UX-UI.md` | **Análise UX/UI sênior** que fundamentou o redesign: diagnóstico da v1, personas, princípios, arquitetura da informação, percurso e layout. |

## Como retomar
- Para reativar o redesign: mova `index-cefor-v2.html` de volta para a raiz do projeto.
- A análise (`ANALISE-UX-UI.md`) pode voltar para `docs/`.
- Para reativar a v1: mova `calculadora-workload-estimator.html` de volta para a raiz (substituindo o stub).
- Abrir local: `python -m http.server 8000` na raiz → `http://127.0.0.1:8000/arquivo/index-cefor-v2.html`.

## Versão ativa (fora do arquivo)
- `index-cefor.html` — calculadora MOOC fiel ao Quadro 2 (blocos fixos por tipo de aprendizagem). **Única versão em uso.**
