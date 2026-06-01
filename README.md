# Employee Retention Analysis Using SQL BigQuery

## 📌 Project Overview
This project focuses on analyzing employee attrition and turnover factors using the **IBM HR Analytics Employee Attrition & Performance** dataset from Kaggle. By leveraging **Google BigQuery**, this analysis aims to uncover key data-driven insights regarding why employees leave the organization, specifically focusing on departmental trends, financial factors, workload, and job satisfaction.

The ultimate goal of this project is to provide actionable insights for the Human Resources (HR) department to improve employee retention strategies and mitigate turnover costs.

---

## 🛠️ Tech Stack & Tools
* **Database Platform:** Google BigQuery (SQL Workspace)
* **Language:** Standard SQL
* **Dataset Source:** IBM HR Analytics (Kaggle)

---

## 📊 Key Analytical Queries & Insights

### 1. Attrition Analysis by Department
* **Objective:** Determine which department experiences the highest turnover rate to help HR prioritize engagement initiatives.
* **Query:**
```sql
SELECT 
  Department,
  -- Directly calculate the average of the attrition numeric column, multiply by 100, and round it
  ROUND(AVG(Attrition_Numeric) * 100, 0) AS Avg_of_Attrition
FROM Kaggle.HR_Retention
GROUP BY Department
-- Keep sorting from smallest to largest so the chart trends upward
ORDER BY Avg_of_Attrition ASC;
```

* **Insight:**  The Sales department exhibits the highest attrition rate at 21%, followed by Human Resources (19%) and Research & Development (14%).

### 2. Work-Life Balance Analysis: Impact of Overtime on Attrition
* **Objective:** Examine how working overtime correlates with an employee's likelihood to leave the company
* **Query:**
```sql
SELECT 
  Overtime,
  ROUND(AVG(Attrition_Numeric) * 100, 0) AS Avg_of_Attrition
FROM Kaggle.HR_Retention
GROUP BY Overtime
ORDER BY Avg_of_Attrition ASC;
```

* **Insight:**  There is a massive spike in turnover among employees who work overtime. Employees who work overtime (Overtime = Yes) have an attrition rate of 31%, which is three times higher than those who do not work overtime (10%). This highlights that heavy workloads and poor work-life balance are critical drivers of employee resignation.

### 3. Financial Analysis: Relationship Between Monthly Income and Attrition
* **Objective:** Explore how compensation and monthly income impact an employee's decision to leave the company.
* **Query:**
```sql
SELECT 
  Attrition,
  ROUND(AVG(Monthly_Income), 0) AS Avg_of_Monthly_Income
FROM Kaggle.HR_Retention
GROUP BY Attrition
ORDER BY Avg_of_Monthly_Income ASC;
```

* **Insight:**  There is a clear financial gap between employees who stay and those who leave. Employees who left the company (Attrition = Yes) earned an average monthly income of $4,787, which is approximately 30% lower ($2,046 less) than the average income of employees who stayed ($6,833). This strongly confirms that lower compensation is a major driver of employee turnover.

### 4. Sentiment Analysis: Correlation Between Job Satisfaction and Attrition
* **Objective:** To evaluate how an employee's subjective job satisfaction rating impacts their likelihood of leaving the organization and to identify critical thresholds for HR intervention.
* **Query:**
```sql
SELECT
  JOB_SATISFACTION,
ROUND(AVG(Attrition_Numeric)* 100,0) AS Avg_of_Attrition
FROM Kaggle.HR_Retention
GROUP BY JOB_SATISFACTION
ORDER BY Avg_of_Attrition DESC;
```

* **Insight:**  There is a clear downward trend showing that higher job satisfaction leads to better employee retention. Employees with the lowest satisfaction level (Job Satisfaction = 1) exhibit the highest attrition rate at 23%. As satisfaction increases to medium (2) and high (3), attrition stabilizes around 16% - 17%. The turnover rate drops significantly to its lowest point of 11% when employees report the highest level of satisfaction.

---
## 💡 HR Recommendations based on Data
 **1)** To evaluate how an employee's subjective job satisfaction rating impacts their likelihood of leaving the organization and to identify critical thresholds for HR intervention.
Sales Department Intervention: Since the Sales department has a critical attrition rate of 21%, HR should conduct targeted stay-interviews and review the commission/incentive structures for sales representatives.

 **2)** Compensation Benchmark: Standardize compensation ranges for roles showing a high correlation between lower monthly income and a True attrition status to remain competitive in the market.

 **3)** Workload and Retention Balance: HR needs to audit departments with excessive overtime hours. Implementing better workload distribution or hiring temporary staff could be cheaper than losing 31% of over-worked employees.

**4)** Proactive Pulse Surveys: Regularly track job satisfaction levels. Since employees with a rating of 1 have a 23% chance of leaving, HR can proactively intervene before they submit their resignation.
