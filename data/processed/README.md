**Data Cleaning**
- Removed the duration column to prevent data leakage (since it is known only after the call)
- Stripped whitespace from string columns to prevent inconsistencies
- Converted the target variable (y) from yes/no to numeric (0/1)
- Created a new feature previously_contacted based on pdays
- Removed the original pdays column for improved interpretability
- Checked for and removed duplicate records
- Saved the cleaned dataset to data/processed/bank_cleaned.csv
- Ensured raw data remains unchanged in data/raw/

