# Bank Loan Analysis using SQL & Tableau

## 📌 Project Overview
This project presents an end-to-end **Bank Loan Analysis** using **SQL for data analysis** and **Tableau for visualization**.  
The objective is to monitor lending performance, analyze borrower behavior, and evaluate portfolio health using real-world banking KPIs.

The project covers:
- Loan application trends
- Funded vs received amounts
- Interest rate & DTI analysis
- Good Loan vs Bad Loan classification
- Region, purpose, term, and employment-based insights

---

## 🎯 Business Problem
Banks need a consolidated reporting system to:
- Track loan performance over time
- Identify high-risk and low-risk loans
- Monitor repayment behavior
- Support data-driven lending decisions

This project solves that by creating **SQL-driven KPIs** and **interactive Tableau dashboards**.

---

## 🛠 Tools & Technologies
- **SQL** – KPI calculations & data aggregation  
- **Tableau Public** – Interactive dashboards  
- **CSV Dataset** – Bank loan data  

---

## 📊 Key KPIs Calculated
- Total Loan Applications  
- Month-to-Date (MTD) Loan Applications  
- Previous Month-to-Date (PMTD) Applications  
- Total Funded Amount  
- Total Amount Received  
- Average Interest Rate  
- Average Debt-to-Income Ratio (DTI)  
- Good Loan vs Bad Loan Percentage  

---

## 🧮 Complete SQL Queries Used

```sql
SELECT * FROM bank_loan_data;

-- Total Loan Applications
SELECT COUNT(id) AS Total_Applications FROM bank_loan_data;

-- MTD Loan Applications
SELECT COUNT(id) AS MTD_Applications
FROM bank_loan_data
WHERE MONTH(issue_date) = 12;

-- PMTD Loan Applications
SELECT COUNT(id) AS PMTD_Applications
FROM bank_loan_data
WHERE MONTH(issue_date) = 11;

-- Total Funded Amount
SELECT SUM(loan_amount) AS Total_Funded_Amount
FROM bank_loan_data;

-- MTD Funded Amount
SELECT SUM(loan_amount) AS MTD_Funded_Amount
FROM bank_loan_data
WHERE MONTH(issue_date) = 12;

-- PMTD Funded Amount
SELECT SUM(loan_amount) AS PMTD_Funded_Amount
FROM bank_loan_data
WHERE MONTH(issue_date) = 11;

-- Total Amount Received
SELECT SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data;

-- Average Interest Rate
SELECT AVG(int_rate) * 100 AS Avg_Interest_Rate
FROM bank_loan_data;

-- Average DTI
SELECT AVG(dti) * 100 AS Avg_DTI
FROM bank_loan_data;

-- Good Loan Percentage
SELECT 
(COUNT(CASE WHEN loan_status IN ('Fully Paid','Current') THEN id END) * 100.0)
/ COUNT(id) AS Good_Loan_Percentage
FROM bank_loan_data;

-- Bad Loan Percentage
SELECT 
(COUNT(CASE WHEN loan_status = 'Charged Off' THEN id END) * 100.0)
/ COUNT(id) AS Bad_Loan_Percentage
FROM bank_loan_data;

-- Loan Status Summary
SELECT 
loan_status,
COUNT(id) AS Loan_Count,
SUM(loan_amount) AS Total_Funded,
SUM(total_payment) AS Total_Received,
AVG(int_rate * 100) AS Avg_Interest_Rate,
AVG(dti * 100) AS Avg_DTI
FROM bank_loan_data
GROUP BY loan_status;

-- Monthly Trend
SELECT 
MONTH(issue_date) AS Month_Number,
DATENAME(MONTH, issue_date) AS Month_Name,
COUNT(id) AS Applications,
SUM(loan_amount) AS Funded_Amount,
SUM(total_payment) AS Amount_Received
FROM bank_loan_data
GROUP BY MONTH(issue_date), DATENAME(MONTH, issue_date)
ORDER BY Month_Number;

-- State-wise Analysis
SELECT 
address_state,
COUNT(id) AS Applications,
SUM(loan_amount) AS Funded_Amount,
SUM(total_payment) AS Amount_Received
FROM bank_loan_data
GROUP BY address_state;

-- Loan Term Analysis
SELECT 
term,
COUNT(id) AS Applications,
SUM(loan_amount) AS Funded_Amount,
SUM(total_payment) AS Amount_Received
FROM bank_loan_data
GROUP BY term;

-- Employee Length Analysis
SELECT 
emp_length,
COUNT(id) AS Applications,
SUM(loan_amount) AS Funded_Amount,
SUM(total_payment) AS Amount_Received
FROM bank_loan_data
GROUP BY emp_length;

-- Loan Purpose Analysis
SELECT 
purpose,
COUNT(id) AS Applications,
SUM(loan_amount) AS Funded_Amount,
SUM(total_payment) AS Amount_Received
FROM bank_loan_data
GROUP BY purpose;

# Bank Loan Analysis – Tableau Dashboard

## Tableau Dashboard Information
- Tool: Tableau Public
- Data Source: financial_loan.csv
- Calculated Fields:
  - Month-to-Date (MTD)
  - Previous Month-to-Date (PMTD)
  - Month-over-Month (MoM) Growth
  - Good Loan vs Bad Loan Classification Logic

---

## Dashboards Created

### Dashboard 1: Summary
This dashboard provides a high-level overview of loan performance.
- KPI Cards
- Total Loan Applications
- Total Funded Amount
- Total Amount Received
- Average Interest Rate
- Average Debt-to-Income Ratio (DTI)
- Good Loan vs Bad Loan comparison

---

### Dashboard 2: Overview
This dashboard focuses on trend-based and categorical insights.
- Monthly Loan Trend (Line Chart)
- State-wise Loan Distribution (Filled Map)
- Loan Term Analysis (Donut Chart)
- Employment Length Analysis (Bar Chart)
- Loan Purpose Breakdown (Bar Chart)
- Home Ownership Analysis (Tree Map)

---

### Dashboard 3: Details
This dashboard provides detailed, loan-level analysis.
- Complete loan-level tabular data
- Filters available for:
  - Loan Status
  - State
  - Loan Purpose
  - Loan Term

---

## Tableau Public Dashboard Link
View Live Dashboard:  
https://public.tableau.com/app/profile/dev.dixit2546/viz/BankLoanReport_17747909445300/DETAIL?publish=yes

---

## Key Insights
- Majority of loans are Fully Paid or Current
- Charged-off loans represent higher financial risk
- Certain states contribute most to overall loan volume
- Debt Consolidation is the most common loan purpose
- Borrowers with longer employment length show better repayment patterns

---

## Author
Dev Dixit  
B.Tech – Computer Science  
Skills: SQL, Tableau, Data Analytics

---

## License
This project is licensed under the MIT License.


