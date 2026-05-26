# 📊 Financial Loan Data Analysis Project

##  1. Project Overview

This project focuses on analyzing a financial loan dataset to understand borrower behavior, loan performance, and risk patterns.

The workflow includes:

* Data cleaning and preprocessing using Python
* Data analysis using MySQL
* Data visualization using Power BI

The goal is to derive meaningful business insights such as default risk, profitability, and customer segmentation.

---

##  2. Dataset Details

* **Total Records:** 38,576
* **Total Columns:** 24

### Data Types:

* Numerical: 9 columns
* Categorical: 15 columns

###  Key Features:

* Borrower details → income, employment, home ownership
* Loan details → amount, term, interest rate
* Loan status → loan_status, total_payment
* Time-based → issue_date, payment dates

---

##  3. Data Loading

The dataset was loaded using Python Pandas:

```python
import pandas as pd

# Load using file path
file_path = r"F:\SQL works\Power BI project\financial_loan.csv"
df = pd.read_csv(file_path)
```

✔ Data successfully loaded into a DataFrame for analysis.

---

##  4. Data Cleaning

###  4.1 Missing Value Analysis

```python
df.isnull().sum()
```

###  Findings:

* Only **emp_title** had missing values:

  * 1,438 missing (~3.7%)
* All other columns were complete

---

###  4.2 Handling Missing Values

```python
df['emp_title'] = df['emp_title'].fillna('Unknown')
```

###  Justification:

* emp_title is not critical for risk analysis
* Preserved all rows (no data loss)
* Ensured dataset consistency

---

##  5. Data Transformation

###  5.1 Date Conversion

```python
date_cols = ['issue_date', 'last_payment_date', 'last_credit_pull_date', 'next_payment_date']

for col in date_cols:
    df[col] = pd.to_datetime(df[col], dayfirst=True)
```

###  Reason:

* Original format was **DD-MM-YYYY**
* Required for time-based analysis

---

###  5.2 Term Conversion

```python
df['term'] = df['term'].str.extract('(\d+)').astype(int)
```

✔ Converted from "36 months" → 36

---

###  5.3 Employment Length Conversion

```python
df['emp_length'] = df['emp_length'].str.extract('(\d+)')
df['emp_length'] = df['emp_length'].fillna(0).astype(int)
```

✔ Converted to numeric format for analysis

---

##  6. Feature Engineering

###  Risk Ratio

```python
df['risk_ratio'] = df['loan_amount'] / df['annual_income']
```

✔ Measures borrower risk based on income

---

###  Profit Calculation

```python
df['profit'] = df['total_payment'] - df['loan_amount']
```

✔ Measures lender profitability

---

##  7. Data Export

Cleaned dataset saved as:

```python
df.to_csv("financial_loan_cleaned.csv", index=False)
```

###  Ready for:

* Power BI dashboard
* SQL analysis
* Machine learning

---

##  8. MySQL Analysis

### Database Creation

```sql
CREATE DATABASE financial_loan_project;
USE financial_loan_project;
```

### Sample Analysis Queries

```sql
-- Total Loans
SELECT COUNT(*) FROM financial_loan;

-- Total Loan Amount
SELECT SUM(loan_amount) FROM financial_loan;

-- Default Rate
SELECT
    ROUND(SUM(CASE WHEN loan_status = 'Charged Off' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2)
    AS default_rate
FROM financial_loan;
```

---

##  9. Power BI Dashboard

### Key KPIs:

* Total Loan Applications
* Total Funded Amount
* Total Amount Received
* Average Interest Rate
* Average DTI
* Default Rate

### Visualizations:

* Loan Status Distribution
* Monthly Loan Trends
* State-wise Loan Analysis
* Purpose-wise Loan Distribution
* Risk Analysis (using risk_ratio)

---

##  10. Key Insights

* Majority of loans are fully paid (~86%)
* High risk_ratio customers are more likely to default
* Interest rates vary significantly across grades
* Certain states contribute higher loan volumes

---

##  11. Tools & Technologies Used

* Python (Pandas)
* MySQL
* Power BI

---

##  12. Conclusion

This project demonstrates an end-to-end data analytics workflow:

✔ Data Cleaning (Python)
✔ Data Analysis (MySQL)
✔ Data Visualization (Power BI)

The final dashboard provides actionable insights into loan performance, risk assessment, and profitability, making it suitable for real-world business decision-making.

