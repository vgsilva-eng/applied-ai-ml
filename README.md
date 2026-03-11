#        Statistics & Probability - Final Team Project 


# Project Overview


ADDING HERE





## Table of Contents

1. [Dataset](#dataset)
2. [Project Structure](#project-structure)
3. [Technical Report Sections](#technical-report-sections)
4. [Results](#results)
5. [Technologies Used](#technologies-used)
6. [Collaborators](#collaborators)
7. [License](#license)
   


## Dataset

**Source:** [UCI Machine Learning Repository - Adult Census Income Dataset](https://archive.ics.uci.edu/dataset/193/cardiotocography)

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
