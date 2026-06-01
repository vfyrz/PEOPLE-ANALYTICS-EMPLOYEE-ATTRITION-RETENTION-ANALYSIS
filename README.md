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
