# Models

## Model Selection

| Model | Role | Rationale |
|---|---|---|
| Logistic Regression | Baseline | Interpretable, fast, good for establishing a performance floor |
| Random Forest | Intermediate | Handles non-linearity; provides feature importance scores |
| XGBoost | Primary | State-of-the-art for tabular data; highest expected performance |

---

## Objective Function & Evaluation Metrics

Classification tasks use log loss / cross-entropy as the training objective. For evaluation:

| Metric | Rationale |
|---|---|
| ROC-AUC | Overall discriminative ability of the model |
| F1-Score | Balances precision and recall under class imbalance |
| PR-AUC | Preferred over raw accuracy given the class imbalance |
| Precision & Recall | Reported separately to support business decision-making |
| Confusion Matrix | Visual summary of prediction errors |

> **Business framing:** False negatives (missing a likely subscriber) are more costly than false positives (contacting a low-probability client). The decision threshold will be tuned accordingly.

---

## Explainability

SHAP (SHapley Additive Explanations) values will be used to:
- Identify the top predictors of subscription globally
- Explain individual predictions for business stakeholders
- Detect and document fairness concerns across demographic groups
