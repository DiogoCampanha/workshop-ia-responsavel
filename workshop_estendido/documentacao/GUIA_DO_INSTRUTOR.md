# Guia do Instrutor — versão estendida (3 encontros de 1h40)

> ⚠️ **Este documento contém spoilers do workshop** (atributos sensíveis, tipos de viés e dilemas). Não distribuir aos participantes.

## Formato

- 3 encontros de 1h40 · até **6 grupos** · 1 estudo de caso por grupo
- Os alunos usam **só o notebook** `workshop_estendido/workshop_ia_responsavel_estendido.ipynb`, que cobre os 3 dias
- Slides do instrutor, um deck por dia (com notas do apresentador e minutagem): `documentacao/slides/`
  - `dia1_treinando_um_modelo.pptx` · `dia2_fairness_e_tradeoffs.pptx` · `dia3_apresentacoes_e_discussao.pptx`

**Links para enviar aos alunos:**
- Colab: `https://colab.research.google.com/github/DiogoCampanha/workshop-ia-responsavel/blob/main/workshop_estendido/workshop_ia_responsavel_estendido.ipynb`
- Download: `https://raw.githubusercontent.com/DiogoCampanha/workshop-ia-responsavel/main/workshop_estendido/workshop_ia_responsavel_estendido.ipynb`

## Desenho pedagógico do Dia 1 (aprendizagem por descoberta)

Os alunos **não recebem** o atributo sensível nem pistas de viés no início:

1. **1.1–1.5** — escolhem o caso, exploram, tratam os faltantes (Decisão 2), treinam (Decisão 3) e avaliam. A ficha do caso mostra só o contexto neutro.
2. **1.6 — hipótese** — o grupo registra em `HIPOTESES_DO_GRUPO` quem pode ser prejudicado e quais colunas são suspeitas. *A célula bloqueia (`assert`) se não preencherem.*
3. **1.7 — revelação** — **o instrutor informa a cada grupo, individualmente** (papel ou de viva voz — nunca projetar), o atributo sensível do caso. O grupo preenche `SENSIVEL = "..."` à mão e confronta com a hipótese.
4. **1.8 — Decisão 4** — o grupo retreina SEM a coluna sensível e compara as acurácias (spoiler: quase não muda — gancho para os proxies no Dia 2).

### 🤫 Atributos sensíveis para entregar aos grupos (Dia 1, seção 1.7)

| Caso | Valor exato a preencher em `SENSIVEL` |
|---|---|
| adult | `"sexo"` |
| compas | `"raca"` |
| german | `"faixa_etaria"` |
| diabetes | `"raca"` |
| law | `"raca"` |
| student | `"zona"` |

## Os 6 casos (viés e dilema DIFERENTES em cada um)

| Código | Tema | Tipo de viés | Dilema ético (revelado no notebook 2.6) |
|---|---|---|---|
| `adult` | Renda (censo EUA) | histórico nos rótulos | descrever o mundo × corrigi-lo (paridade × oportunidade) |
| `compas` | Reincidência criminal | de medição (prisão ≠ crime) | calibração × FPR igual — teorema da impossibilidade |
| `german` | Crédito bancário | representação + custos 5:1 | quem paga o custo da equidade; métricas instáveis em grupo pequeno |
| `diabetes` | Readmissão hospitalar | de acesso nos rótulos (positivo = benefício) | eficiência utilitarista × acesso igual a vagas limitadas |
| `law` | Exame da ordem | por proxy (LSAT/GPA) | "cegar" o modelo × usar a raça para corrigir |
| `student` | Risco de reprovação | de intervenção (ajuda que rotula) | estigma do FP × abandono do FN; limiares por grupo? |

## ⚠️ Avisos por caso (observados nos testes com os dados reais)

- **german:** com a árvore de decisão (padrão), o modelo **não supera o chute da maioria** (68,7% × 70,0%). Recomende `"logistica"` (73,0%) ou `"floresta"` (74,3%), ou use o fato como discussão sobre "acurácia engana". A coluna `idade` permanece no modelo e a faixa etária deriva dela: remover só `faixa_etaria` não "cega" nada (o proxy perfeito).
- **diabetes:** só ~11% dos pacientes são readmitidos, então com o limiar 0,5 o modelo quase nunca prevê "sim" (taxa de seleção < 1%). Oriente o grupo a explorar **limiares entre 0,10 e 0,20** na seção 2.5. As curvas mostram onde. No dataset, `"None"` em `max_glu_serum` e `A1Cresult` significa "exame não realizado", e o notebook trata isso como informação, não como dado faltante.
- **law:** 89% dos estudantes passam, então a acurácia mal supera o chute da maioria, mas as diferenças de FPR entre grupos são grandes. É um ótimo exemplo de "acurácia engana".
- **student:** o modelo usa a nota do 1º período (G1), como fazem os sistemas reais de alerta precoce. Sem ela, os modelos testados (regressão logística e árvore) não superavam o chute da maioria.

## Estrutura do notebook

- **Dia 1 (1.1–1.8):** 4 decisões (dataset, faltantes, modelo, atributo sensível) + hipótese e revelação + 2 tarefas.
- **Dia 2 (2.1–2.6):** 4 lentes de auditoria (representação, métricas por grupo, regra dos 80%, importâncias/proxies) → limiares por grupo (Decisão 5) → dilema do caso e posição do grupo (Decisão 6).
- **Dia 3 (3.1–3.3):** gera o relatório de impacto (`relatorio_impacto_<caso>.txt` + figura antes×depois) e traz o roteiro dos 8 minutos de apresentação.

## Dados e infraestrutura

- O notebook baixa os dados de `workshop_estendido/recursos/dados/` neste repositório e, em reserva, das fontes originais (UCI, ProPublica, Fairlearn, mirrors).
- O `recursos/material_instrutor.csv` (contextos, dilemas, significado de FP/FN) fica **fora do notebook** e só é exibido no momento pedagógico certo.
- A pasta `recursos/dados/` é preenchida pelo workflow do GitHub Actions (`.github/workflows/baixar_dados.yml`). Para atualizar, execute-o na aba **Actions**.
- **Sem internet na sala:** distribua a pasta `recursos/` junto com o notebook (mesma pasta). O notebook usa as cópias locais automaticamente.

## Setup dos alunos (enviar antes do Dia 1)

```
pip install pandas scikit-learn matplotlib
```
Python ≥ 3.9 com Jupyter (Anaconda, VS Code) ou o link do Google Colab acima.

## Cronograma sugerido

**Dia 1:** por que IA Responsável (10') → caso + exploração + preparação (20') → treino e avaliação (25') → discussão "onde pode ser injusto?" + revelação (20') → retreino sem o atributo + mini-projeto (25').

**Dia 2:** representação (15') → métricas por grupo (20') → regra dos 80% (15') → importâncias/proxies (15') → conflito de limiares + impossibilidade (30') → dilema e decisão do grupo (5').

**Dia 3:** abertura (5') → 6 apresentações de 8' (55') → discussão coletiva (25') → síntese e boas práticas (15').
