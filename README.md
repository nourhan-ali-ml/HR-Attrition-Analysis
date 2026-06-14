# 📊 HR Attrition Analysis Dashboard
### Business Intelligence Case Study | GBS BI Hub

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Excel](https://img.shields.io/badge/Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)

---

## 🎯 Project Overview

End-to-end HR attrition analysis project built to identify key drivers of employee turnover and provide actionable retention strategies. The analysis covers **1,470 employees** across multiple departments and job roles.

**Live Dashboard:** [View Here](https://nourhan-hr-attrition-analysis-dashboard.netlify.app/)

---

## 📸 Dashboard Preview

> *(Add Power BI screenshots here)*

**Page 1 — Executive Overview**
![Page 1](screenshots/page1.png)

**Page 2 — Key Drivers**
![Page 2](screenshots/page2.png)

**Page 3 — Outliers & High Risk**
![Page 3](screenshots/page3.png)

---

## 🔍 Key Findings

| Metric | Value |
|--------|-------|
| Overall Attrition Rate | **16.12%** (above industry avg ~13%) |
| Total Employees Analyzed | **1,470** |
| Total Attrited | **237 employees** |
| Highest Risk Role | **Sales Representative (39.8%)** |
| Overtime Risk Multiplier | **3× (30.5% vs 10.4%)** |
| Income Gap | **$2,046/month** (attrited vs active) |
| High-Risk Employees | **79 employees (48.1% attrition rate)** |

---

## ⚡ Key Attrition Drivers

1. 🔴 **Overtime** — Employees working OT leave at 30.5% vs 10.4% without OT
2. 🔴 **Compensation Gap** — Attrited employees earned $2,046 less per month
3. 🟡 **Junior Tenure** — Employees with <5 years leave at 32.9% vs 10.7% seniors
4. 🟡 **Stock Options** — No equity = 24.4% attrition vs 9.4% with Level 1 options
5. 🟡 **Low Satisfaction** — Score 1 = 22.8% attrition vs 11.3% at score 4

---

## 🛠️ Technical Implementation

### Data Model — Star Schema
```
FACT_Employee (central table)
├── DIM_Department
├── DIM_JobRole
├── DIM_Employee_Profile
└── DIM_Satisfaction
```

### DAX Measures (10 measures)
- Attrition Rate %
- Total Attrition
- Avg Monthly Income
- Income Gap (Attrited vs Active)
- High Risk Count
- Overtime Attrition Rate
- Entry Level Attrition %
- Avg Tenure Attrited
- No Stock Option Attrition %
- Avg Income Active / Attrited

### SQL Query
```sql
SELECT
    d.DepartmentName,
    jr.JobRole,
    COUNT(CASE WHEN f.Attrition = 'Yes' THEN 1 END) AS AttritionCount,
    ROUND(AVG(f.MonthlyIncome), 0)                   AS AvgMonthlyIncome
FROM       FACT_Employee   f
INNER JOIN DIM_Department  d   ON f.Department = d.DepartmentName
INNER JOIN DIM_JobRole     jr  ON f.JobRole    = jr.JobRole
GROUP BY d.DepartmentName, jr.JobRole
ORDER BY AttritionCount DESC;
```

### Python — Experience Level Classification
```python
def classify_experience(years):
    if years < 5:   return 'Junior'
    elif years <= 9: return 'Mid'
    else:            return 'Senior'

df['ExperienceLevel'] = df['TotalWorkingYears'].apply(classify_experience)
```

**Results:**
| Experience Level | Employee Count | Attrition Rate |
|-----------------|---------------|----------------|
| Junior (<5 yrs) | 228 | 32.9% |
| Mid (5-9 yrs) | 493 | 16.6% |
| Senior (10+ yrs) | 749 | 10.7% |

---

## 💡 Strategic Recommendations

| # | Initiative | Expected Impact | Timeline |
|---|-----------|----------------|----------|
| 01 | Revise Sales Rep compensation ($2,626 avg) | 39.8% → <20% | 0–3 months |
| 02 | Cap overtime at 10 hrs/week | -50% OT-driven exits | 1–2 months |
| 03 | Early career retention program (<5 yrs) | 32.9% → <18% | 2–4 months |
| 04 | Expand ESOP to Job Level 1 | 2.6× retention improvement | 3–6 months |
| 05 | Deploy predictive attrition monitoring | -30% avoidable exits | Ongoing |

**Projected Outcome: 16.12% → 9.62% attrition** *(40% reduction)*

---

## 📁 Project Structure

```
hr-attrition-analysis/
├── HR_Attrition_BI_Solution_NourhanAli.xlsx  # Star Schema + SQL + Python + DAX
├── HR_Attrition_Presentation_NourhanAli.pptx # Stakeholder presentation (13 slides)
├── screenshots/                               # Dashboard screenshots
└── README.md
```

---

## 👩‍💻 Author

**Nourhan Ali** | Data & BI Analyst
📧 bio.eng.nourhanali@gmail.com
🔗 [LinkedIn](https://linkedin.com/in/nourhanali)
🐱 [GitHub](https://github.com/nourhan-ali-ml)
🌐 [Live Dashboard](https://nourhan-hr-attrition-analysis-dashboard.netlify.app/)
