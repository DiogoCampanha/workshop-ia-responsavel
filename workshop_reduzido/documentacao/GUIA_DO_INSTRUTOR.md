# Guia do Instrutor — versão reduzida (encontro único de 2h)

> ⚠️ **Este documento contém spoilers do workshop** (atributos sensíveis, tipos de viés e dilemas). Não distribuir aos participantes.

## Formato

- 1 encontro de **2h** · **5 grupos** · 1 estudo de caso por grupo, sem repetição
- Os alunos usam **só o notebook** `workshop_reduzido/workshop_ia_responsavel_reduzido.ipynb` (download ou Colab)
- Slides do instrutor: `documentacao/slides/workshop_ia_responsavel_2h.pptx` (23 slides, com notas do apresentador e minutagem)

**Links para enviar aos alunos:**
- Colab: `https://colab.research.google.com/github/DiogoCampanha/workshop-ia-responsavel/blob/main/workshop_reduzido/workshop_ia_responsavel_reduzido.ipynb`
- Download: `https://raw.githubusercontent.com/DiogoCampanha/workshop-ia-responsavel/main/workshop_reduzido/workshop_ia_responsavel_reduzido.ipynb`

## Cronograma (120 min)

| Tempo | Bloco | Notebook | Slides |
|---|---|---|---|
| 0–10' | Abertura: por que importa + mapa da IA Responsável | setup (2 primeiras células) | 1–4 |
| 10–25' | **Parte 1** · Treinar, direto ao ponto | 1.1–1.2 + Tarefa 1 | 5–8 |
| 25–40' | **Parte 2** · Hipótese → revelação → com/sem atributo | 2.1–2.3 | 9–10 |
| 40–90' | **Parte 3** · Auditoria de fairness (o coração do encontro) | 3.1–3.5 + Tarefas 2–4 | 11–19 |
| 90–100' | **Parte 4** · O dilema do caso | Decisão 4 | 20 |
| 100–120' | **Parte 5** · Painel final + apresentações relâmpago (2,5' por grupo) + síntese | painel final | 21–23 |

**Se o tempo apertar,** corte da Parte 1, nunca da Parte 3. Nesta ordem:
1. Pule a Tarefa 1 e leia o resultado do treino em voz alta.
2. Faça as lentes 1 e 3 (3.1 e 3.3) só como leitura: executar e comentar em 1 min cada.
3. No exercício de limiares (3.5), peça só a 1ª tentativa (igualar a taxa de seleção).

## As 4 decisões dos grupos

| Decisão | Onde | O que o grupo escolhe |
|---|---|---|
| 1 | 1.1 | Caso (`DATASET`) e modelo (`MODELO`). O padrão é `"logistica"`: rápido e melhor que o "chute da maioria" em todos os casos |
| 2 | 2.3 | Usar ou não o atributo sensível. As duas versões são treinadas e comparadas automaticamente na lente 4 |
| 3 | 3.5 | Limiares de decisão por grupo |
| 4 | Parte 4 | Posição no dilema ético do caso |

A remoção de linhas com dados faltantes é automática nesta versão (só afeta o caso `adult`, ~7% das linhas).

## Desenho pedagógico: aprendizagem por descoberta

Os alunos **não recebem** o atributo sensível nem pistas de viés no início:

1. **Parte 1** — treinam e avaliam. A ficha do caso mostra só o contexto neutro.
2. **2.1 — hipótese** — o grupo registra em `HIPOTESES_DO_GRUPO` quem pode ser prejudicado e quais colunas são suspeitas. *A célula bloqueia (`assert`) se não preencherem.*
3. **2.2 — revelação** — quando **todos** os grupos tiverem registrado a hipótese, o instrutor projeta o **slide 10** ("A revelação"), com o atributo sensível de cada caso. Cada grupo preenche `SENSIVEL = "..."` à mão e compara com a sua hipótese.
4. **2.3 — Decisão 2** — o notebook treina o modelo COM e SEM o atributo e o grupo escolhe o oficial.
5. **3.4 — "cegar" resolve?** — comparação automática COM × SEM, lado a lado, mais um **detector de proxies** (um modelo simples tenta adivinhar o grupo usando só as outras colunas).

### 🤫 Atributos sensíveis (mostrados no slide 10, seção 2.2 do notebook)

| Caso | Valor exato a preencher em `SENSIVEL` |
|---|---|
| adult | `"sexo"` |
| compas | `"raca"` |
| german | `"faixa_etaria"` |
| law | `"raca"` |
| student | `"zona"` |

## Os 5 casos (viés e dilema DIFERENTES em cada um)

| Caso | Tema | Tipo de viés | Dilema (revelado na Parte 4) |
|---|---|---|---|
| `adult` | Renda (censo EUA) | histórico nos rótulos | descrever o mundo × corrigi-lo (paridade × oportunidade) |
| `compas` | Reincidência criminal | de medição (prisão ≠ crime); aqui o "sim" **prejudica** | calibração × FPR igual — teorema da impossibilidade |
| `german` | Crédito bancário | representação (jovens = 15% da base) + custos 5:1 | quem paga o custo da equidade |
| `law` | Exame da ordem | por proxy (LSAT/GPA) | "cegar" o modelo × usar a raça para corrigir |
| `student` | Risco de reprovação | de intervenção (ajuda que rotula) | estigma do FP × abandono do FN |

## O que esperar com os dados reais (modelo padrão: regressão logística)

Valores obtidos nos testes com os dados reais. Os grupos verão números próximos a estes.

| Caso | Acurácia × chute da maioria | Disparate impact (limiar 0,5) | Destaques para a discussão |
|---|---|---|---|
| adult | 84,6% × 75,1% | 0,33 ❌ | Igualar a seleção (M=0,66, F=0,18) leva o DI a 0,95, mas a precisão do grupo F cai de 0,70 para 0,54 |
| compas | 66,9% × 53,0% | 0,46 ❌ | O "sim" prejudica: o grupo com maior taxa de seleção é o mais penalizado |
| german | 73,0% × 70,0% | 0,88 ✅ | Passa na regra dos 80%, mas com só ~57 jovens no teste. **O detector de proxies acerta 100%:** a coluna `idade` continua no modelo e a faixa etária deriva dela (o proxy perfeito) |
| law | 90,1% × 89,0% | 0,82 ✅ (por pouco) | **"Acurácia engana" ao vivo:** 89% passam no exame, então o modelo mal supera o chute. Mesmo assim, o FPR é 0,54 (Non-White) × 0,92 (White). Sem a raça, a disparidade quase não muda (DI 0,82 → 0,84): LSAT, GPA e decis são proxies |
| student | 87,2% × 84,6% | 0,85 ✅ | Os dois erros pesam mais no grupo rural: TPR 0,46 (rural) × 0,77 (urbana), ou seja, mais alunos em risco que ninguém ajuda; e FPR 0,11 × 0,075, mais rótulos indevidos. Base pequena: 195 alunos no teste. Proxies da zona: escola, tempo de deslocamento |

> Com outros modelos os números mudam. A árvore de decisão, por exemplo, **não supera o chute da maioria** no caso `german`, o que pode virar uma boa discussão se algum grupo a escolher.

## Dados e infraestrutura

- O notebook baixa os dados de `workshop_reduzido/recursos/dados/` neste repositório e, em reserva, das fontes originais (UCI, ProPublica, mirrors).
- O `recursos/material_instrutor.csv` (contextos, dilemas, significado de FP/FN) fica **fora do notebook** e só é exibido no momento pedagógico certo.
- A pasta `recursos/dados/` é preenchida pelo workflow do GitHub Actions (`.github/workflows/baixar_dados.yml`). Para atualizar, execute-o na aba **Actions**.
- **Sem internet na sala:** distribua a pasta `recursos/` junto com o notebook (mesma pasta). O notebook usa as cópias locais automaticamente.

## Setup dos alunos (enviar antes)

```
pip install pandas scikit-learn matplotlib
```
Python ≥ 3.9 com Jupyter, ou simplesmente o link do Google Colab acima (nada a instalar). Peça que executem as 2 primeiras células **ao chegar**.
