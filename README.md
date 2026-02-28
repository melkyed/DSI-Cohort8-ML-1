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


**Description**

The dataset is organized as a table with 17 variables and 45,211 records, mixing demographic, financial, and campaign related attributes. These include personal characteristics such as age, job, and marital status; financial indicators such as balance; and marketing interaction details such as duration of the last call, campaign contact count, and pdays, which often appears as –1 to indicate no previous contact. Many entries contain the placeholder “unknown,” especially in fields like education, contact, and poutcome, as seen in rows where job is “blue collar” or “admin.” and the contact method is listed as “unknown.”


**3 Risks & Unknowns**

- Class imbalance: this dataset is imbalanced with ony 12% in the class we are interested (subcribed customers)
    - so accuracy can look good while the model is useless for identifying likely subscribers.
    - We would recommend to use PR-AUC instead of raw accuracy.

- Sampling / representativeness: Data is from a specific bank (portugalese), geography, and a specific time period.
    - patterns may not generalize to other institutions or later years.(May 2018 to Nov 2010)
    - dataset outdated, may not offfer best data set for the model to predict modern problems.

- Data Leakage:
    - duration column is measuring the length of the call, and this infoamtion is not available ahead of the call.
    - hence should not be used for modelling.

- Proxy and fairness concerns: 
    - Variables like age, job, marital, education can act as proxies for protected characteristics or socioeconomic status—risking biased recommendations if used blindly.

Scope:
- we will need to work with stateholders to further clarify their business priorities. 
- for example, is business more interested in maximizing profit or in lifting the acceptance rate.

**5 Roles and Tasks:**

| [Madina] | [Data Lead - Data Cleaning] 

| [Ryan] | [Visualization/Storytelling Lead]

| [Haichen] | [Modeling/EDA Lead/Visualization] 

| [Mel] | [Modeling/EDA Lead] 

| [Group effort] | [Reporting] 
