# Workshop — IA Responsável na Prática (viés & fairness)

Material de um workshop prático de **IA Responsável**, com foco em **viés e fairness**, para estudantes de graduação em Ciência da Computação. Os participantes treinam um modelo com dados reais, encontram a injustiça dentro dele, tentam corrigi-la e descobrem que corrigir é escolher.

O workshop existe em duas versões **independentes**:

| Versão | Formato | Casos | Notebook dos alunos |
|---|---|---|---|
| [**Reduzida**](workshop_reduzido/) | 1 encontro de 2h | 5 | [`workshop_ia_responsavel_reduzido.ipynb`](workshop_reduzido/workshop_ia_responsavel_reduzido.ipynb) |
| [**Estendida**](workshop_estendido/) | 3 encontros de 1h40, com mini-projeto | 6 | [`workshop_ia_responsavel_estendido.ipynb`](workshop_estendido/workshop_ia_responsavel_estendido.ipynb) |

## 👩‍🎓 Para participantes

Vocês só precisam do **notebook** da versão indicada pelo instrutor. Todo o resto é baixado automaticamente.

**Versão de 2h:**
- [Abrir no Google Colab](https://colab.research.google.com/github/DiogoCampanha/workshop-ia-responsavel/blob/main/workshop_reduzido/workshop_ia_responsavel_reduzido.ipynb) (nada a instalar), ou
- baixar o [notebook](https://raw.githubusercontent.com/DiogoCampanha/workshop-ia-responsavel/main/workshop_reduzido/workshop_ia_responsavel_reduzido.ipynb) e rodar localmente com `pip install pandas scikit-learn matplotlib`.

> ⚠️ Não abram as pastas `documentacao/` e `recursos/`: elas contêm spoilers das atividades.

## 🧑‍🏫 Para instrutores

Cada versão segue a mesma estrutura:

```
workshop_<versão>/
├── workshop_ia_responsavel_<versão>.ipynb   ← único arquivo dos alunos
├── documentacao/                            ← só para o instrutor
│   ├── GUIA_DO_INSTRUTOR.md                 (cronograma, atributos sensíveis, avisos por caso)
│   └── slides/                              (apresentações com notas do apresentador)
└── recursos/                                ← carregado automaticamente pelo notebook
    ├── material_instrutor.csv               (contextos e dilemas de cada caso)
    └── dados/                               (datasets, baixados pelo GitHub Actions)
```

Os datasets em `recursos/dados/` são baixados das fontes originais pelo workflow [`.github/workflows/baixar_dados.yml`](.github/workflows/baixar_dados.yml). Para atualizá-los, execute-o na aba **Actions**.

## Estudos de caso e fontes dos dados

Este workshop só é possível graças a dados e trabalhos disponibilizados publicamente. Todos os créditos aos autores originais:

| Caso | Dataset | Versões | Fonte e créditos |
|---|---|---|---|
| Renda | **Adult (Census Income)** | ambas | Becker, B. & Kohavi, R. (1996). UCI Machine Learning Repository. [doi:10.24432/C5XW20](https://doi.org/10.24432/C5XW20) · CC BY 4.0 |
| Justiça criminal | **COMPAS Recidivism** | ambas | Angwin, J., Larson, J., Mattu, S. & Kirchner, L. (2016), *Machine Bias*, ProPublica. Dados: [propublica/compas-analysis](https://github.com/propublica/compas-analysis) |
| Crédito | **Statlog German Credit** | ambas | Hofmann, H. (1994). UCI Machine Learning Repository. [doi:10.24432/C5NC77](https://doi.org/10.24432/C5NC77) · CC BY 4.0 |
| Exame da ordem | **Law School (LSAC)** | ambas | Wightman, L. F. (1998), *LSAC National Longitudinal Bar Passage Study*. Versão limpa de Le Quy, T. et al. (2022), *A survey on datasets for fairness-aware machine learning* ([tailequy/fairness_dataset](https://github.com/tailequy/fairness_dataset)) |
| Educação | **Student Performance** | ambas | Cortez, P. & Silva, A. (2008), *Using Data Mining to Predict Secondary School Student Performance*. UCI ML Repository ([doi:10.24432/C5TG7T](https://doi.org/10.24432/C5TG7T)) · CC BY 4.0 |
| Saúde | **Diabetes 130-US Hospitals** | estendida | Strack, B. et al. (2014), *BioMed Research International*. UCI ML Repository ([doi:10.24432/C5230J](https://doi.org/10.24432/C5230J)); versão pré-processada pela equipe **Fairlearn** para o tutorial SciPy 2021 ([fairlearn/talks](https://github.com/fairlearn/talks)) |

## Agradecimentos e referências

- **ProPublica**, pela investigação *Machine Bias* (2016) e por abrir os dados que fundaram o debate moderno sobre fairness algorítmico.
- **Equipe Fairlearn** (fairlearn.org), pelo pré-processamento do dataset de diabetes e pelo material educacional que inspirou parte desta abordagem.
- **UCI Machine Learning Repository**, pela curadoria e hospedagem de datasets há décadas.
- **Le Quy et al.**, pelo survey e pelo repositório de datasets para fairness-aware ML.
- Fundamentos teóricos: Barocas, Hardt & Narayanan, *Fairness and Machine Learning* ([fairmlbook.org](https://fairmlbook.org)) · Hardt, Price & Srebro (2016), *Equality of Opportunity in Supervised Learning* · Kleinberg, Mullainathan & Raghavan (2016) e Chouldechova (2016), sobre o teorema da impossibilidade · Obermeyer et al. (2019), *Science* · Buolamwini & Gebru (2018), *Gender Shades* · Mitchell et al. (2019), *Model Cards* · Gebru et al. (2018), *Datasheets for Datasets*.
- Ferramentas: [scikit-learn](https://scikit-learn.org), [pandas](https://pandas.pydata.org), [Fairlearn](https://fairlearn.org).

## Licença e uso

Material didático de uso livre para fins educacionais, com atribuição. Os datasets pertencem aos seus autores originais e mantêm as licenças indicadas acima. Os dados retratam pessoas reais: use-os com o respeito que o tema do workshop exige.
