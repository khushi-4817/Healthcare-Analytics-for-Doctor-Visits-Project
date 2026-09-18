# 🏥 Healthcare Analytics for Doctor Visits

> **A comprehensive data analytics project** exploring the factors that drive doctor visit frequency among 5,190 Australian patients. Built as part of a healthcare analytics study using survey microdata.

---

## 📌 Project Overview

This project analyses a patient-level health survey dataset to understand **who visits the doctor, how often, and why**. The dataset exhibits a classic zero-inflated count distribution — 79.8% of patients recorded zero visits — making it an excellent case study for statistical modelling, exploratory analysis, and data visualisation.

---

## 📁 Repository Structure

```
Healthcare Analytics for Doctor Visits/
│
├── 📊 1776250375-P2-Healthcare Analytics for Doctor Visits.csv   # Raw dataset
├── 📓 Healthcare_Analytics_for_Doctor_Visits.ipynb               # Jupyter analysis notebook
├── 🖥️  dashboard.html                                             # Interactive dark-theme dashboard (19 charts)
├── 📄  report.html                                                # Narrative storytelling report
├── 📑  Khushi Wanjari_TIRTC_Heathcare Analytics for Doctor Visits.pptx  # Presentation slides
├── 📖  README.md                                                  # This file
└── 🔒  .gitignore                                                 # Git ignore rules
```

---

## 📂 Dataset Description

**File:** `1776250375-P2-Healthcare Analytics for Doctor Visits.csv`  
**Source:** Australian health survey (GSOEP-style microdata)  
**Rows:** 5,190 patient records  
**Columns:** 13 variables

### Variable Dictionary

| Variable | Type | Description |
|---|---|---|
| `visits` | Integer (0–9) | Number of doctor visits in the reference period |
| `gender` | Categorical | Patient gender: `male` / `female` |
| `age` | Float (0.19–0.72) | Age (scaled/normalised; higher = older) |
| `income` | Float (0.0–1.5) | Household income (scaled; higher = wealthier) |
| `illness` | Integer (0–5) | Number/severity of illnesses in past 2 weeks |
| `reduced` | Integer (0–14) | Days of reduced activity due to illness |
| `health` | Integer (0–12) | Self-assessed health score (0 = best health) |
| `private` | Binary | Private health insurance: `yes` / `no` |
| `freepoor` | Binary | Free government health card (low income): `yes` / `no` |
| `freerepat` | Binary | Free repatriation health card: `yes` / `no` |
| `nchronic` | Binary | Non-limiting chronic condition: `yes` / `no` |
| `lchronic` | Binary | Limiting chronic condition: `yes` / `no` |

---

## 📊 Key Statistics

| Metric | Value |
|---|---|
| Total patients | 5,190 |
| Average visits per patient | 0.302 |
| Maximum visits recorded | 9 |
| Zero-visit patients | **4,141 (79.8%)** |
| Female patients | 2,702 (52.1%) |
| Private insurance holders | 2,298 (44.3%) |
| Limiting chronic condition | 605 (11.7%) |
| Non-limiting chronic condition | 2,092 (40.3%) |
| Free poor cardholders | 222 (4.3%) |
| Free repatriation cardholders | 1,091 (21.0%) |

---

## 🔍 Key Findings

### 1. Zero-Inflated Visit Pattern
Nearly **80% of patients visited zero times**, creating a heavily right-skewed distribution. This invalidates standard linear regression — zero-inflated Poisson or negative-binomial models are required.

### 2. Illness Severity is the Strongest Driver
| Severity | Avg Visits | % Who Visited |
|---|---|---|
| 0 – None | 0.079 | 6.8% |
| 1 – Mild | 0.295 | 19.6% |
| 2 | 0.404 | 27.3% |
| 3 | 0.421 | 30.6% |
| 4 | 0.577 | 36.5% |
| 5 – Severe | 0.814 | **41.9%** |

### 3. Chronic Conditions Double Visits
- **Limiting chronic condition** (lchronic): +130% increase over baseline
- **Non-limiting chronic condition** (nchronic): +27% increase

### 4. Gender Disparity
Female patients average **0.362 visits** vs **0.236** for males — a **53% higher rate**, consistent across all subgroups.

### 5. Socioeconomic Gradient
| Income Bracket | Avg Visits | % Visited |
|---|---|---|
| Low (< 0.3) | 0.398 | 25.6% |
| Mid (0.3–0.7) | 0.290 | 19.7% |
| High (≥ 0.7) | 0.224 | 15.7% |

Low-income patients visit **78% more often** than high-income patients.

### 6. Age Effect
The oldest cohort (scaled 0.72, approx. 65+) averages **0.483 visits** — 2.4× more than the youngest cohort (0.201).

### 7. Insurance Paradox
- **Freerepat** cardholders: highest visit rate (31.6%, avg 0.467) — driven by age/chronic condition profile
- **Freepoor** cardholders: **lowest** visit rate (9.0%, avg 0.158) — access barriers beyond cost
- **Private insurance**: no significant effect vs uninsured (0.295 vs 0.307)

---

## 🖥️ Dashboard

Open [`dashboard.html`](dashboard.html) in any modern browser.

**Contains 19 interactive charts across 5 themed sections:**

| Section | Charts |
|---|---|
| 01 · Overview | Visits distribution, CDF, Gender split |
| 02 · Health Burden | Illness severity line, % visited bar, Chronic grouped bar, Health score distribution, Health×Illness heatmap |
| 03 · Demographics | Gender visits bar, Radar chart, Gender×Chronic bar, Age dual-axis, Income dual-axis |
| 04 · Insurance | Coverage stacked bar, % visiting by insurance, Avg visits by insurance, Gender×insurance grouped bar |
| 05 · Wellbeing | Activity-reduced days line, Illness severity donut |

Each chart includes an inline **story caption** explaining the key takeaway.

---

## 📄 Report

Open [`report.html`](report.html) in any modern browser for the full **narrative storytelling report** — a long-form prose document covering all 7 analytical themes with stat callouts, data tables, modelling recommendations, and a policy conclusion.

---

## 🔬 Modelling Recommendations

Because the outcome variable (`visits`) is a non-negative integer with excess zeros, the following models are appropriate:

| Model | When to Use |
|---|---|
| **Zero-Inflated Poisson (ZIP)** | When zeros arise from two distinct processes (structural non-visitors + occasional visitors) |
| **Zero-Inflated Negative Binomial (ZINB)** | When there is also overdispersion (variance > mean) |
| **Hurdle Model** | When the zero/non-zero decision and the count process are modelled separately |
| **Negative Binomial Regression** | Simpler baseline if zero inflation is mild |

**Recommended feature set:** `illness`, `lchronic`, `nchronic`, `age`, `gender`, `reduced`, `health`, `income`, `freerepat`

---

## 🛠️ Setup & Usage

### Prerequisites
- Python 3.8+
- Jupyter Notebook or JupyterLab

### Install dependencies
```bash
pip install pandas numpy matplotlib seaborn scipy statsmodels jupyter
```

### Run the notebook
```bash
jupyter notebook Healthcare_Analytics_for_Doctor_Visits.ipynb
```

### View the dashboard
[📊 View Dashboard](dashboard.html)
Open `dashboard.html` directly in any browser — no server required.

---

## 📚 Technologies Used

| Tool | Purpose |
|---|---|
| Python / Pandas | Data loading, cleaning, aggregation |
| NumPy / SciPy | Statistical calculations |
| Matplotlib / Seaborn | Notebook visualisations |
| ECharts 5 | Interactive dashboard charts |
| HTML / CSS | Dashboard & report styling |
| Jupyter Notebook | Exploratory analysis |

---

## 👤 Author

**Khushi Wanjari**  
Healthcare Analytics Project  

---

## 📜 License

This project is for educational and research purposes. Dataset sourced from Australian health survey microdata.

---

*Made with ❤️ and IBM Bob*
