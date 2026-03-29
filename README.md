# Bank Loan Analysis using SQL & Tableau

## Project Overview
This project presents an end-to-end **Bank Loan Analysis** using **SQL for data analysis** and **Tableau for data visualization**.  
The objective is to monitor lending performance, analyze borrower behavior, and evaluate loan portfolio health using real-world banking KPIs.

The analysis focuses on:
- Loan application trends
- Funded vs received amounts
- Interest rate and DTI evaluation
- Good Loan vs Bad Loan classification
- Insights by region, loan purpose, term, and employment length

---

## Business Problem
Banks require a consolidated reporting system to:
- Track loan performance over time
- Identify high-risk and low-risk loans
- Monitor repayment behavior
- Enable data-driven lending decisions

This project addresses these requirements through **SQL-driven KPIs** and **interactive Tableau dashboards**.

---

## Tools & Technologies
- **SQL** – KPI calculations and aggregations  
- **Tableau Public** – Interactive dashboards and data storytelling  
- **CSV Dataset** – Bank loan data  

---

## Dataset Information
- **File Name:** `financial_loan.csv`
- **Data Type:** Structured loan-level data
- **Granularity:** One row per loan application

### Key Columns
- `id` – Loan ID  
- `issue_date` – Loan issue date  
- `loan_amount` – Funded loan amount  
- `total_payment` – Amount received from borrower  
- `int_rate` – Interest rate  
- `dti` – Debt-to-Income ratio  
- `loan_status` – Fully Paid / Current / Charged Off  
- `term` – Loan duration  
- `emp_length` – Employment length  
- `purpose` – Loan purpose  
- `address_state` – Borrower state  

---

## Key KPIs Calculated
- Total Loan Applications  
- Month-to-Date (MTD) Loan Applications  
- Previous Month-to-Date (PMTD) Applications  
- Total Funded Amount  
- Total Amount Received  
- Average Interest Rate  
- Average Debt-to-Income Ratio (DTI)  
- Good Loan Percentage  
- Bad Loan Percentage  

---

## SQL Queries Used

```sql
-- View data
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
