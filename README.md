# PEOPLE-ANALYTICS-EMPLOYEE-ATTRITION-RETENTION-ANALYSIS
Data-driven People Analytics project using SQL to explore employee turnover patterns, analyze departmental attrition rates, and provide actionable recommendations for HR retention.

## 🛠️ Tech Stack & Tools
* **Database Platform:** Google BigQuery
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
  -- Directly calculate the average of the Attrition numeric column, multiply by 100, and round it
  ROUND(AVG(Attrition_Numeric) * 100, 0) AS Avg_of_Attrition
FROM Kaggle.HR_Retention
GROUP BY Department
-- Keep sorting from smallest to largest so the chart trends upward
ORDER BY Avg_of_Attrition ASC;

* **Insight:** The Sales department exhibits the highest attrition rate at 21%, followed by Human Resources (19%) and Research & Development (14%).

---

### 2. Attrition Analysis by Overtime
* **Objective:**Examine how working overtime correlates with an employee's likelihood to leave the company.
* **Query:**
```sql
SELECT 
 Overtime,
-- Directly calculate the average of the Attrition numeric column, multiply by 100, and round it
ROUND(AVG(ATTRITION_NUMERIC)* 100, 0) AS Avg_of_Attrition
FROM Kaggle.HR_Retention
GROUP BY Overtime
-- Keep sorting from smallest to largest so the chart trends upward
ORDER BY Avg_of_Attrition ASC;

* **Insight:**  There is a massive spike in turnover among employees who work overtime. Employees who work overtime (`Overtime = Yes`) have an attrition rate of **31%**, which is **three times higher** than those who do not work overtime (**10%**). This highlights that heavy workloads and poor work-life balance are critical drivers of employee resignation.

---

### 3. Financial Analysis: Relationship of Monthly Income and Attrition
* **Objective:**Explore how compensation impacts an employee's decision to leave the company.
* **Query:**
```sql
SELECT 
  Attrition,
  -- Directly calculate the average of the Monthly_Income column, and round it
ROUND(AVG(MONTHLY_INCOME), 0) AS Avg_of_Monthly_Income
FROM Kaggle.HR_Retention
GROUP BY Attrition
-- Keep sorting from smallest to largest so the chart trends upward
ORDER BY Avg_of_Monthly_Income ASC;

* **Insight:**  There is a clear financial gap between employees who stay and those who leave. Employees who left the company (`Attrition = Yes`) earned an average monthly income of **$4,787**, which is approximately **30% lower** ($2,046 less) than the average income of employees who stayed (**$6,833**). This strongly confirms that lower compensation is a major driver of employee turnover.

---

### 4. Financial Analysis: Relationship of Monthly Income and Attrition
* **Objective:** To evaluate how an employee's subjective job satisfaction rating impacts their likelihood of leaving the organization and to identify critical thresholds for HR intervention.
* **Query:**
```sql
SELECT 
  Job_Satisfaction,
 -- Directly calculate the average of the Attrition numeric column, and round it
ROUND(AVG(Attrition_Numeric)* 100,0) AS Avg_of_Attrition
FROM Kaggle.HR_Retention
GROUP BY Job_Satisfaction
-- Keep sorting from smallest to largest so the chart trends upward
ORDER BY Avg_of_Attrition ASC;

* **Insight:**  There is a clear downward trend showing that higher job satisfaction leads to better employee retention. Employees with the lowest satisfaction level (`Job Satisfaction = 1`) exhibit the highest attrition rate at **23%**. As satisfaction increases to medium (2) and high (3), attrition stabilizes around **16% - 17%**. The turnover rate drops significantly to its lowest point of **11%** when employees report the highest level of satisfaction (`Job Satisfaction = 4`).
