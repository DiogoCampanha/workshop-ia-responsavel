# Workshop — Introdução à IA Responsável na Prática

Material completo de um workshop prático de **IA Responsável (viés & fairness)** para estudantes de graduação em Ciência da Computação. Três encontros de 1h40, seis estudos de caso com dados reais, aprendizagem por descoberta: os participantes treinam um modelo, encontram a injustiça dentro dele, tentam corrigi-la — e descobrem que corrigir é escolher.

## Conteúdo do repositório

| Arquivo/pasta | Descrição |
|---|---|
| `workshop_ia_responsavel.ipynb` | Notebook único dos 3 dias do workshop (em português) |
| `dados/` | Os 6 datasets usados nos estudos de caso (baixados automaticamente das fontes originais) |
| `material_instrutor.csv` | Contextos e dilemas éticos de cada caso — carregado pelo notebook no momento pedagógico certo. **Participantes: não leiam! (spoilers)** |
| `GUIA_DO_INSTRUTOR.md` | Guia de condução do workshop. **Contém spoilers** |
| `.github/workflows/baixar_dados.yml` | Workflow que baixa/atualiza os datasets em `dados/` |

## Para participantes

```bash
pip install pandas scikit-learn matplotlib
```

Baixe o `workshop_ia_responsavel.ipynb`, abra no Jupyter/VS Code/Colab e siga as instruções do notebook. Todo o resto é baixado automaticamente.

## Estudos de caso e fontes dos dados

Este workshop só é possível graças a dados e trabalhos disponibilizados publicamente. Todos os créditos aos autores originais:

| Caso | Dataset | Fonte e créditos |
|---|---|---|
| 💰 Renda | **Adult (Census Income)** | Becker, B. & Kohavi, R. (1996). UCI Machine Learning Repository. [doi:10.24432/C5XW20](https://doi.org/10.24432/C5XW20) · Licença CC BY 4.0 |
| ⚖️ Justiça criminal | **COMPAS Recidivism** | Angwin, J., Larson, J., Mattu, S. & Kirchner, L. (2016), *Machine Bias*, ProPublica. Dados: [propublica/compas-analysis](https://github.com/propublica/compas-analysis) |
| 🏦 Crédito | **Statlog German Credit** | Hofmann, H. (1994). UCI Machine Learning Repository. [doi:10.24432/C5NC77](https://doi.org/10.24432/C5NC77) · Licença CC BY 4.0 |
| 🏥 Saúde | **Diabetes 130-US Hospitals** | Strack, B. et al. (2014), *BioMed Research International*. UCI ML Repository ([doi:10.24432/C5230J](https://doi.org/10.24432/C5230J)); versão pré-processada pela equipe **Fairlearn** para o tutorial SciPy 2021 ([fairlearn/talks](https://github.com/fairlearn/talks)) |
| 🎓 Exame da ordem | **Law School (LSAC)** | Wightman, L. F. (1998), *LSAC National Longitudinal Bar Passage Study*. Versão limpa de Le Quy, T. et al. (2022), *A survey on datasets for fairness-aware machine learning* ([tailequy/fairness_dataset](https://github.com/tailequy/fairness_dataset)) |
| 🏫 Educação | **Student Performance** | Cortez, P. & Silva, A. (2008), *Using Data Mining to Predict Secondary School Student Performance*. UCI ML Repository ([doi:10.24432/C5TG7T](https://doi.org/10.24432/C5TG7T)) · Licença CC BY 4.0 |

## Agradecimentos e referências

- **ProPublica** — pela investigação *Machine Bias* (2016) e por abrir os dados que fundaram o debate moderno de fairness algorítmico.
- **Equipe Fairlearn** (fairlearn.org) — pelo pré-processamento do dataset de diabetes e pelo material educacional que inspirou parte desta abordagem.
- **UCI Machine Learning Repository** — pela curadoria e hospedagem de datasets há décadas.
- **Le Quy et al.** — pelo survey e repositório de datasets para fairness-aware ML.
- Fundamentos teóricos: Barocas, Hardt & Narayanan, *Fairness and Machine Learning* ([fairmlbook.org](https://fairmlbook.org)) · Hardt, Price & Srebro (2016), *Equality of Opportunity in Supervised Learning* · Kleinberg, Mullainathan & Raghavan (2016) e Chouldechova (2016) — teorema da impossibilidade · Obermeyer et al. (2019), *Science* · Mitchell et al. (2019), *Model Cards* · Gebru et al. (2018), *Datasheets for Datasets*.
- Ferramentas: [scikit-learn](https://scikit-learn.org), [pandas](https://pandas.pydata.org), [Fairlearn](https://fairlearn.org).

## Licença e uso

Material didático de uso livre para fins educacionais, com atribuição. Os datasets pertencem aos seus autores originais e mantêm as licenças indicadas acima. Os dados retratam pessoas reais — use-os com o respeito que o tema do workshop exige.
