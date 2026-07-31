# Employee Attrition & Churn Prediction Model

## Project Overview
Identifying flight-risk employees is critical for organizational stability, as finding, interviewing, and hiring new staff is both time-consuming and expensive. The objective of this project is to analyze internal HR data to uncover the primary drivers of employee turnover and deploy a predictive model that identifies high-risk employees before they leave.

## Data Dictionary
The dataset consists of 15,000 employee records across 10 variables:

| Variable | Description |
| :--- | :--- |
| `satisfaction_level` | Employee-reported job satisfaction level [0–1] |
| `last_evaluation` | Score of employee's last performance review [0–1] |
| `number_project` | Number of projects employee contributes to |
| `average_monthly_hours` | Average number of hours employee worked per month |
| `tenure` | How long the employee has been with the company (years) |
| `work_accident` | Whether or not the employee experienced an accident while at work |
| `left` | Whether or not the employee left the company (Target variable) |
| `promotion_last_5years` | Whether or not the employee was promoted in the last 5 years |
| `department` | The employee's department |
| `salary` | The employee's salary level (low, medium, high) |

## Exploratory Data Analysis & Cleaning Insights
* **Data Cleaning:** Standardized column names to `snake_case` and dropped 3,008 duplicate rows to prevent the predictive model from overfitting to duplicated observations.
* **Key Observations:** 
  * There is a strong negative relationship between job satisfaction and turnover, presenting a bimodal distribution among those who left (highly dissatisfied vs. highly satisfied employees).
  * Employees at the extreme ends of workload—severely underutilized staff (2 projects) and severely overworked staff (6–7 projects, high hours)—exhibit massive turnover spikes due to burnout or disengagement.
  * Turnover heavily peaks around the 4-year and 5-year tenure marks.

## Modeling Strategy & Methodology
* **Feature Selection:** Utilized all available features to capture a holistic view of the employee workplace experience.
* **Algorithm Selection:** A **Random Forest Classifier** was chosen because employee churn occurs across non-linear extremes (e.g., under-worked vs. overworked), and tree-based models handle these complexities without strict linear assumptions.
* **Optimization:** Hyperparameter tuning was performed using `GridSearchCV` (`max_depth`, `min_samples_leaf`, `n_estimators`) to achieve optimal model depth and prevent overfitting.
* **Evaluation Rationale:** The evaluation prioritized **Recall** and the **F1-Score**, as failing to catch an at-risk employee (False Negative) is significantly more costly to retention than a False Positive.

## Executive Summary & Strategic Recommendations

### Model Performance
* **Metrics:** The tuned Random Forest model achieved **~98% Accuracy** and a **~95% F1-score**, maintaining an extremely low rate of False Negatives.
* **Top Predictors:** Feature importance analysis confirmed that `satisfaction_level` is the primary driver of churn, followed closely by `tenure`, `number_project`, and `average_monthly_hours`.

### Conclusion
Employee turnover is driven by two distinct mechanisms: burnout among high-performers managing excessive hours and project loads, and dissatisfaction among underutilized employees.

### Actionable Recommendations
1. **Workload Management:** HR should actively monitor and cap simultaneous project loads at a maximum of 5 to prevent high-performer burnout.
2. **Review Promotion & Compensation Structures:** High-evaluation employees working long hours leave at disproportionate rates, indicating a need to better align compensation and promotions with output.
3. **Targeted Interventions:** Deploy this predictive model to flag active employees matching historical flight-risk profiles, specifically targeting checkpoints around the 4-year tenure mark.