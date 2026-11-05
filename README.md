# Audible Audiobooks Data Cleaning

A Python / pandas data cleaning project that turns a messy raw dataset of **87,489 audiobooks** from audible.in into a clean, analysis-ready CSV.

## Overview

Raw scraped data is rarely ready for analysis. This project walks through a complete cleaning workflow: fixing text, extracting numbers from combined strings, correcting data types, converting currency, removing duplicates and handling missing values.

## What the notebook does

| Step | Task | Approach |
|------|------|----------|
| 1 | Load and inspect | `read_csv`, `.info()` |
| 2 | Clean text fields | Remove the `Writtenby:` and `Narratedby:` prefixes from `author` and `narrator` |
| 3 | Parse ratings | Split the combined `stars` text (e.g. "4.5 out of 5 stars41 ratings") into `rating_stars` and `n_ratings` using regex |
| 4 | Fix data types | `price` to float, `rating_stars` to category, `releasedate` to datetime |
| 5 | Convert durations | Turn text like "2 hrs and 20 mins" into a numeric `time_mins` column |
| 6 | Check ranges | Histograms and `.describe()` to spot out-of-range values |
| 7 | Convert currency | Prices from INR to USD (1 INR = 0.012 USD) |
| 8 | Standardise categories | Consistent capitalisation in `language` |
| 9 | Remove duplicates | Detect duplicates on `name`, `author`, `narrator`, `time_mins` and `price`, keeping the latest release date (70 removed) |
| 10 | Handle missing data | Keep unrated audiobooks to avoid biasing price analysis |
| 11 | Export | Save the cleaned data to `data/audible_clean.csv` |

## Results

- **Rows:** 87,489 → 87,419 after duplicate removal
- **Columns:** 8 → 9 (`stars` split into two columns, `time` replaced by `time_mins`)
- **Languages:** 36, now consistently capitalised
- **Unrated audiobooks:** 72,387 kept (missing rating values left as NaN)

### Cleaned dataset columns

| Column | Type | Description |
|--------|------|-------------|
| `name` | object | Audiobook title |
| `author` | object | Author name |
| `narrator` | object | Narrator name |
| `releasedate` | datetime | Release date |
| `language` | object | Audiobook language |
| `price` | float | Price in USD |
| `rating_stars` | category | Average star rating (1 to 5) |
| `n_ratings` | float | Number of ratings |
| `time_mins` | int | Duration in minutes |

## Tech stack

Python, pandas, NumPy, Matplotlib, Jupyter

## Getting started

```bash
git clone https://github.com/SaChuma/audible-data-cleaning.git
cd audible-data-cleaning
pip install -r requirements.txt
jupyter notebook notebook.ipynb
```

## Project structure

```
├── notebook.ipynb          # Full cleaning workflow
├── data/
│   ├── audible_raw.csv     # Original raw dataset
│   └── audible_clean.csv   # Cleaned output
├── requirements.txt
└── README.md
```

## Data source

[Audible dataset on Kaggle](https://www.kaggle.com/datasets/snehangsude/audible-dataset) (audiobooks from audible.in, 1998 to 2025 pre-planned releases).

## Author

**Sandiso Maqhajana** · [GitHub](https://github.com/SaChuma) · [LinkedIn](https://linkedin.com/in/sandiso-qhajie)
