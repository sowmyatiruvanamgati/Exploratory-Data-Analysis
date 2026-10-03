# 🚢 Exploratory Data Analysis — Titanic Dataset

A complete, reproducible EDA project using **Python, pandas, numpy and fg-data-profiling**
(the maintained successor of `ydata-profiling`).

| | |
|---|---|
| **Dataset** | Titanic passengers (891 rows × 12 columns) — [source](https://github.com/datasciencedojo/datasets) |
| **Question** | Which factors were associated with survival? |
| **Skills shown** | Data cleaning, feature engineering, summary statistics, visualisation, outlier detection, hypothesis testing, automated profiling |

## 📦 Deliverables

| File | Description |
|---|---|
| `Titanic_EDA.ipynb` | **Notebook** with all EDA steps (already executed, with outputs) |
| `Titanic_EDA.html` | Same notebook as a web page (no Jupyter needed to read it) |
| `report.html` | **Automated HTML profiling report** of the raw data |
| `report_cleaned.html` | Profiling report of the cleaned data |
| `INSIGHTS.md` | **Insights summary** (8 bullets) |
| `data/titanic.csv` | Original dataset |
| `data/titanic_cleaned.csv` | Cleaned dataset with engineered features |
| `figures/` | All charts as PNG files |
| `requirements.txt` | Libraries needed |

## 🛠️ Setup (step by step)

1. Install **Python 3.10 – 3.14** (check with `python --version`).
2. Open a terminal in this folder.
3. Create and activate a virtual environment (keeps libraries separate from other projects):
   ```bash
   python -m venv venv
   venv\Scripts\activate          # Windows
   source venv/bin/activate       # macOS / Linux
   ```
4. Install the libraries:
   ```bash
   pip install -r requirements.txt
   ```
   (Equivalent to `pip install pandas numpy ydata-profiling` from the task — see the note on naming below.)

## ▶️ How to run

```bash
jupyter notebook Titanic_EDA.ipynb
```
Then choose **Kernel → Restart & Run All**. It takes about 1 minute and creates `report.html`, `report_cleaned.html`, `figures/` and `data/titanic_cleaned.csv`.
If `data/titanic.csv` is missing, the notebook downloads it automatically.

**The profiling one-liner** (what the task asks for):
```python
from data_profiling import ProfileReport          # (old name: from ydata_profiling import ProfileReport)
ProfileReport(df, explorative=True).to_file("report.html")
```

> **Note on naming:** `ydata-profiling` was renamed to **`fg-data-profiling`** (import name `data_profiling`).
> The notebook tries the new name first and falls back to the old one, so it works with either package.

## 🔬 What the notebook covers

1. **Setup & load** – imports, versions, data dictionary
2. **Data quality** – missing values (Cabin 77%, Age 20%, Embarked 0.2%), duplicates (none), zero fares (15)
3. **Summary statistics** – describe, skewness
4. **Cleaning & feature engineering** – Title-based age imputation, `HasCabin`, `Deck`, `FamilySize`, `AgeGroup`, `FareLog` …
5. **Univariate analysis** – distributions of every key variable
6. **Outliers** – IQR rule, decision to keep and log-transform
7. **Bivariate analysis** – survival vs sex, class, port, title, age, fare, family, cabin
8. **Correlation matrix**
9. **Hypothesis tests** – chi-square and Mann-Whitney U with effect sizes
10. **Automated profiling** – `ProfileReport` → `report.html`
11. **Insights summary**

## 📌 Key findings

- Overall survival: **38.4%**
- **Women 74% vs men 19%**; **1st class 63% vs 3rd class 24%**
- 97% of first-class women survived, only 14% of third-class men
- Children survived more (58%), but overall age difference is not significant (p ≈ 0.16)
- Families of 2–4 did best (58%); alone 30%; large families 16%

See [`INSIGHTS.md`](INSIGHTS.md) for the full list.

## ⚠️ Troubleshooting

| Problem | Fix |
|---|---|
| `pip install` fails on a very new Python | Use Python 3.12 or 3.13, or run the notebook in Google Colab |
| `ModuleNotFoundError: data_profiling` | Run `pip install fg-data-profiling` in the same environment as the notebook kernel |
| Notebook can't find the kernel | Run `python -m ipykernel install --user --name python3` |
| Profiling is slow | Normal for the first run; use `ProfileReport(df, minimal=True)` for a faster, smaller report |
| Errors with pandas 3.x | The profiling library needs `pandas<3`; `requirements.txt` already enforces this |

**Tested with:** Python 3.12, pandas 2.3.3, numpy 2.5.3, scipy 1.18, matplotlib 3.11, seaborn 0.13.2, fg-data-profiling 4.20.0.

## 📚 Credits

Titanic dataset from [datasciencedojo/datasets](https://github.com/datasciencedojo/datasets). Profiling by [fg-data-profiling](https://github.com/Data-Centric-AI-Community/fg-data-profiling) (formerly ydata-profiling).
