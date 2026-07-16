# Guia do Instrutor — Workshop IA Responsável na Prática

> ⚠️ **Este documento contém spoilers do workshop** (atributos sensíveis, tipos de viés e dilemas). Não distribuir aos participantes.

## Formato

3 encontros de 1h40 · até 6 grupos · 1 estudo de caso por grupo · notebook único (`workshop_ia_responsavel.ipynb`) que cobre os 3 dias.

## Desenho pedagógico do Dia 1 (aprendizagem por descoberta)

Os alunos **não recebem** o atributo sensível nem qualquer pista de viés no início:

1. **1.1–1.5** — escolhem o caso, exploram, tratam faltantes (Decisão 2), treinam (Decisão 3) e avaliam. A ficha do caso mostra apenas contexto neutro.
2. **1.6 — hipótese** — sem ferramentas novas, o grupo registra em `HIPOTESES_DO_GRUPO` quem pode ser prejudicado e quais colunas são suspeitas. *A célula bloqueia (assert) se não preencherem.*
3. **1.7 — revelação** — **o instrutor informa a cada grupo, individualmente** (papel ou verbal — não projetar!), o atributo sensível do caso; o grupo preenche `SENSIVEL = "..."` à mão e confronta com a hipótese.
4. **1.8 — Decisão 4** — retreinam SEM a coluna sensível e comparam acurácias (spoiler: quase não muda — gancho para proxies no Dia 2).

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

## Estrutura do notebook

- **Dia 1 (1.1–1.8):** 4 decisões (dataset, faltantes, modelo, atributo sensível) + hipótese e revelação + 2 tarefas.
- **Dia 2 (2.1–2.6):** 4 lentes de auditoria (representação, métricas por grupo, regra dos 80%, importâncias/proxies) → limiares por grupo (Decisão 5) → dilema do caso e posição do grupo (Decisão 6).
- **Dia 3 (3.1–3.3):** gera o relatório de impacto (`relatorio_impacto_<caso>.txt` + figura antes×depois) e traz o roteiro dos 8 minutos de apresentação.

## Dados e infraestrutura

- O notebook baixa os dados primeiro deste repositório (`dados/`) e, em fallback, das fontes originais (UCI, ProPublica, Fairlearn, mirrors).
- O `material_instrutor.csv` (contextos, dilemas, significado de FP/FN) fica **fora do notebook** e é baixado deste repositório — o notebook só o exibe no momento pedagógico certo. Alunos curiosos podem abrir o CSV no repositório; se isso preocupar, mova-o para um repo privado espelho e ajuste `URL_MATERIAL` na célula de infraestrutura.
- Os datasets em `dados/` são baixados/atualizados pelo workflow do GitHub Actions (`.github/workflows/baixar_dados.yml`) — execute-o manualmente na aba Actions se necessário.
- Sem internet na sala: distribua a pasta `dados/` e o `material_instrutor.csv` junto com o notebook (o fallback local é automático).

## Setup dos alunos (enviar antes do Dia 1)

```
pip install pandas scikit-learn matplotlib
```
Python ≥ 3.9 com Jupyter (Anaconda, VS Code ou Google Colab — no Colab basta fazer upload do .ipynb).

## Cronograma sugerido

**Dia 1:** por que RAI (10') → caso + exploração + preparação (20') → treino e avaliação (25') → discussão "onde pode ser injusto?" + revelação (20') → retreino sem atributo + mini-projeto (25').

**Dia 2:** representação (15') → métricas por grupo (20') → regra dos 80% (15') → importâncias/proxies (15') → conflito de limiares + impossibilidade (30') → dilema e decisão do grupo (5').

**Dia 3:** abertura (5') → 6 apresentações de 8' (55') → discussão coletiva (25') → síntese e boas práticas (15').
