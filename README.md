# IBM HR Employee Attrition Analysis

## Project Overview

This project analyzes employee attrition using the **IBM HR Analytics Attrition Dataset**. The goal is to understand key factors contributing to employee turnover and to build predictive **logistic regression models** that can identify employees at higher risk of leaving the organization.

The project follows an **end-to-end analytics workflow**, including data exploration, visualization, feature selection, model building, evaluation, and comparison of multiple models.

---

## Dataset

* **Source:** IBM HR Analytics Employee Attrition Dataset (Kaggle)
* **Observations:** 1,470 employees
* **Features:** 35 variables covering demographics, job role, compensation, satisfaction, work-life balance, and tenure
* **Target Variable:** `Attrition` (Yes / No)

Attrition distribution:

* **No:** 84%
* **Yes:** 16%

This highlights a **class imbalance**, which influenced model evaluation (focus on sensitivity, specificity, ROC).

---

## Tools & Technologies

* **Language:** R
* **Libraries:**

  * `tidyverse` (data manipulation & visualization)
  * `ggplot2` (EDA & plots)
  * `caret` (confusion matrix & model evaluation)
  * `pROC` (ROC curves & threshold optimization)

---

## Exploratory Data Analysis (EDA)

Key analyses performed:

* Attrition distribution analysis
* Attrition vs **Education Field**
* Attrition by **Gender & Education Field**
* Income distribution and comparison by attrition status
* Relationship between **OverTime** and **Monthly Income**

### Key EDA Insights

* Attrition varies significantly across **job roles** and **education fields**
* Employees working **overtime** show higher attrition risk
* Lower income bands exhibit a higher concentration of attrition cases

---

## Modeling Approach

Two logistic regression models were developed using different feature subsets.

### Common Steps

1. Data preprocessing and factor handling
2. Conversion of `Attrition` into binary (1 = Yes, 0 = No)
3. 70/30 Train–Validation split
4. Logistic Regression using `glm()`
5. Threshold tuning using ROC & Youden’s Index
6. Model evaluation via confusion matrix

---

## Model 1

**Key Features Included:**

* JobRole
* OverTime
* MonthlyIncome
* TotalWorkingYears
* Age
* DistanceFromHome
* JobLevel
* DailyRate
* YearsAtCompany
* HourlyRate

### Significant Predictors

* OverTime (strongest positive predictor)
* JobRole (Sales Representative, Sales Executive, HR, Lab Technician)
* DistanceFromHome
* DailyRate

### Performance (Threshold = 0.3)

* **Accuracy:** 84.13%
* **Sensitivity:** 45.78%
* **Specificity:** 93.02%
* **Balanced Accuracy:** 69.40%

This model performs well at identifying **non-attrition cases**, with relatively improved sensitivity compared to Model 2.

---

## Model 2

**Key Features Included:**

* BusinessTravel
* StockOptionLevel
* EnvironmentSatisfaction
* JobSatisfaction
* YearsWithCurrManager
* YearsSinceLastPromotion
* EducationField
* Department

### Significant Predictors

* BusinessTravel (Frequent & Rare travel increases attrition)
* StockOptionLevel (protective factor)
* EnvironmentSatisfaction
* JobSatisfaction
* YearsWithCurrManager

### Performance (Threshold = 0.3)

* **Accuracy:** 79.59%
* **Sensitivity:** 22.89%
* **Specificity:** 92.74%
* **Balanced Accuracy:** 57.81%

Model 2 shows lower sensitivity, making it less effective at identifying employees likely to leave.

---

## Model Comparison Summary

| Metric      | Model 1    | Model 2 |
| ----------- | ---------- | ------- |
| Accuracy    | **84.13%** | 79.59%  |
| Sensitivity | **0.46**   | 0.23    |
| Specificity | 0.93       | 0.93    |

**Model 1 outperforms Model 2**, especially in sensitivity, making it more suitable for attrition risk identification.

---

## Key Business Insights

* Overtime is the strongest driver of attrition
* Certain job roles (Sales, HR, Lab Technicians) are at higher risk
* Longer tenure with the same manager reduces attrition
* Satisfaction metrics (job & environment) play a critical role
* Stock options act as a retention mechanism

---

## Conclusion

This project demonstrates how **logistic regression**, combined with strong EDA and threshold optimization, can be used to understand and predict employee attrition. While both models achieve high specificity, **Model 1 provides a better balance between accuracy and sensitivity**, making it more actionable for HR decision-making.

---

## Future Improvements

* Handle class imbalance using SMOTE or weighted loss
* Compare with tree-based models (Random Forest, XGBoost)
* Feature scaling and interaction terms
* Cost-sensitive evaluation (false negatives vs false positives)


