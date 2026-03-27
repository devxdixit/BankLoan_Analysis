# BankLoan_Analysis
# 📊 Bank Loan Analysis | SQL + Tableau Portfolio Project

## 🔹 Project Overview
This project is an **end-to-end Data Analyst portfolio project** focused on analysing **bank loan data** using **MS SQL Server** and **Tableau**.

The objective of this project is to help banks and financial institutions:
- Monitor loan performance
- Analyse funding and repayment trends
- Identify Good Loans vs Bad Loans
- Understand borrower behaviour and regional performance
- Make data-driven lending decisions

All dashboards are built in **Tableau** using data extracted and processed through **SQL**.

---

## 🔹 Tools & Technologies Used
- **Database**: MS SQL Server  
- **Query Language**: SQL  
- **Visualization Tool**: Tableau  
- **Documentation**: PDF / DOCX  
- **Version Control**: GitHub  

---

## 🔹 Business Problem
Banks deal with thousands of loan applications and repayments. Without proper analysis, it becomes difficult to:
- Track loan quality
- Measure risk exposure
- Monitor repayment performance
- Identify profitable and risky borrower segments

This project solves these challenges by creating **interactive Tableau dashboards** backed by **SQL-driven KPIs**.

---

## 🔹 Key Performance Indicators (KPIs)

### 📌 Summary KPIs
- Total Loan Applications  
- Month-to-Date (MTD) Loan Applications  
- Total Funded Amount  
- Total Amount Received  
- Average Interest Rate  
- Average Debt-to-Income Ratio (DTI)  

### 📌 Good Loan vs Bad Loan KPIs

**Good Loans (Loan Status: Fully Paid, Current)**
- Good Loan Application Percentage  
- Good Loan Applications  
- Good Loan Funded Amount  
- Good Loan Amount Received  

**Bad Loans (Loan Status: Charged Off)**
- Bad Loan Application Percentage  
- Bad Loan Applications  
- Bad Loan Funded Amount  
- Bad Loan Amount Received  

---

## 🔹 Dashboards Created in Tableau

### 🟦 Dashboard 1: Summary
- KPI cards for key loan metrics  
- Good Loan vs Bad Loan comparison  
- Loan Status grid view  

### 🟦 Dashboard 2: Overview
- Monthly Trends by Issue Date (Line Chart)  
- Regional Analysis by State (Map)  
- Loan Term Analysis (Donut Chart)  
- Employment Length Analysis (Bar Chart)  
- Loan Purpose Breakdown (Bar Chart)  
- Home Ownership Analysis (Tree Map)  

### 🟦 Dashboard 3: Details
- Detailed loan-level data  
- Interactive filters for deep analysis  

---

## 🔹 SQL Queries (Used as Tableau Data Source)

```sql
-- Total Loan Applications
SELECT COUNT(id) AS Total_Applications
FROM bank_loan_data;

-- Total Funded Amount
SELECT SUM(loan_amount) AS Total_Funded_Amount
FROM bank_loan_data;

-- Total Amount Received
SELECT SUM(total_payment) AS Total_Amount_Received
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
