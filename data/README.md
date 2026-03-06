# Data

## Dataset

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
| `duration` | Numeric | Last contact duration in seconds. See data leakage note |

**Campaign History**

| Variable | Type | Description |
|---|---|---|
| `campaign` | Numeric | Number of contacts made during this campaign |
| `pdays` | Numeric | Days since last contact from a previous campaign (-1 = never contacted before) |
| `previous` | Numeric | Number of contacts made before this campaign |
| `poutcome` | Categorical | Outcome of the previous campaign: failure, other, success, unknown |

---

## Folder Contents

```
data/
├── raw/              # Original, unmodified dataset files (git-ignored)
├── processed/        # Cleaned and feature-engineered datasets
└── sql/              # SQL scripts for data extraction or querying
```

> Do not commit raw data files directly. The `data/raw/` folder is listed in `.gitignore`. Use `.gitkeep` to preserve the empty folder in the repo.

See `data/processed/README.md` for a full log of cleaning and transformation steps applied to the raw data.
