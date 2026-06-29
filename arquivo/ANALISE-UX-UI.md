# Análise UX/UI — Calculadora de Carga Horária EaD (CEFOR/IFES)

> Análise sênior de experiência e interface + proposta de redesign. Base: `index-cefor.html` (v1 funcional), público e dores da transcrição da reunião (29/06/2026). Entrega associada: `index-cefor-v2.html`.

---

## 1. Quem usa e para quê (o problema real)

**Personas**
- **Professor proponente iniciante** — sem apoio de design instrucional. Da transcrição: *"não sabe nem por onde começar"*. Precisa de **guia, linguagem simples e exemplos**.
- **Designer instrucional / professor experiente** — precisa de **velocidade, controle e edição rápida**.

**Job-to-be-done**
> "Quando planejo ou reviso um curso EaD, quero traduzir as atividades planejadas em **carga horária realista**, para declarar uma CH coerente e equilibrar os tipos de aprendizagem — **sem precisar ser especialista em cálculo**."

**Dor central (transcrição):** ninguém tem parâmetro; erra-se muito a CH (em geral **superestima** e sobrecarrega o aluno). A ferramenta precisa **reduzir a discrepância** entre o declarado e o planejado, e **educar** sobre o equilíbrio de tipos de aprendizagem (Laurillard) — sem impor.

---

## 2. Diagnóstico da v1 (heurísticas de Nielsen + carga cognitiva)

| # | Problema | Heurística ferida | Efeito |
|---|---|---|---|
| 1 | Resultado fica no rodapé; ao editar no topo, a carga total some da vista | Visibilidade do status | Usuário perde o feedback do que importa |
| 2 | 10 blocos visíveis ao mesmo tempo, com selects técnicos | Lei de Hick / carga cognitiva | Iniciante **paralisa** ("por onde começo?") |
| 3 | Termos como "300 palavras/min", "complexidade alta" sem ajuda | Reconhecer > recordar | Insegurança, erro de preenchimento |
| 4 | Sem onboarding / ponto de partida | Ajuda e documentação | Abandono no primeiro contato |
| 5 | Sem senso de progresso/conclusão | Visibilidade do status | Não se sabe "o que já fiz e o que falta" |
| 6 | Estrutura espelha o modelo do pesquisador (tipos de Laurillard), não o do professor (atividades concretas) | Correspondência sistema↔mundo real | Atrito conceitual |
| 7 | Scroll longo entre entrada e feedback | Visibilidade / proximidade | Quebra o ciclo ação→resultado |
| 8 | Mobile: 10 cards empilhados | — | Scroll infinito, sem prioridade |

---

## 3. Princípios do redesign

1. **Visão geral sempre visível** — painel-resumo persistente (sticky) com **carga total, calibração, equilíbrio e próximo passo**. Responde a "o que já fiz e o que falta" a todo instante.
2. **Progressive disclosure** — uma decisão por vez; complexidade sob demanda. Adicionar atividade é um ato simples; os detalhes aparecem no card.
3. **Modelo mental do usuário** — adicionar **atividades concretas** (Leitura, Vídeo, Quiz…). O **tipo de aprendizagem (Laurillard)** é mostrado como *consequência* (selo no card + barra de equilíbrio), educando sem obrigar.
4. **Feedback imediato e próximo** — toda ação atualiza o painel na hora; defaults fazem o card já nascer com um tempo calculado (ensina a relação parâmetro→carga).
5. **Linguagem clara + ajuda contextual** — microcopy simples, descrição em cada tipo, taxa exibida ("≈ 300 palavras/min").
6. **Guia explícito** — barra de **3 etapas** (Configurar · Atividades · Calibrar) + **"próximo passo sugerido"** dinâmico.
7. **Reduzir esforço** — **exemplo pronto** ("carregar curso de exemplo"), defaults sensatos, edição inline, e **salvar automático** (localStorage) para não perder o trabalho.
8. **Acessível e responsivo** — foco visível, ESC/clique-fora fecham modal, `prefers-reduced-motion`, painel vira faixa fixa no mobile.

---

## 4. Arquitetura da informação e percurso

```
ETAPA 1 — Configurar        ETAPA 2 — Construir            ETAPA 3 — Calibrar/Concluir
nome do curso               + Adicionar atividade           CH declarada × estimada
contexto MOOC/híbrido   →   (catálogo por tipo de       →   veredito (Realista/Sub/Super)
(CH pretendida)             aprendizagem) → cards            equilíbrio + exportar
```

O painel-resumo (direita) acompanha as 3 etapas o tempo todo: carga total, progresso, equilíbrio, próximo passo.

---

## 5. Layout proposto

**Duas colunas (desktop):**
- **Construtor (esquerda, ~1fr)** — nome do curso editável + contexto + etapas; banner de onboarding dismissível; botão **"+ Adicionar atividade"** que abre um **catálogo** (modal) com os 10 tipos agrupados por tipo de aprendizagem, cada um com ícone + 1 linha de descrição; **linha do tempo de atividades** (cards editáveis inline com tempo calculado, remover/duplicar).
- **Painel-resumo (direita, sticky ~380px)** — **Carga total** (número grande) + equiv./semana; **Calibração** (input + veredito); **Equilíbrio por tipo de aprendizagem** (barra + "X/7 tipos"); **Distribuição** Individual/Social/Síncrono; **Próximo passo sugerido**; ações (imprimir/PDF, limpar).

**Mobile:** empilha; painel essencial vira **faixa fixa inferior** (carga total + abrir resumo).

---

## 6. Microinterações (refinadas, com `prefers-reduced-motion`)
- Reveal escalonado no load; card de atividade entra com slide+fade; carga total faz *count-up*; barra de equilíbrio anima largura; veredito troca de cor suavemente.

## 7. Sistema visual (mantido da marca, elevado)
- **Cor:** verde IFES dominante; **vermelho só para alerta/veredito**; cores por **macro-tipo** — Individual = verdes, Social = roxos, Síncrono = âmbar (dá significado à barra de equilíbrio).
- **Tipografia:** Archivo (display) + Hanken Grotesk (corpo) + JetBrains Mono (números) — trio distintivo e já institucional; coerência de marca > novidade.
- **Ícone por tipo** de atividade (SVG line) para reconhecimento rápido.

---

## 8. O que muda na prática (v1 → v2)

| Aspecto | v1 (`index-cefor.html`) | v2 (`index-cefor-v2.html`) |
|---|---|---|
| Mentalidade | 10 blocos por tipo de aprendizagem | "Adicionar atividade" concreta; Laurillard como consequência |
| Resultado | no rodapé | painel-resumo **sempre visível** (sticky) |
| Guia | nenhum | etapas + onboarding + próximo passo + exemplo |
| Ajuda | selects técnicos | descrição + taxa por tipo, microcopy |
| Persistência | nenhuma | **salva automático** (localStorage) |
| Conclusão | sem senso de progresso | etapas marcadas + "X/7 tipos" + veredito |

> **Não muda:** a base de cálculo (Quadro 2) permanece idêntica e validada (16/16). O redesign é de **experiência**, não de fórmula.
