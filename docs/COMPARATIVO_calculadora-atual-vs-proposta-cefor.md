# Comparativo — Calculadora atual × Proposta CEFOR/IFES

> Diferenças entre a calculadora **já implementada** (`index.html`, porte fiel do *Course Workload Estimator* de Barre/Brown/Esarey, em `docs/source/`) e a **proposta de calculadora para MOOCs do IFES** (`docs/COMO ESTIMAR A CARGA HORÁRIA…md`, Quadro 2, baseada em Laurillard 2012 + McInnes et al. 2026).
>
> Classificação de cada diferença: **[+] ACRESCENTADA** · **[~] MODIFICADA** · **[–] RETIRADA**.

---

## 1. Contexto

| | Calculadora **atual** (`index.html`) | **Proposta** CEFOR/IFES |
|---|---|---|
| **Base teórica** | *Course Workload Estimator* (Betsy Barre, Allen Brown, Justin Esarey — Wake Forest / Rice), CC BY-NC-SA 4.0 | Conversational Framework de **Laurillard (2012)**; rates de **McInnes et al. (2026)**, Liu & Evans (2020), Beer (2019) |
| **Público-alvo do modelo** | Ensino superior presencial/híbrido (genérico) | **MOOCs assíncronos sem tutoria** do IFES (com extensão opcional a híbridos) |
| **Organização das atividades** | Por **mídia/formato** (leitura, escrita, vídeo, fórum, prova, outras, síncrono) | Por **tipo de aprendizagem** (Aquisição, Investigação, Prática, Produção, Discussão, Colaboração) + Síncrono/Presencial |
| **Unidade de medida da leitura/escrita** | **Páginas** (com densidade de palavras/página) | **Palavras** (palavras/minuto e palavras/hora) |
| **Eixos de ajuste** | Matrizes multidimensionais (densidade × objetivo × dificuldade) | **Complexidade única** (Baixa / Média / Alta) |

A diferença **não é cosmética**: muda o *fundamento* do cálculo. A calculadora atual é um tradutor fiel de um modelo norte-americano de carga em sala de aula; a proposta é um modelo **nativo de MOOC** orientado pelo tipo de aprendizagem e pela contagem de palavras (porque "para material digital é difícil fazer com páginas" — reunião 06:10).

---

## 2. A diferença-raiz: mudança de fundamento

```
ATUAL  →  7 blocos por MÍDIA          PROPOSTA  →  6 tipos de APRENDIZAGEM (Laurillard) + Síncrono
─────────────────────────────        ──────────────────────────────────────────────────────────
§02 Leitura          ─┐               AQUISIÇÃO   ├─ Ler (palavras/min)
§04 Vídeo/Áudio      ─┴───────────►              └─ Assistir/Ouvir (× duração da mídia)
                                      INVESTIGAÇÃO ── definida pelo professor          [novo]
§06 Avaliações/Provas ────────────►   PRÁTICA     ├─ Questionário (min/questão)         [novo]
                                                  └─ Atividade Interativa H5P/jogo      [novo]
§03 Escrita          ─┐               PRODUÇÃO    ├─ Escrita (palavras/hora)
§07 Outras atividades─┴───────────►              └─ Artefatos (definido pelo professor)
§05 Fóruns           ─────────────►   DISCUSSÃO   ── simples 30 min / profunda 1,5 h
                                      COLABORAÇÃO ── 2× produção individual (*)         [novo]
§08 Encontros ao vivo─────────────►   SÍNCRONA/PRESENCIAL ── duração do evento (*)
```
`(*)` só se aplica em MOOCs **híbridos / contexto de pesquisa restrito** — MOOCs padrão do IFES são totalmente assíncronos, sem tutoria e sem colaboração/síncrono.

---

## 3. Diferenças detalhadas por categoria

### 3.1 [~] Leitura — de matriz por página para palavras/minuto por complexidade
- **Atual:** entrada em **páginas/semana**; ritmo vindo de matriz **3×3×3** (`READING_RATE`) cruzando *densidade da página* (450/600/750 palavras), *nível conceitual* (nenhum/alguns/muitos conceitos novos) e *objetivo* (sobrevoar/compreender/analisar). Resultado em **páginas/hora** (de 67 até 5).
- **Proposta:** entrada em **palavras**; ritmo por **complexidade única**:
  - Baixa (ideias principais): **300 palavras/min**
  - Média (significado de conceitos): **130 palavras/min**
  - Alta (análise crítica): **70 palavras/min**
- **Impacto:** muda a **unidade de entrada** (página → palavra) e **colapsa 3 eixos em 1**. Justificativa da reunião: páginas variam demais em material digital/HTML; conta-se por palavra.

### 3.2 [~] Vídeo/Áudio — de horas diretas (1×) para múltiplo da duração
- **Atual:** **horas/semana** digitadas diretamente, **sem multiplicador** (1× — o tempo assistido = a carga).
- **Proposta:** tempo = **múltiplo da duração da mídia**, por complexidade:
  - Baixa: **2× a duração** da mídia
  - Alta: **3× a duração** da mídia
- **Impacto:** passa a contabilizar o **tempo de processamento** do aluno (pausas, anotações, repetições). É uma das mudanças de maior efeito numérico.

### 3.3 [+] Questionário (Prática) — novo, por questão
- **Atual:** inexistente como tal (o que mais se aproxima é "§06 Avaliações", em horas de estudo).
- **Proposta:** tempo **por questão**, por complexidade:
  - Baixa (múltipla escolha / baixa complexidade): **2 min/questão**
  - Alta (resposta curta / alta complexidade): **5 min/questão**
- **Impacto:** modelo **nativo de MOOC** (quizzes), substituindo a lógica de "prova + horas de estudo".

### 3.4 [+] Atividade Interativa H5P / jogo (Prática) — nova
- **Atual:** inexistente.
- **Proposta:** Baixa **15 min** · Alta **30 min** por atividade.
- **Impacto:** categoria totalmente nova, específica de objetos interativos de MOOC. A própria proposta reconhece a ausência de referencial teórico forte para esse item.

### 3.5 [~] Escrita (Produção) — de horas/página por matriz para palavras/hora por complexidade
- **Atual:** entrada em **páginas no curso**; ritmo de matriz **2×3×3** (`WRITING_RATE`) cruzando *densidade* (250/500 palavras/página), *nível de elaboração* (sem/mínima/extensa revisão) e *gênero* (reflexão/argumentação/pesquisa). Resultado em **horas/página** (0,75 a 10).
- **Proposta:** entrada em **palavras**; ritmo por **complexidade única**:
  - Baixa (escrita livre/reflexiva): **250 palavras/hora**
  - Média (argumentativa baseada no material): **125 palavras/hora**
  - Alta (baseada em pesquisa do estudante): **60 palavras/hora**
- **Impacto:** muda unidade (página → palavra) e **colapsa densidade + elaboração + gênero** num só eixo de complexidade.

### 3.6 [~] Outras atividades → Artefatos (Produção)
- **Atual:** "§07 Outras atividades" — quantidade × horas por atividade, com checkbox "mediada (tutoria/contato)".
- **Proposta:** **Artefatos** (mídias, apresentações, planos de aula, projetos) — **tempo definido pelo professor** conforme a complexidade.
- **Impacto:** recategorização/renomeação dentro de "Produção"; **remove o conceito de "mediada/contato"** (ver 3.11) e formaliza o campo "definido pelo professor".

### 3.7 [+] Investigação — nova categoria
- **Atual:** inexistente (eventualmente diluída em "Outras").
- **Proposta:** investigação/exploração de um tema, busca e avaliação de informações — **tempo definido pelo professor**.
- **Impacto:** novo tipo de aprendizagem (eixo "Aquisição/Investigação" de Laurillard) que hoje não existe na ferramenta.

### 3.8 [~] Fóruns → Discussão — de fórmula por palavras/minutos para tempo fixo por complexidade
- **Atual:** "§05 Fóruns" — postagens/semana × formato:
  - Texto: `(palavras × posts) / 250`
  - Áudio/vídeo: `0,18·X + X/6` (total) e `X/3` (contato/exibido), X = min × posts
- **Proposta:** tempo **fixo por discussão**, por complexidade:
  - Baixa (discussão simples/livre): **30 min**
  - Alta (discussão profunda, ≥250 palavras, perguntas e respostas): **1,5 h**
- **Impacto:** simplifica radicalmente; **elimina** a fórmula de áudio/vídeo e o *quirk* `0,18X + X/6 ≠ X/3` documentado no README (item 4).

### 3.9 [+] Colaboração — nova categoria condicional (*)
- **Atual:** inexistente.
- **Proposta:** atividades em grupo / avaliação por pares — sempre **complexidade Alta** = **2× o tempo de uma atividade de produção individual**; **tempo definido pelo professor**.
- **Impacto:** novo tipo de aprendizagem social. **Só se aplica em MOOCs híbridos/pesquisa** — em MOOC padrão do IFES, ausente.

### 3.10 [~] Encontros ao vivo → Síncrona/Presencial — reenquadrado e condicional (*)
- **Atual:** "§08 Encontros ao vivo" — encontros/semana × duração (horas). Sempre disponível.
- **Proposta:** "Atividade síncrona **ou presencial**" (aulas, encontros, mentorias, palestras) — **duração do evento**; **condicional (*)** ao contexto híbrido.
- **Impacto:** amplia o escopo para **presencial** (não só webconferência) e marca como **exceção** (não padrão em MOOC).

### 3.11 [–] Avaliações/Provas com "horas de estudo" + prova cronometrada
- **Atual:** "§06 Avaliações" — nº de provas × horas de estudo por prova + opção *take-home* cronometrado (`exam.length` em minutos).
- **Proposta:** **não existe**. O conceito de "prova" com horas de estudo é substituído pelo **Questionário** (3.3, por questão). Não há campo de "horas de estudo por prova" nem de "tempo limite cronometrado".
- **Impacto:** módulo inteiro **retirado/substituído**.

### 3.12 [–] Eixos de ajuste das matrizes (densidade, objetivo, elaboração, gênero)
- **Atual:** leitura usa *densidade da página* + *nível conceitual* + *objetivo*; escrita usa *densidade* + *elaboração* + *gênero*.
- **Proposta:** todos colapsam numa **complexidade única** (Baixa/Média/Alta). Densidade de página, objetivo, nível de elaboração e gênero como *campos separados* **deixam de existir**.
- **Impacto:** simplificação forte da interface; menos cliques, menos precisão "teórica", mais usabilidade.

### 3.13 [~] Saídas: Contato/Tutoria perde sentido no padrão
- **Atual:** três saídas — **Total**, **Autônomo** (independente) e **Contato** (mediado/tutoria: fóruns + síncrono + "outras" mediadas).
- **Proposta:** MOOC do IFES é **totalmente assíncrono e sem tutoria** → a saída **"Contato/semana" tende a zero** no caso padrão (só faz sentido em híbrido/pesquisa).
- **Impacto:** a separação Autônomo × Contato, central na ferramenta atual, **deixa de ser informativa** para o caso de uso principal.

---

## 4. Lista consolidada das diferenças

### [+] ACRESCENTADAS (existem na proposta, não existem hoje)
1. **Questionário** (Prática) — 2 min/questão (baixa) · 5 min/questão (alta).
2. **Atividade Interativa H5P/jogo** (Prática) — 15 min (baixa) · 30 min (alta).
3. **Investigação** — tempo definido pelo professor.
4. **Colaboração** — 2× produção individual, sempre alta complexidade *(condicional, só híbrido)*.
5. **Multiplicador de mídia no vídeo/áudio** — 2×/3× a duração *(hoje é 1× direto)*.
6. **Escala de complexidade unificada** (Baixa/Média/Alta) como eixo único de todas as atividades.
7. **Campos "tempo definido pelo professor"** formalizados (Artefatos, Investigação, Colaboração).
8. **Modelo presencial** explícito (não só webconferência) na atividade síncrona.

### [~] MODIFICADAS (existem em ambos, mas mudam de modelo/valor)
1. **Leitura:** páginas + matriz 3×3×3 → **palavras/minuto** por complexidade (300/130/70).
2. **Escrita:** páginas + matriz 2×3×3 → **palavras/hora** por complexidade (250/125/60).
3. **Vídeo/Áudio:** horas diretas (1×) → **múltiplo da duração** (2×/3×).
4. **Fóruns → Discussão:** fórmula por palavras/minutos → **tempo fixo** (30 min / 1,5 h).
5. **Outras atividades → Artefatos:** genérico → recategorizado em "Produção", tempo do professor.
6. **Encontros ao vivo → Síncrona/Presencial:** sempre disponível → **condicional**, com presencial incluído.
7. **Organização geral:** por mídia → por **tipo de aprendizagem (Laurillard)**.
8. **Saídas:** Autônomo × **Contato/tutoria** → Contato tende a desaparecer (assíncrono).
9. **Créditos/base teórica:** Barre/Brown/Esarey (CC BY-NC-SA) → Laurillard 2012 + McInnes 2026 / Liu & Evans 2020 / Beer 2019 (autoria IFES: Amorim, Battestin, Passos).

### [–] RETIRADAS (existem hoje, não existem na proposta)
1. **Módulo "Avaliações/Provas"** com horas de estudo por prova.
2. **Prova cronometrada / take-home** (tempo limite em minutos).
3. **Eixo "Densidade da página"** (450/600/750 palavras) — leitura.
4. **Eixos duplos da leitura** ("nível conceitual" + "objetivo") como campos separados.
5. **Eixos "Densidade" + "Nível de elaboração (drafting)"** — escrita.
6. **Eixo "Gênero do texto"** como campo separado (vira complexidade).
7. **Fórmula de fórum em áudio/vídeo** (`0,18X + X/6` vs `X/3`) e o *quirk* associado.
8. **Conceito de "atividade mediada / contato / tutoria"** no caso padrão de MOOC.

---

## 5. Implicações de implementação

| Tema | O que muda | Atenção |
|---|---|---|
| **Unidade de entrada** | Página → **palavra** em leitura e escrita | Exige que o professor saiba/contabilize a contagem de palavras do material (na reunião, levantado como ponto a automatizar — 15:37) |
| **Multiplicador de vídeo** | 1× → 2×/3× | Pode elevar bastante a carga estimada de cursos com muito vídeo |
| **Provas** | Remover o módulo §06 | Migrar quem usa "prova" para "Questionário" |
| **Complexidade** | Um seletor único Baixa/Média/Alta por atividade | Vídeo, quiz, interativa e discussão só têm **Baixa/Alta** (sem "Média"); leitura e escrita têm os três níveis |
| **Condicionais (*)** | Colaboração e Síncrono/Presencial só aparecem em modo "híbrido" | Prever um *toggle* de contexto (MOOC padrão × híbrido/pesquisa) |
| **Contato/Autônomo** | Saída "Contato" ~ irrelevante no padrão | Reavaliar se mantém as 3 saídas ou simplifica para carga total |
| **Calibração declarada × estimada** | **Não está na proposta**, mas é diferencial da ferramenta atual | Recomendado **manter** — é exatamente a dor central da reunião (validar a CH declarada) |

---

## 6. Pontos que a proposta NÃO especifica (a resolver na implementação)

1. **Agregação semanal × total:** o Quadro 2 define só o *tempo por atividade*; não diz se o resultado é "h/semana" (modelo atual) ou **carga total do curso**. Para MOOC autoinstrucional/assíncrono, o total tende a fazer mais sentido que o "por semana". **Decisão pendente.**
2. **Nível "Média" ausente** em vídeo, questionário, atividade interativa e discussão (só Baixa/Alta). Confirmar se é intencional.
3. **Conversão palavra↔página** para quem ainda pensa em páginas (material legado).
4. **Como obter a contagem de palavras/duração de mídia** (manual agora; candidato a automação futura via mapa de atividades / sala do MOOC — reunião 14:45–16:29).
5. **Calibração "reversa"** (entrar com a CH desejada e a ferramenta sugerir atividades) — ideia levantada na reunião como evolução futura, fora do escopo desta versão.

---

## 7. Próximos passos sugeridos

1. **[Recomendado]** Implementar uma **v2 do `index.html`** reorganizada por tipo de aprendizagem (Laurillard), com os novos rates do Quadro 2, mantendo a **calibração declarada × estimada** e um *toggle* MOOC padrão × híbrido.
2. Antes de codar, **fechar as 5 decisões pendentes** da seção 6 com a Aline/Vanessa (sobretudo agregação semanal × total e o nível "Média").
3. Manter a **calculadora atual intacta** como referência e criar a nova lado a lado (`index-cefor.html`), para comparação numérica auditável (linha pedida na reunião — 20:00–21:05).
4. Outra abordagem — diga qual.

---

### Arquivos consultados
- `index.html` (calculadora atual) · `docs/source/server.R` + `ui.R` (base original)
- `docs/COMO ESTIMAR A CARGA HORÁRIA…PROPOSTA…IFES.md` (Quadro 2 + Laurillard)
- `docs/transcrição da Reuniao MOOC 29-06-2026….txt` (racional das decisões)
