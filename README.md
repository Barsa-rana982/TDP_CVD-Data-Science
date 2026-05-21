# Cardiovascular Disease (CVD) Data Science Project

Analysis of cardiovascular disease outcomes across Australian Primary Health Networks (PHNs) using 2017–18 health data. The project explores the relationship between socioeconomic factors, lifestyle risk factors, and CVD mortality/hospitalisation rates.

---

## Project Structure

```
CVD/
├── CVD.ipynb                          # Main analysis notebook
├── cvd_RiskFactor.ipynb               # Risk factor preprocessing notebook
├── CVD-death.xlsx                     # Raw CVD mortality data (AIHW)
├── CVD-hospitalisation.xlsx           # Raw CVD hospitalisation data (AIHW)
├── risk-factors-prevalence.xlsx       # Risk factors: HBP, obesity, inactivity, smoking
├── socioeconomic&population.xlsx      # Socioeconomic & population characteristics
├── phn-2017-concordance-files-...xlsx # PHN–SA2 concordance mapping
└── Socioeconomic_vs_CVD.twbx          # Tableau dashboard
```

---

## Notebooks

### `cvd_RiskFactor.ipynb`
Preprocesses the raw risk factor Excel file and exports cleaned CSVs:
- High blood pressure (HBP) by PHN, age group, sex
- Insufficient physical activity (IPA) by PHN, age group, sex
- Obesity (OB) by PHN, age group, sex
- Current smoking (CS) by PHN, age group, sex
- Merges all risk factors into `Risk_Factors.csv` and joins with CVD data into `Risk_Factors_CVD.csv`

### `CVD.ipynb`
End-to-end analysis pipeline with the following stages:

| Stage | Description |
|-------|-------------|
| **Data Preprocessing** | Loads CVD death, hospitalisation, socioeconomic, and risk factor sheets; flattens multi-level headers; exports cleaned CSVs |
| **Data Merging** | Joins CVD outcomes with risk factors and socioeconomic indicators into `Final_CVD_Merged.xlsx` |
| **Long Format Export** | Melts SES variables into `SES_vs_CVD_LongFormat.xlsx` with PHN→State mapping for Tableau |
| **EDA** | Visualises SES vs CVD outcomes by gender, age group, and state |
| **Linear Regression** | OLS regression of SES predictors against CVD death rate per 100k |
| **Logistic Regression** | Classifies CVD risk (Yes/No) using SES and demographic features |

---

## Key Findings

- **Socioeconomic factors alone do not predict CVD death rates** — the linear regression model achieved R² = 0.002 with no significant predictors (all p-values > 0.05)
- **SES features are effective for classification** — logistic regression successfully classifies PHNs by CVD risk level
- Incorporating health-related risk factors (smoking, obesity, physical inactivity, hospitalisation rate) is recommended to improve regression model performance

---

## Data Sources

All data is sourced from the [Australian Institute of Health and Welfare (AIHW)](https://www.aihw.gov.au), 2017–18:
- CVD deaths and hospitalisations at PHN level (by age group and sex)
- Risk factor prevalence at PHN level
- Socioeconomic and population characteristics at PHA level
- PHN to SA2 concordance file (ASGS 2021)

---

## Requirements

```
pandas
openpyxl
matplotlib
seaborn
statsmodels
scikit-learn
```

Install with:
```bash
pip install pandas openpyxl matplotlib seaborn statsmodels scikit-learn
```

---

## How to Run

1. Clone the repository and open in Jupyter or VS Code
2. Run `cvd_RiskFactor.ipynb` first — this generates the risk factor CSVs
3. Run `CVD.ipynb` — this processes all data, merges, analyses, and produces outputs
