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
│   ├── AAI-501_Final_Project.ipynb   # Main project notebook (full pipeline)
│   ├── dataset_cleaning.ipynb        # Initial EDA and data exploration
│   └── Model_Analysis.ipynb          # Supplementary model analysis
│
├── requirements.txt                # Python dependencies
├── README.md                       # Project documentation
└── LICENSE                         # MIT License
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
   - Stratified 70/30 train/test split to preserve class proportions
   - SMOTE applied to training set only to address class imbalance
   - Feature scaling via `StandardScaler` inside pipeline (leak-free)

### 4. **Feature Selection**
   - `SelectKBest(f_classif, k=10)` for Linear SVM
   - `SelectFromModel(RandomForestClassifier)` for Random Forest
   - `SelectFromModel(XGBClassifier)` for XGBoost (selected 6 features: AC, ASTV, ALTV, MSTV, DP, Mean)

### 5. **Model Development**
   - Three models trained inside scikit-learn `Pipeline` (preprocessing + feature selection + model)
   - **Linear SVM** — `class_weight='balanced'`, SelectKBest, GridSearchCV for feature selection tuning
   - **Random Forest** — `class_weight='balanced'`, SelectFromModel
   - **XGBoost** — GridSearchCV for hyperparameter tuning (`k`,`n_estimators`, `max_depth`, `learning_rate`), SelectKBest

### 6. **Model Evaluation**
   - Primary metric: **Macro F1-Score** (treats all classes equally)
   - Per-class precision, recall, and F1-score
   - Confusion matrix analysis
   - Cross-validation (5-fold StratifiedKFold) on training data
   - SHAP values for model interpretability
   - Overfitting check (train vs. test performance gap)

### 7. **Results & Interpretation**
   - Model comparison and selection (XGBoost best overall)
   - SHAP analysis confirming clinically meaningful feature signals
   - Overfitting assessment with recommendations

---

## Results

> **Status:** Completed

### Key Findings from EDA
- **Class Imbalance:** Normal (78%), Suspect (14%), Pathologic (8%)
- **Top Predictive Features:** `ASTV`, `ALTV`, `AC`, `LB`, `DL`, `DP`
- **No missing values** detected
- **Outliers are clinically significant**, not errors
- **Tree-based models** (Random Forest, XGBoost) outperformed linear models as expected

### Final Model Results

| Model | Macro F1 | Pathologic Recall | Suspect Recall |
|-------|----------|------------------|----------------|
| Linear SVM | Lowest | ~75.5% | ~84.1% |
| Random Forest | Strong | ~92.5% | ~64.8% |
| **XGBoost** | **Best** | **~92.5%** | **~72.7%** |

**XGBoost** selected as final model — Accuracy **92.9%**, strongest macro F1, highest recall for the clinically critical Pathologic class.

### SHAP Key Findings
- `ASTV` and `ALTV` are the most influential features — higher abnormal variability strongly increases predicted risk
- Loss of accelerations (`AC`) is a key indicator of Pathologic classification
- Baseline heart rate (`LB`) depression signals fetal distress
- All top features align with established clinical CTG interpretation guidelines

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
| `xgboost` | XGBoost gradient boosting classifier |
| `imbalanced-learn` | SMOTE for class imbalance handling |
| `shap` | Model interpretability via SHAP values |
| `ucimlrepo` | Dataset loading from UCI repository |
| `graphviz` | XGBoost decision tree visualization |

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

**Last Updated:** April 4, 2026
