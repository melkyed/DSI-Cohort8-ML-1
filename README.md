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
**Business Motivation**

Marketing campaigns conducted through phone calls require significant time, effort, and financial resources. However, only a small percentage of clients actually subscribe to the term deposit product. As a result, the bank spends resources contacting many customers who are unlikely to be interested.

The goal of this project is to build a machine learning model that predicts whether a bank client will subscribe to a term deposit based on demographic information, financial characteristics, and previous campaign interaction history.

By identifying clients who are more likely to subscribe before contacting them, the bank can increase campaign efficiency, reduce unnecessary calls, improve conversion rates, and optimize the allocation of marketing resources.

In addition, we want to understand which factors most influence whether a client says yes. By identifying these key drivers, the bank can improve its marketing strategy and make more informed decisions about future campaigns.

**Dataset**
Dataset name: Bank Marketing
Source / link: https://archive.ics.uci.edu/dataset/222/bank+marketing

Characteristics and data type
•   age — numeric, continuous
•   job — categorical (management, technician, services, etc.)
•   marital — categorical (married, single, divorced)
•   education — categorical (primary, secondary, tertiary unknown)
•   default — binary (yes/no)
•   balance — numeric, can be negative
•   housing — binary (yes/no)
•   loan — binary (yes/no)
•   contact — categorical (mostly “unknown” in your sample)
•   day — numeric (day of month)
•   month — categorical (mostly “may” in your sample)
•   duration — numeric (call duration in seconds)
•   campaign — numeric (number of contacts during this campaign)
•   pdays — numeric (days since last contact; -1 means “never contacted before”)
•   previous — numeric (number of previous contacts)
•   poutcome — categorical (outcome of previous campaign)
•   y — target variable (yes/no)

Description
The dataset is organized as a table with 17 variables and 45,211 records, mixing demographic, financial, and campaign related attributes. These include personal characteristics such as age, job, and marital status; financial indicators such as balance; and marketing interaction details such as duration of the last call, campaign contact count, and pdays, which often appears as –1 to indicate no previous contact. Many entries contain the placeholder “unknown,” especially in fields like education, contact, and poutcome, as seen in rows where job is “blue collar” or “admin.” and the contact method is listed as “unknown.”


