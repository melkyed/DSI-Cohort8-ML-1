# DSI-Cohort8-ML-1
### Optimizing Bank Marketing Campaigns: Data-Driven Targeting for Term Deposits
**Data Sciences Institute — Cohort 8 | Machine Learning Stream**

---

## Table of Contents
1. [Project Overview](#1-project-overview)
2. [Dataset & Variables](#2-dataset--variables)
3. [Folder Structure & Setup](#3-folder-structure--setup)
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

The dataset is organised as a table mixing demographic, financial, and campaign-related attributes. Personal characteristics include age, job, and marital status; financial indicators include balance; and marketing interaction details include duration of the last call, campaign contact count, and `pdays` (which appears as `-1` to indicate no previous contact). Many entries contain the placeholder `"unknown"`, especially in fields like `education`, `contact`, and `poutcome`.

### Target Variable

| Variable | Type | Values |
|---|---|---|
| `y` | Binary | `yes` = subscribed to term deposit, `no` = did not subscribe |

### Predictor Variables

**Client Demographics**

| Variable | Type | Description |
|---|---|---|
| `age` | Numeric, continuous | Age of the client |
| `job` | Categorical | Job type: management, technician, services, admin, blue-collar, etc. |
| `marital` | Categorical | Marital status: married, single, divorced |
| `education` | Categorical | Education level: primary, secondary, tertiary, unknown |
| `default` | Binary | Has credit in default? (yes, no) |
| `balance` | Numeric | Average yearly account balance in euros — can be negative |
| `housing` | Binary | Has a housing loan? (yes, no) |
| `loan` | Binary | Has a personal loan? (yes, no) |

**Campaign Contact Info**

| Variable | Type | Description |
|---|---|---|
| `contact` | Categorical | Communication type: cellular, telephone, unknown |
| `day` | Numeric | Last contact day of the month |
| `month` | Categorical | Last contact month: jan, feb, ..., dec |
| `duration` | Numeric | Last contact duration in seconds ⚠️ See data leakage note |

**Campaign History**

| Variable | Type | Description |
|---|---|---|
| `campaign` | Numeric | Number of contacts made during this campaign |
| `pdays` | Numeric | Days since last contact from a previous campaign (-1 = never contacted before) |
| `previous` | Numeric | Number of contacts made before this campaign |
| `poutcome` | Categorical | Outcome of the previous campaign: failure, other, success, unknown |

---

## 3. Folder Structure & Setup

### Repository Structure

```
DSI-Cohort8-ML-1/
│
├── data/
│   ├── raw/              # Original, unmodified dataset files
│   ├── processed/        # Cleaned and feature-engineered datasets
│   └── sql/              # SQL scripts for data extraction or querying
│
├── experiments/          # Notebooks and scripts for model experiments
├── models/               # Saved model artefacts (.pkl, .joblib, etc.)
├── reports/              # Final reports, visualisations, presentation decks
├── src/                  # Reusable source code (pipelines, utilities, etc.)
│
├── README.md
└── .gitignore
```

### Local Setup

**1. Clone the repository**
```bash
git clone https://github.com/melkyed/DSI-Cohort8-ML-1.git
cd DSI-Cohort8-ML-1
```

**2. Create and activate a virtual environment**
```bash
python -m venv ml-team1-env --python 3.11
source ml-team1-env/bin/activate        # Mac/Linux
venv\Scripts\activate           # Windows
```

**3. Install dependencies**
```bash
pip install -r requirements.txt
```

**4. Download the dataset**

Download the Bank Marketing dataset from the [UCI ML Repository](https://archive.ics.uci.edu/dataset/222/bank+marketing) and place the raw files in:
```
data/raw/
```

### Git Workflow

```bash
# Always pull before starting work
git pull origin main

# Create a branch for your feature or section
git checkout -b feature/your-feature-name

# Stage, commit, and push
git add .
git commit -m "descriptive commit message"
git push origin feature/your-feature-name

# Open a Pull Request on GitHub for review before merging to main
```

> 🔒 Do not commit raw data files directly. The `data/raw/` folder is listed in `.gitignore`. Use `.gitkeep` to preserve the empty folder in the repo.

---

## 4. Methodology

**Primary Objective:** Develop and evaluate a predictive ML model that determines the likelihood of a client subscribing to a term deposit using demographic, financial, and historical campaign data.

**Secondary Objectives:**
- Identify and rank the most influential customer attributes driving subscription decisions
- Isolate high-probability customer segments with conversion rates substantially above the historical campaign baseline
- Analyse the precision-recall trade-off and establish an optimal classification threshold aligned with the bank's marketing budget and revenue goals

### 4.1 Problem Framing

This is a binary classification problem: the output is either `yes` (subscribed) or `no` (did not subscribe). We may also explore framing this as a regression problem (predicting subscription probability) to enable threshold tuning based on business cost-benefit analysis.

### 4.2 Data Preparation Pipeline

**Data Cleaning**
- Handle missing values and `unknown` categorical encodings
- Validate numeric ranges and detect outliers
- Check for duplicate records

**Feature Engineering**

| Feature | Description |
|---|---|
| Contact Recency Bins | Transform `pdays` into bins: Never Contacted / Recently Contacted (<30 days) / Long Ago (>30 days) |
| Campaign Intensity | Interaction term between `campaign` and `previous` contacts |
| Financial Health Score | Composite feature from `balance`, `housing`, `loan`, `default` |
| Previous Success Indicator | Binary flag for previous campaign success |

**Encoding Strategy**
- One-hot encoding for nominal categoricals: `job`, `marital`, `education`, `contact`, `month`, `poutcome`
- Binary encoding for yes/no variables: `housing`, `loan`, `default`

**Feature Scaling**
- `StandardScaler` for distance-based models (Logistic Regression)
- No scaling required for tree-based models (Random Forest, XGBoost)

**Data Split**

| Split | Proportion | Approx. Samples |
|---|---|---|
| Training | 70% | ~31,500 |
| Validation | 15% | ~6,750 |
| Test | 15% | ~6,750 |

### 4.3 Model Selection

| Model | Role | Rationale |
|---|---|---|
| Logistic Regression | Baseline | Interpretable, fast, good for establishing a performance floor |
| Random Forest | Intermediate | Handles non-linearity; provides feature importance scores |
| XGBoost | Primary | State-of-the-art for tabular data; highest expected performance |

### 4.4 Objective Function & Evaluation Metrics

Classification tasks use log loss / cross-entropy as the training objective. For evaluation:

| Metric | Rationale |
|---|---|
| ROC-AUC | Overall discriminative ability of the model |
| F1-Score | Balances precision and recall under class imbalance |
| PR-AUC | Preferred over raw accuracy given the class imbalance |
| Precision & Recall | Reported separately to support business decision-making |
| Confusion Matrix | Visual summary of prediction errors |

> **Business framing:** False negatives (missing a likely subscriber) are more costly than false positives (contacting a low-probability client). The decision threshold will be tuned accordingly.

### 4.5 Explainability

SHAP (SHapley Additive Explanations) values will be used to:
- Identify the top predictors of subscription globally
- Explain individual predictions for business stakeholders
- Detect and document fairness concerns across demographic groups

### 4.6 ML System Design Considerations

| Consideration | Approach |
|---|---|
| **Reliability** | Return calibrated probabilities; flag low-confidence predictions rather than forcing binary output |
| **Fairness** | Audit predictions across `age`, `marital`, `job` to detect and mitigate discriminatory patterns |
| **Adaptability** | Document a retraining strategy based on performance monitoring as data distributions shift |
| **Business vs ML Objectives** | ML objective = maximise F1/AUC. Business objective = increase campaign ROI. Quantify cost savings from targeting top 20% predicted subscribers vs. random outreach |

### 4.7 Expected Deliverables

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
| **Data Leakage** | `duration` measures call length, which is only available after the call ends  at which point the outcome is already known. | Exclude `duration` from all production models. |
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

