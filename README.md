4. Methodology
4.1 Problem Framing
This is a binary classification problem where the model predicts one of two outcomes: subscription (yes) or non-subscription (no). Following the course framework, we will also explore framing this as a regression problem (predicting subscription probability) to enable threshold tuning based on business cost-benefit analysis.
4.2 Data Preparation Pipeline
Data Cleaning:
•	Handle missing values and 'unknown' categorical encodings
•	Validate numeric ranges and detect outliers
•	Check for duplicate records
Feature Engineering:
•	Contact Recency Bins: Transform pdays into categorical bins (Never Contacted, Recently Contacted <30 days, Long Ago >30 days)
•	Campaign Intensity: Interaction term between campaign and previous contacts
•	Financial Health Score: Composite feature from balance, housing, loan, default
•	Previous Success Indicator: Binary flag for previous campaign success
Encoding Strategy:
•	One-hot encoding for nominal categorical variables (job, marital, education, contact, month, poutcome)
•	Binary encoding for yes/no variables (housing, loan, default)
Feature Scaling:
•	StandardScaler for distance-based models (Logistic Regression)
•	No scaling required for tree-based models (Random Forest, XGBoost)
Data Split:
•	Training: 70% (~31,500 samples)
•	Validation: 15% (~6,750 samples)
•	Test: 15% (~6,750 samples)
4.3 Model Selection & Training
Baseline Model:
Logistic Regression - Establishes performance floor, provides interpretable coefficients, fast training and inference
