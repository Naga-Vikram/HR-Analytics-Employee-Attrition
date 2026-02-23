# HR Analytics – Employee Attrition Analysis (Python & SQL)

## 🎯 Why I Chose This Project

Employee attrition is one of the most critical challenges faced by organizations today, directly impacting **hiring costs, productivity, and workforce stability**. I chose this project to understand **why employees leave**, how attrition can be **quantified using data**, and how analytics can support **better HR decision-making**.

Rather than limiting the analysis to spreadsheets, I intentionally designed this project using **Python, SQL, and a cloud-hosted PostgreSQL database (Supabase)** to simulate a **real-world analytics workflow**.  
The goal was to move from a *student-style CSV analysis* to a **professional, scalable data pipeline** that reflects how analytics is done in modern organizations.

This project emphasizes:
- 📊 Business-driven problem solving  
- 🧠 Metric accuracy and analytical reasoning  
- 🏗️ Industry-style data architecture  
- 📈 Clear storytelling through insights  

---

## 🔄 Why This Analysis Was Done in Both Excel and Python

I intentionally performed the **same HR attrition analysis using two different approaches — Excel and Python with SQL** — to demonstrate **tool-agnostic analytical thinking** and adaptability across real-world analytics environments.

The **Excel version** of this project focuses on:
- Interactive dashboards
- Business-facing reporting
- KPI stability using DAX and Pivot-based modeling

📊 **Excel Dashboard Project:**  
[HR Analytics – Employee Attrition Dashboard (Excel)](https://github.com/Naga-Vikram/HR-Analytics-Employee-Attrition-Excel)

The **Python & SQL version** of this project focuses on:
- Working with a **cloud-hosted PostgreSQL database (Supabase)**
- Writing **server-side SQL queries** for KPI computation
- Building a **scalable, production-style analytics pipeline**
- Separating data storage, analysis logic, and visualization

By implementing the same business problem in both tools, this project highlights:
- 🧠 Strong analytical fundamentals independent of tools  
- 🔄 Ability to translate business logic across platforms  
- 🏢 Readiness to work in both **reporting-centric** (Excel) and **engineering-driven** (Python/SQL) environments  

Together, these two implementations provide a **complete view of how HR analytics can be executed at different levels of organizational maturity**.

---

## 📘 Project Assets

- **Notebook:** `HR_Analytics_Employee_Attrition.ipynb`  
- **Languages:** Python, SQL  
- **Database:** PostgreSQL (Supabase – cloud hosted)  
- **Analysis Type:** Exploratory & KPI-driven analytics  
- **Audience:** HR Managers, Business Analysts, Data Analysts, Decision Makers  

📘 **Kaggle Notebook:**  
[HR Analytics – Employee Attrition Analysis](https://www.kaggle.com/code/vikky11/hr-analytics)

The notebook is structured to clearly separate **data setup, analysis logic, visualization, and insights**, ensuring readability and professional presentation.

---

## 🛠️ Technology Stack

### Core Technologies
- **Python** – Data analysis and visualization  
- **SQL (PostgreSQL)** – KPI computation and aggregation  
- **Supabase** – Cloud-hosted PostgreSQL database  
- **SQLAlchemy** – Secure database connectivity  
- **Pandas** – Data manipulation and result processing  
- **Matplotlib** – Insight-focused visualizations  

This stack mirrors **real-world analytics environments**, where data resides in databases rather than flat files.

---

## 📂 Dataset

- **Dataset Name:** IBM HR Analytics Employee Attrition & Performance  
- **Records:** 1,470 employees  
- **Source:** [IBM HR Analytics Employee Attrition dataset](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset) kaggle
- **Data Type:** Structured HR data including demographics, job roles, compensation, overtime, tenure, and attrition status  

The dataset closely reflects **enterprise HR systems**, making the analysis directly relevant to industry use cases.

---

## 🔄 Data Pipeline

The project follows a **production-inspired data pipeline**:

1. 📥 Original dataset loaded from CSV  
2. ☁️ Data stored in a **Supabase-hosted PostgreSQL database**  
3. 🔐 Secure database access using environment secrets  
4. 🧮 Analysis performed using **SQL queries executed on the database**  
5. 📊 Query results imported into Python for visualization and interpretation  

This approach avoids CSV-only analysis and demonstrates **scalable analytics thinking**.

---

## 🧩 Analysis Framework

The analysis is structured into logical layers:

### 1. Data Layer
- Data stored in PostgreSQL  
- No artificial filtering or outlier removal  
- Business realism preserved  

### 2. Query Layer (SQL)
- Aggregations performed directly in SQL  
- KPIs calculated using `CASE WHEN`, `GROUP BY`, and aggregate functions  
- Server-side computation ensures accuracy and scalability  

### 3. Analysis Layer (Python)
- Query results processed using Pandas  
- Business questions translated into interpretable outputs  

### 4. Visualization & Insight Layer
- Clean, focused Matplotlib visualizations  
- Insights written immediately after visuals for clarity  

This layered approach ensures **separation of concerns**, similar to professional analytics workflows.

---

## 📊 Key Metrics & Queries

The following key HR KPIs were computed **directly at the database level using SQL**, ensuring accuracy, scalability, and reusability across analytics tools.

---

### 🔹 Attrition Count

```sql
SELECT
    COUNT(*) AS attrition_count
FROM ibm_hr_attrition
WHERE "Attrition" = 'Yes';
```
This query returns the **total number of employees who exited**, helping quantify the scale of attrition.  

### 🔹 Overall Attrition Rate

```sql
SELECT
    ROUND(
        SUM(CASE WHEN "Attrition" = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*),
        2
    ) AS attrition_rate_percent
FROM ibm_hr_attrition;
```
This query calculates the **percentage of employees who left the organization**, serving as the baseline attrition metric.

### 🔹 Overtime vs Attrition Comparison

```sql
SELECT
    "OverTime",
    COUNT(*) AS total_employees,
    SUM(CASE WHEN "Attrition" = 'Yes' THEN 1 ELSE 0 END) AS attrition_count,
    ROUND(
        SUM(CASE WHEN "Attrition" = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*),
        2
    ) AS attrition_rate_percent
FROM ibm_hr_attrition
GROUP BY "OverTime";
```
This query compares attrition rates between employees **working overtime vs not working overtime**, revealing workload-related retention risks.  

### 🔹 Average Monthly Income by Job Role
```sql
SELECT
    "JobRole",
    ROUND(AVG("MonthlyIncome"), 2) AS avg_monthly_income
FROM ibm_hr_attrition
GROUP BY "JobRole"
ORDER BY avg_monthly_income DESC;
```
This query highlights **compensation differences across job roles**, which were later analyzed in relation to attrition patterns.  

Server-side aggregation ensures that these metrics are:
- ✅ Accurate  
- ♻️ Reusable  
- 📈 Suitable for dashboards and BI tools  

---

## 🔍 Key Insights

### 1. Overall Attrition Severity
Approximately **1 in every 6 employees** left the organization, indicating that attrition is a **significant business concern**, not a minor fluctuation.

---

### 2. Overtime as the Strongest Attrition Driver
Employees working overtime showed an attrition rate of **30.53%**, compared to **10.44%** for employees not working overtime.

This indicates that employees working overtime are **nearly three times more likely to leave**, making workload and burnout management a critical retention lever.

---

### 3. Department-Level Risk
- 📌 **Sales** recorded the highest attrition rate  
- 📌 **HR** followed closely  
- 📌 **R&D** showed comparatively lower attrition  

Attrition risk is unevenly distributed, highlighting the need for **targeted retention strategies**.

---

### 4. Job Role & Compensation Impact
Lower-paid roles such as **Sales Representatives** and **Laboratory Technicians** experienced higher attrition, while higher-paid roles showed stronger retention.

This suggests that **compensation alignment and role expectations** play a key role in workforce stability.

---

## 🎨 Visualization Strategy

Visualizations were designed to:
- Highlight comparisons clearly  
- Avoid decorative complexity  
- Support decision-making rather than exploration alone  

Each chart is paired with an insight explaining **what changed, why it matters, and how it can be acted upon**.

---

## 🌟 What Makes This Project Unique

This project stands out because it:

- ☁️ Uses a **cloud-hosted PostgreSQL database** instead of only CSV files  
- 🧮 Computes KPIs using **SQL-first analytics**  
- 🏢 Mimics **enterprise data workflows**  
- 🎯 Emphasizes **business reasoning over tool demonstration**  
- 🧾 Separates setup, analysis, and insights for clarity  

Many HR analytics projects stop at charts — this project focuses on **decision-ready insights**.

---

## ✅ Conclusion

This project demonstrates how **Python and SQL** can be combined to build a **professional HR analytics pipeline** aligned with real organizational practices.

It showcases:
- Business-driven problem framing  
- Scalable, database-backed analysis  
- Strong SQL fundamentals  
- Clear data storytelling  
 


