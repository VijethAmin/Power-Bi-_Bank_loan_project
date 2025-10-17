Project Report: Financial Loan Analysis Dashboard in Power BI


Objective:
The main objective of this project is to analyze loan application and payment data to uncover trends in borrower profiles, loan performance, and risk levels. The dashboard provides key insights into loan distribution, default rates, customer demographics, and repayment behavior to support better financial decision-making.

Problem Statement:
Banks and financial institutions handle large volumes of loan data but struggle to quickly identify which loans are performing well, which borrower groups are risky, and how income or credit grades impact repayment.
This project aims to transform raw loan data into an interactive Power BI dashboard that simplifies performance monitoring and risk analysis.

Dataset Overview:
The dataset used in this project consists of 38,234 loan records with key features about loan applications, borrower details, and repayment metrics.

Key Columns Used:

Column Name	Description
loan_status	Indicates if the loan was Fully Paid, Current, or Charged Off
application_type	Type of application (INDIVIDUAL or JOINT)
emp_length	Employment length of borrower
grade / sub_grade	Credit grade assigned by the lender
home_ownership	Indicates whether borrower owns, rents, or has a mortgage
purpose	Reason for the loan (e.g., debt consolidation, credit card, home improvement)
term	Loan term (36 or 60 months)
verification_status	Whether income was verified
annual_income	Borrower’s annual income
dti	Debt-to-Income ratio
installment	Monthly installment amount
int_rate	Interest rate of the loan
loan_amount	Amount of loan issued
total_acc	Total number of borrower’s credit accounts
total_payment	Total payment made till date

Data Cleaning & Transformation Steps:
Removed Irrelevant Columns: Unused columns like issue_date, id, or text-based IDs were removed.
Handled Missing Values: Replaced or removed nulls in annual_income, int_rate, and dti fields.

Changed Data Types:
Converted loan_amount, annual_income, total_payment, and installment to Whole Numbers / Decimal Numbers.
Changed int_rate and dti to Percentage format.

Created New Calculated Columns (DAX):

Default Rate = DIVIDE(
    CALCULATE(COUNTROWS(Data), Data[loan_status] = "Charged Off"),
    COUNTROWS(Data),
    0
)

Loan to Income Ratio = DIVIDE(SUM(Data[loan_amount]), SUM(Data[annual_income]), 0)

Payment Rate = DIVIDE(SUM(Data[total_payment]), SUM(Data[loan_amount]), 0)

Dashboard Design and Visualizations:
Loan Portfolio Overview

KPIs (Cards):

Total Loan Amount = SUM(loan_amount)
Total Payments Received = SUM(total_payment)
Average Interest Rate = AVERAGE(int_rate)
Default Rate % = Default Rate

Visuals:

Donut Chart: Loan Status Distribution (loan_status)
Bar Chart: Loan Amount by Loan Purpose (purpose)
Clustered Column Chart: Loan Grade vs Loan Amount (grade by loan_status)

Borrower Profile Insights

Visuals:
Histogram: Annual Income Distribution (annual_income)
Column Chart: Home Ownership vs Loan Amount (home_ownership)
Clustered Column Chart: Employment Length vs Loan Status (emp_length)
Pie Chart: Application Type Distribution (application_type)

Insight Example:
Borrowers with “10+ years” experience are more likely to have higher loan amounts.
Majority of loans are “INDIVIDUAL” applications.

Risk & Performance Analysis

Visuals:
Scatter Plot: Debt-to-Income (DTI) vs Loan Amount (colored by loan_status)
Stacked Column Chart: Sub-Grade vs Default Rate (sub_grade by loan_status)
Bar Chart: Loan Term (36 months vs 60 months) by Loan Status
Card: Average Installment Amount

Insights:
Loans with higher dti values show greater risk of being “Charged Off.”
60-month loans show higher defaults compared to 36-month ones.
“Debt Consolidation” purpose dominates the dataset.

Key Insights from the Dashboard:

Loan Performance: Approximately X% of loans are charged off, indicating potential risk areas.
Income Trend: Higher-income borrowers tend to borrow more but show lower default rates.
Interest Impact: Loans with higher int_rate often correlate with poorer loan grades.
Purpose Analysis: “Debt consolidation” and “Credit Card” are the top loan purposes.
Term-wise Default: 60-month term loans have a noticeably higher default percentage.
