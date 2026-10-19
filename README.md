# CSET485 – AI and Society · Assignment 1

**Stress-testing a credit-approval model on the German Credit Data**

| | |
|---|---|
| Student | Udbhav |
| Enrollment no. | S24CSEU0095 |
| Dataset (last digit 5) | German Credit Data – UCI Statlog (1,000 applicants, 20 attributes) |
| Random seed (last 3 digits 095) | random_state = 95, 70% train / 30% test |

## Files

| File | Description |
|---|---|
| AI_ASSIGNMENT.pdf | Final report |
| AI_ASSIGNMENT.docx | Editable Word version of the report |
| AI_SOCIETY_PROJECT.ipynb | Jupyter notebook with the code and outputs |

## Contents of the notebook

- Data loading from UCI and target encoding (approve = 1 good, 0 bad)
- Preprocessing: missing values, outliers (IQR), log transform, one-hot encoding, train/test split, scaling
- Model A (linear regression) and Model B (logistic regression)
- Subgroup analysis by sex (Simpson's paradox check)
- Error analysis and subgroup audit by age
- Fairness sweep over thresholds 0.05 to 0.95 (young vs older) and trade-off chart

## How to run

Open AI_SOCIETY_PROJECT.ipynb in Google Colab or Jupyter and choose Run all.
The data is downloaded from:
https://archive.ics.uci.edu/ml/machine-learning-databases/statlog/german/german.data
