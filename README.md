# DSI-Cohort8-ML-1
### Optimizing Bank Marketing Campaigns: Data-Driven Targeting for Term Deposits
**Data Sciences Institute — Cohort 8 | Machine Learning Stream**

---

## Table of Contents
1. [Project Overview](#1-project-overview)
2. [Dataset & Variables](#2-dataset--variables)
3. [Repository Structure](#3-repository-structure)
4. [Methodology](#4-methodology)
5. [Risks & Unknowns](#5-risks--unknowns)
6. [Team & Roles](#6-team--roles)

---

## 1. Project Overview

**Business Problem**
Marketing campaigns conducted through phone calls require significant time, effort, and financial resources. However, only a small percentage of clients actually subscribe to the term deposit product. As a result, the bank spends resources contacting many customers who are unlikely to be interested.
The goal of this project is to build a machine learning model that predicts whether a bank client will subscribe to a term deposit based on demographic information, financial characteristics, and previous campaign interaction history. By identifying clients who are more likely to subscribe before contacting them, the bank can increase campaign efficiency, reduce unnecessary calls, improve conversion rates, and optimize the allocation of marketing resources. In addition, we want to understand which factors most influence whether a client says yes. By identifying these key drivers, the bank can improve its marketing strategy and make more informed decisions about future campaigns.


## 2. Dataset & Variables

**Source:** UCI Machine Learning Repository — [Bank Marketing Dataset (ID 222)](https://archive.ics.uci.edu/dataset/222/bank+marketing)
**Records:** 45,211 | **Variables:** 16 predictors + 1 target

The dataset mixes demographic, financial, and campaign-related attributes. Many entries contain the placeholder `"unknown"`, especially in fields like `education`, `contact`, and `poutcome`.

See [`data/README.md`](data/README.md) for the full variable dictionary and folder contents.

---

## 3. Repository Structure

```
DSI-Cohort8-ML-1/
│
├── data/                 # Raw, processed datasets and SQL scripts
├── notebooks/            # EDA and modelling notebooks
├── models/               # Saved model artefacts (.pkl, .joblib, etc.)
├── reports/              # Final reports, visualisations, presentation decks
├── src/                  # Reusable source code (pipelines, utilities, etc.)
│
├── README.md
└── .gitignore
```

See [`notebooks/README.md`](notebooks/README.md) for local setup instructions and git workflow.

---

## 4. Methodology

**Primary Objective:** Develop and evaluate a predictive ML model that determines the likelihood of a client subscribing to a term deposit using demographic, financial, and historical campaign data.

**Secondary Objectives:**
- Identify and rank the most influential customer attributes driving subscription decisions
- Isolate high-probability customer segments with conversion rates substantially above the historical campaign baseline
- Analyse the precision-recall trade-off and establish an optimal classification threshold aligned with the bank's marketing budget and revenue goals

### 4.1 Problem Framing

This is a binary classification problem: the output is either `yes` (subscribed) or `no` (did not subscribe). We may also explore framing this as a regression problem (predicting subscription probability) to enable threshold tuning based on business cost-benefit analysis.

### 4.2 Data Preparation

The preprocessing pipeline covers data cleaning, feature engineering, encoding, and scaling. A 70/15/15 train/validation/test split is applied. See [`notebooks/README.md`](notebooks/README.md) for the full pipeline details.

### 4.3 Modelling & Evaluation

Three models are evaluated — Logistic Regression (baseline), Random Forest, and XGBoost — assessed on ROC-AUC, F1-Score, PR-AUC, and Confusion Matrix. SHAP values are used to explain predictions and identify top drivers of subscription. See [`models/README.md`](models/README.md) for model selection rationale, evaluation metrics, and explainability approach.

### 4.4 ML System Design Considerations

| Consideration | Approach |
|---|---|
| **Reliability** | Return calibrated probabilities; flag low-confidence predictions rather than forcing binary output |
| **Fairness** | Audit predictions across `age`, `marital`, `job` to detect and mitigate discriminatory patterns |
| **Adaptability** | Document a retraining strategy based on performance monitoring as data distributions shift |
| **Business vs ML Objectives** | ML objective = maximise F1/AUC. Business objective = increase campaign ROI. Quantify cost savings from targeting top 20% predicted subscribers vs. random outreach |

### 4.5 Expected Deliverables

- Exploratory Data Analysis (EDA) report with visualisations
- Preprocessing pipeline (reproducible, documented)
- Trained and tuned models with performance comparison
- SHAP-based feature importance analysis
- Business impact summary: projected ROI improvement from targeted outreach
- Final project report and presentation

---

## 5. Risks & Unknowns

| Risk | Detail | Mitigation |
|---|---|---|
| **Class Imbalance** | Only 12% of records are positive (subscribed). Accuracy can look good while the model fails to identify likely subscribers. | Use PR-AUC and F1-Score instead of raw accuracy. Apply SMOTE or class weights. |
| **Sampling / Representativeness** | Data is from a single Portuguese bank over a specific time period (May 2008 – Nov 2010). Patterns may not generalise to other institutions or modern campaigns. | Document limitations clearly; treat findings as bank-specific. |
| **Data Leakage** | `duration` measures call length, which is only available after the call ends — at which point the outcome is already known. | Exclude `duration` from all production models. |
| **Proxy & Fairness Concerns** | Variables like `age`, `job`, `marital`, and `education` can act as proxies for protected characteristics, risking biased recommendations if used blindly. |
| **Scope Clarity** | Business priorities need further clarification, is the goal to maximise profit or lift the acceptance rate? These lead to different threshold decisions. | Engage stakeholders early to align on the primary business metric. |

---

## 6. Team & Roles

| Name | Role | Responsibilities |
|---|---|---|
| Madina Jumabayeva | Data Lead | Data cleaning, preprocessing pipeline |
| Ryan | Visualisation / Storytelling Lead | EDA visualisations, business narrative |
| Haichen Zhang | Modelling / EDA Lead | Model training, evaluation, EDA |
| Melkamu Gishu | Modelling / EDA Lead | Model tuning, SHAP analysis, reporting |

---
## 7. Self-reflection video:

pending links from group memebers.

---
