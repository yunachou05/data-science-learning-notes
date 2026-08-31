# PCE Growth Regime Classification and Economic Feature Discovery (economic machine-learning experiment)

### An Experimental Supervised Machine Learning Framework for Classifying U.S. Personal Consumption Expenditure Growth

**Author:** Yuna Chou  
**Project:** IBM Machine Learning Professional Certificate – Course 3 Final Project

---

## Project Overview

This project explores whether historical economic indicators contain useful
predictive information for distinguishing between **Weak** and **Strong**
quarterly U.S. Personal Consumption Expenditure (PCE) growth regimes.

The project is designed as an experimental supervised machine learning study
rather than a production forecasting system.

The main objectives are to:

1. Construct a binary PCE growth classification target.
2. Preserve chronological ordering to avoid future-data leakage.
3. Establish naïve baseline performance.
4. Train and compare multiple supervised classification algorithms.
5. Evaluate models using multiple classification metrics.
6. Explore which economic indicators contain useful predictive information.
7. Examine model stability across different economic periods.

---

## Research Question

> Can historical economic indicators help distinguish between Weak and Strong
> quarterly Real PCE growth regimes?

A secondary question is:

> Which machine learning models and economic features provide the most useful
> predictive information under chronological out-of-sample testing?

---

## Data

The analysis covers approximately:

**2007 Q1 – 2026 Q2**

The target variable is quarterly growth in **Real Personal Consumption
Expenditures (Real PCE)**.

Economic predictors represent several dimensions of the U.S. economy,
including:

- Income and wages
- Labor-market conditions
- Household credit
- Household wealth
- Housing
- Consumer sentiment
- Monetary policy
- Financial conditions
- Exchange rates
- Market volatility
- Demographics

Primary economic data were obtained from the Federal Reserve Bank of St. Louis
FRED database and U.S. Bureau of Economic Analysis sources.

---

## Target Definition

An initial classification based on positive versus negative PCE growth produced
a highly imbalanced target.

Therefore, alternative thresholds were investigated.

To prevent information leakage, the final classification threshold was
calculated using **training data only**.

The training-period median was:

**0.5576% quarterly Real PCE growth**

The classification target was defined as:

- **Class 0 – Weak Growth:** PCE growth ≤ 0.5576
- **Class 1 – Strong Growth:** PCE growth > 0.5576

The resulting training distribution was:

| Regime | Observations |
|---|---:|
| Weak Growth | 30 |
| Strong Growth | 29 |

This produced a nearly balanced training target.

---

## Chronological Train/Test Design

Because the dataset represents economic time series, observations were not
randomly shuffled.

Instead, a chronological split was used:

**Training:** 2007 Q1 – 2021 Q4  
**Testing:** 2022 Q1 – 2026 Q2

This design helps prevent future economic information from leaking into model
training.

---

## Baseline Difficulty

Before training machine learning models, naïve classifiers were evaluated to
establish minimum performance benchmarks.

The training majority-class baseline was approximately:

**50.8%**

Therefore, a useful machine learning model should meaningfully outperform
naïve classification while maintaining reasonable performance across both
growth regimes.

---

## Machine Learning Models

The following supervised classification algorithms were evaluated:

- Dummy Classifier
- Logistic Regression
- K-Nearest Neighbors (KNN)
- Linear Support Vector Machine (SVM)
- Decision Tree
- Random Forest
- XGBoost

These models represent different learning assumptions, ranging from linear
decision boundaries to nonlinear tree-based ensemble methods.

---

## Model Evaluation

Models were evaluated using multiple metrics:

- Accuracy
- Balanced Accuracy
- Precision
- Recall
- F1 Score
- ROC-AUC
- Confusion Matrix

Using multiple metrics was particularly important because some models produced
apparently strong Recall or F1 scores while collapsing toward prediction of a
single class.

---

## Model Comparison

| Model | Accuracy | Balanced Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---:|---:|---:|---:|---:|---:|
| Most-Frequent Dummy | 0.389 | 0.500 | 0.000 | 0.000 | 0.000 | — |
| Stratified Dummy | 0.444 | 0.442 | — | — | 0.500 | — |
| Logistic Regression | **0.556** | **0.575** | **0.667** | 0.400 | 0.500 | 0.550 |
| KNN | 0.556 | 0.500 | 0.556 | **1.000** | **0.714** | 0.500 |
| Linear SVM | 0.444 | 0.425 | 0.500 | 0.600 | 0.546 | 0.575 |
| Decision Tree V1 | 0.556 | 0.500 | 0.556 | **1.000** | **0.714** | 0.488 |
| Decision Tree V2 | 0.444 | 0.488 | 0.500 | 0.100 | 0.167 | 0.488 |
| Random Forest | 0.500 | 0.475 | 0.539 | 0.700 | 0.609 | 0.400 |
| XGBoost | **0.556** | **0.575** | **0.667** | 0.400 | 0.500 | **0.600** |

---

## Key Findings

No tested model demonstrated strong out-of-sample classification performance.

**Logistic Regression and XGBoost achieved the highest Balanced Accuracy
(0.575), while XGBoost achieved the highest ROC-AUC (0.600).**

KNN and Decision Tree V1 achieved high Strong-Growth Recall and F1 scores,
but both models largely collapsed toward predicting the Strong-Growth class.

This demonstrates an important machine learning lesson:

> A model should not be selected using Accuracy, Recall, or F1 alone.
> Confusion matrices, balanced accuracy, probability discrimination, and
> prediction behavior should be evaluated together.

---

## Walk-Forward Stability Analysis

Instead of relying only on extensive hyperparameter tuning, Decision Tree V2
was also examined using **walk-forward stability analysis**.

The purpose was to evaluate whether the model remained stable as the economic
environment changed through time.

The first four folds achieved approximately **0.50 balanced accuracy** and
frequently predicted only one class.

However, the fifth fold achieved approximately **0.929 balanced accuracy**
during the COVID shock and recovery period.

This suggests that Decision Tree V2 may be **regime-dependent**.

The model struggled to distinguish relatively subtle differences in PCE growth
during normal economic environments but became substantially more effective
when economic conditions changed sharply.

This illustrates how walk-forward validation can reveal temporal instability
that would be hidden by a single train/test performance metric.

---

## Economic Interpretation

The project does not establish causal relationships between economic indicators
and PCE growth.

Instead, feature importance and model behavior should be interpreted as
evidence of **predictive relationships within this dataset**.

One of the broader lessons from the experiment is that economic relationships
may change across macroeconomic regimes.

This is particularly visible when comparing normal expansion periods with the
COVID shock and subsequent recovery.

---

## Project Workflow

Problem Definition  
↓  
Data Preparation  
↓  
PCE Growth Target Construction  
↓  
Chronological Train/Test Split  
↓  
Class Balance Analysis  
↓  
Baseline Difficulty Analysis  
↓  
Supervised Model Training  
↓  
Model Evaluation  
↓  
Model Comparison  
↓  
Feature Discovery  
↓  
Walk-Forward Stability Analysis  
↓  
Economic Interpretation

---

## Repository Structure

```text
pce-growth-regime-classification/
│
├── README.md
├── requirements.txt
├── LICENSE
│
├── notebooks/
│   └── PCE_Growth_Regime_Classification.ipynb
│
├── data/
│   └── project datasets
│
├── figures/
│   └── project visualizations
│
├── results/
│   └── model and feature results
│
└── reports/
    └── PCE_Growth_Regime_Classification_Report.pdf


```python

```
