# Fetal Health Classification using Cardiotocography (CTG) Signals
**AAI501 - Applied Artificial Intelligence & Machine Learning**
**Final Team Project**

---

## Project Overview

Hospitals and clinicians monitor millions of births each year, and **cardiotocography (CTG)** is the dominant fetal monitoring technology. These signals help determine whether the fetus is healthy or experiencing distress (lack of oxygen, abnormal physiology, etc.).

**The Problem:** While CTG devices collect signals continuously, the interpretation is still largely human-dependent and varies significantly between clinicians. This variability can lead to inconsistent diagnoses and delayed interventions.

**Our Solution:** Develop an AI-powered classification system that automatically analyzes fetal health signals and classifies the fetus as:
- **Normal** — healthy, no intervention needed
- **Suspect** — requires monitoring and observation
- **Pathologic** — requires immediate clinical intervention

This project aims to assist clinicians by providing objective, data-driven assessments of fetal health in real-time. 



## Table of Contents

1. [Dataset](#dataset)
2. [Project Structure](#project-structure)
3. [Technical Report Sections](#technical-report-sections)
4. [Results](#results)
5. [Technologies Used](#technologies-used)
6. [Collaborators](#collaborators)
7. [License](#license)
   


## Dataset

**Source:** [UCI Machine Learning Repository - Cardiotocography](https://archive.ics.uci.edu/dataset/193/cardiotocography)

**Description:** 

Cardiotocography is a medical monitoring technique used during pregnancy and labor to assess fetal well-being. It simultaneously records two signals:

1. Fetal Heart Rate (FHR) — how fast the baby's heart is beating
2. Uterine Contractions (UC) — frequency and intensity of contractions

A CTG machine prints a trace that a obstetrician or midwife reads to decide if the baby is healthy, at risk, or in danger.

The Dataset
Source: UCI ML Repository, id=193
Samples: 2,126 fetal CTG exams
Features: 21 signal measurements extracted automatically from CTG traces
Targets: Two labels assigned by expert obstetricians

## Dataset Reference Guide

### The Two Target Labels

| Column | Meaning | Values |
|--------|---------|--------|
| `NSP` | Fetal State **(main target)** | `1` = Normal, `2` = Suspect, `3` = Pathologic |
| `CLASS` | FHR Pattern morphology | `1–10` (10 morphological pattern classes) |

---

### Key Features (21 CTG Signals)

#### Fetal Heart Rate & Event Signals

| Feature | What it Measures |
|---------|-----------------|
| `LB` | Baseline fetal heart rate (bpm) |
| `AC` | Number of accelerations per second |
| `FM` | Fetal movements per second |
| `UC` | Uterine contractions per second |
| `DL` | Light decelerations per second |
| `DS` | Severe decelerations per second |
| `DP` | Prolonged decelerations per second |

#### Variability Signals

| Feature | What it Measures |
|---------|-----------------|
| `ASTV` | % time with abnormal short-term variability |
| `MSTV` | Mean short-term variability |
| `ALTV` | % time with abnormal long-term variability |
| `MLTV` | Mean long-term variability |

#### FHR Histogram Features

| Feature | What it Measures |
|---------|-----------------|
| `Width` | Width of FHR histogram |
| `Min` | Minimum of FHR histogram |
| `Max` | Maximum of FHR histogram |
| `Nmax` | Number of histogram peaks |
| `Nzeros` | Number of histogram zeros |
| `Mode` | Mode of FHR histogram |
| `Mean` | Mean of FHR histogram |
| `Median` | Median of FHR histogram |
| `Variance` | Variance of FHR histogram |
| `Tendency` | Tendency of FHR histogram (`-1` = left, `0` = symmetric, `1` = right) |

---

> **Note:** All features are numeric.
> Zeros in event signals (`AC`, `FM`, `DL`, `DS`, `DP`) represent **absence of events**, not missing data.

---

## Project Structure

```
applied-ai-ml/
│
├── notebooks/
│   └── dataset_cleaning.ipynb      # Exploratory Data Analysis (EDA)
│   └── Model Analysis.ipynb        # Model Selection/Analysis
├── requirements.txt                # Python dependencies
├── README.md                       # Project documentation
├── LICENSE                         # MIT License
├── Projectinstructions.md          # Assignment instructions
└── venv/                           # Virtual environment (not tracked)
```

---

## Technical Report Sections

Our analysis follows a structured approach:

### 1. **Data Exploration & Cleaning**
   - Load CTG dataset from UCI repository
   - Analyze class distribution (Normal vs. Suspect vs. Pathologic)
   - Check for missing values and data quality issues
   - Understand feature distributions and outliers

### 2. **Exploratory Data Analysis (EDA)**
   - Visualize target class distribution
   - Analyze feature distributions (histograms, box plots)
   - Examine feature separability across classes
   - Correlation analysis and multicollinearity detection

### 3. **Data Preprocessing**
   - Handle class imbalance using stratified sampling
   - Feature scaling (StandardScaler for linear models)
   - Feature transformation (log/sqrt for skewed features)
   - Train/test split with stratification

### 4. **Feature Engineering**
   - Create interaction features (e.g., `ASTV × AC`)
   - Generate ratio features (e.g., `AC/UC`)
   - Feature selection based on correlation and importance

### 5. **Model Development**
   - Baseline models: Random Forest, XGBoost
   - Alternative models: Logistic Regression, SVM
   - Class weight balancing for imbalanced data
   - Hyperparameter tuning via GridSearch/RandomSearch

### 6. **Model Evaluation**
   - Primary metric: **Macro F1-Score** (treats all classes equally)
   - Per-class precision, recall, and F1-score
   - Confusion matrix analysis
   - Feature importance analysis

### 7. **Results & Interpretation**
   - Model comparison and selection
   - Clinical interpretation of predictions
   - Error analysis (where does the model fail?)
   - Recommendations for deployment

---

## Results

> **Status:** In Progress

### Key Findings from EDA
- **Class Imbalance:** Normal (78%), Suspect (14%), Pathologic (8%)
- **Top Predictive Features:** `ASTV`, `ALTV`, `AC`, `LB`, `DL`, `DP`
- **No missing values** detected
- **Outliers are clinically significant**, not errors
- **Recommended models:** Tree-based (Random Forest, XGBoost) for robustness

### Expected Results
Final models will be evaluated on:
- 
- 
- @lashana adding here
---

## Technologies Used

### Programming Language
- **Python 3.13**

### Core Libraries
| Library | Purpose |
|---------|---------|
| `pandas` | Data manipulation and analysis |
| `numpy` | Numerical computing |
| `scikit-learn` | Machine learning algorithms and evaluation |
| `ucimlrepo` | Dataset loading from UCI repository |

### Visualization
| Library | Purpose |
|---------|---------|
| `matplotlib` | Static plotting and visualizations |
| `seaborn` | Statistical data visualization |
| `plotly` | Interactive visualizations |

### Statistical Analysis
| Library | Purpose |
|---------|---------|
| `scipy` | Statistical tests and transformations |
| `statsmodels` | Advanced statistical modeling |

### Development Environment
- **Jupyter Notebook** — Interactive analysis and experimentation
- **Virtual Environment (venv)** — Dependency isolation

---

## Collaborators

**Team Members:**
- Viviana Garzon Silva
- Jasmine Duong
- Lashana Narayan

**Institution:** University of San Diego (USD)
**Course:** AAI501 - Applied Artificial Intelligence & Machine Learning
**Semester:** Spring 2026

---

## License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

## References

- **Dataset:** Ayres de Campos et al. (2000). *SisPorto 2.0: A Program for Automated Analysis of Cardiotocograms.* Journal of Maternal-Fetal Medicine, 9:311-318.
- **UCI Repository:** [Cardiotocography Dataset](https://archive.ics.uci.edu/dataset/193/cardiotocography)
- **Clinical Context:** Cardiotocography is used to monitor fetal heart rate and uterine contractions during pregnancy and labor to assess fetal well-being.

---

**Last Updated:** March 30, 2026
