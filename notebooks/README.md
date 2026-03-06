# Notebooks

## Local Setup

**1. Clone the repository**
```bash
git clone https://github.com/melkyed/DSI-Cohort8-ML-1.git
cd DSI-Cohort8-ML-1
```

**2. Create and activate a virtual environment**
```bash
uv venv ml-team1-env --python 3.11
source ml-team1-env/bin/activate        # Mac/Linux
venv\Scripts\activate           # Windows
```

**3. Install dependencies**
```bash
uv pip install -r requirements.txt
```

**4. Download the dataset**

Download the Bank Marketing dataset from the [UCI ML Repository](https://archive.ics.uci.edu/dataset/222/bank+marketing) and place the raw files in:
```
data/raw/
```

---

## Git Workflow

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

---

## Data Preparation Pipeline

### Data Cleaning
- Handle missing values and `unknown` categorical encodings
- Validate numeric ranges and detect outliers
- Check for duplicate records

### Feature Engineering

| Feature | Description |
|---|---|
| Contact Recency Bins | Transform `pdays` into bins: Never Contacted / Recently Contacted (<30 days) / Long Ago (>30 days) |
| Campaign Intensity | Interaction term between `campaign` and `previous` contacts |
| Financial Health Score | Composite feature from `balance`, `housing`, `loan`, `default` |
| Previous Success Indicator | Binary flag for previous campaign success |

### Encoding Strategy
- One-hot encoding for nominal categoricals: `job`, `marital`, `education`, `contact`, `month`, `poutcome`
- Binary encoding for yes/no variables: `housing`, `loan`, `default`

### Feature Scaling
- `StandardScaler` for distance-based models (Logistic Regression)
- No scaling required for tree-based models (Random Forest, XGBoost)

### Data Split

| Split | Proportion | Approx. Samples |
|---|---|---|
| Training | 70% | ~31,500 |
| Validation | 15% | ~6,750 |
| Test | 15% | ~6,750 |
