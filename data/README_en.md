# Project Data

The repository **does not include** the full datasets (tens of megabytes of raw news and stock quotes). They can be restored locally following the steps below.

## Issuers

| Company | Sector |
|---------|--------|
| Sberbank | Finance |
| Lukoil | Oil and gas |
| Magnit | Consumer sector |
| NLMK | Mining and processing |
| Positive Group | IT |

## How to Obtain the Data

### 1. Corporate News

```bash
python src/web_parser.py
```

The parser collects disclosures from [e-disclosure.ru](https://www.e-disclosure.ru) and saves Excel files named `{company}_news_last.xlsx`.

### 2. Stock Quotes

Historical prices — from Yahoo Finance, Investing.com, or MOEX. Notebook `01_data_merge.ipynb` expects CSVs with columns for date and closing price.

### 3. Labeled Dataset for Classification

Training the sentiment models requires a file with manual labeling (~1000 news items):

| Field | Values |
|-------|--------|
| `1. Существенное` | 0 — insignificant, 1 — significant |
| `1. Направление` | -1 — negative, 0 — neutral, 1 — positive |
| `filtered_text` | preprocessed news text |

Example structure — in `data/sample/labeled_news_sample.csv`.

Place the full file at `data/labeled_news.csv` (in `.gitignore`).

### 4. Intermediate Datasets

The notebooks sequentially create:

- `all_news.csv` — merged news from all issuers
- `merged_news.csv` — news + return lags
- `final_df.csv` — final dataset for regression

## Old Experiments

The `archive/rest/` folder (not in git) — drafts, duplicates, and discarded attempts, including CAR calculation.