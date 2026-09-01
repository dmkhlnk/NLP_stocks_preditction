# Assessing the Impact of Issuer News on Security Prices

Educational project (HSE University, 2025): NLP + machine learning for analyzing corporate news of five Russian issuers and forecasting market reaction.

**[Full report (PDF)](docs/project_report.pdf)**

## Objective

Build a pipeline that:

1. Collects corporate news and stock quotes
2. Preprocesses texts (tokenization, lemmatization, TF-IDF)
3. Classifies news by significance and direction of impact on price
4. Attempts to predict log returns based on news text (regression)

## Issuers

Sberbank · Lukoil · Magnit · NLMK · Positive Group — five largest sectors of the Russian market (>85% of market capitalization).

## Repository Structure

```
├── docs/project_report.pdf      # project internship report
├── src/web_parser.py            # news parser from e-disclosure.ru
├── notebooks/                   # main pipeline (run in order)
│   ├── 01_data_merge.ipynb
│   ├── 02_text_preprocessing.ipynb
│   ├── 03_text_analysis_tfidf.ipynb
│   ├── 04_multiclass_classification.ipynb
│   ├── 05_double_binary_classification.ipynb
│   ├── 06_naive_bayes_baseline.ipynb
│   ├── 07_regression_random_forest.ipynb
│   └── 08_regression_catboost.ipynb
└── data/
    ├── README_en.md             # how to obtain the full dataset
    └── sample/                  # sample of the labeled dataset
```

## Results

### Classification (double binary model, Random Forest)

| Stage | F1-score |
|-------|----------|
| Significant / insignificant news | 96% |
| Positive reaction (among significant) | 88% |
| Negative reaction (among significant) | 67% |

The double binary scheme (first filtering out noise, then determining the sign) handled class imbalance better than direct multiclass classification.

### Regression (log returns ~ TF-IDF of news)

Random Forest and CatBoost showed strong overfitting: high R² on train, negative on test. This is documented in the report as a limitation of the "text → returns" approach without event-study labeling.

## Quick Start

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter lab notebooks/
```

Before running the notebooks, prepare the data — see [data/README.md](data/README.md).

## Stack

Python · pandas · scikit-learn · CatBoost · NLTK · pymorphy3 · Selenium · Jupyter

## Authors

**Gorbachev D.** · Nikoshin D. · **Mikhaylenko D.** · Sigaeva M. · Sidorov P.

HSE University, "International Bachelor's in Business and Economics" program, specialization "Data Analysis in Economics and Management".