# 🎓 Jamboree Education - Graduate Admission Prediction (Linear Regression Case Study)

## 🧠 Mindset & Approach

Graduate admissions are influenced by a mix of academic scores, recommendations, and qualitative factors. This case study replicates a real-world business scenario where Jamboree seeks to improve its digital admission prediction tool by identifying key predictors and modeling admission probabilities.

### Project Goals:
- Analyze relationships between admission-related variables.
- Predict a student’s **Chance of Admit** using Linear Regression.
- Validate regression assumptions and evaluate model robustness.
- Derive actionable insights for both students and Jamboree.

---

## 📁 Dataset Overview

**Dataset Name:** `Jamboree_Admission.csv`  
**Source:** Provided by Jamboree Education  
[Dataset Link](https://d2beiqkhq929f0.cloudfront.net/public_assets/assets/000/001/839/original/Jamboree_Admission.csv)

### 🎯 Column Descriptions:

| Column Name                          | Description                                                       |
|-------------------------------------|-------------------------------------------------------------------|
| Serial No.                          | Unique row identifier (dropped during preprocessing)              |
| GRE Score (out of 340)              | Graduate Record Examination score                                 |
| TOEFL Score (out of 120)            | Test of English as a Foreign Language score                       |
| University Rating (1 to 5)          | Rating of the university applied to                               |
| SOP (1 to 5)                        | Statement of Purpose strength                                     |
| LOR (1 to 5)                        | Letter of Recommendation strength                                 |
| Undergraduate GPA (CGPA out of 10) | Academic performance during undergraduate studies                 |
| Research (0 or 1)                   | Whether the applicant has prior research experience               |
| Chance of Admit (0.0 to 1.0)        | Target variable indicating the predicted admission probability    |

---

## 🔍 Problem Statement

Jamboree recently launched an online feature to estimate a student’s probability of admission into Ivy League schools. This case study aims to:
- Identify which factors most significantly impact graduate admissions.
- Build a linear regression model to predict **Chance of Admit**.
- Test model assumptions to ensure reliability.
- Provide data-driven recommendations for students and Jamboree.

---

## ✅ Steps Followed

### 1. 🔎 Exploratory Data Analysis (EDA)
- Dropped the `Serial No.` column as it’s just an identifier.
- Verified no missing or duplicate values.
- Checked distributions using histograms and boxplots.
- Studied feature relationships using scatterplots and a correlation heatmap.
- Converted relevant variables ('University Rating', 'SOP', 'LOR', 'Research') to categorical types for specific analyses.

### 2. 🧹 Data Preprocessing
- Cleaned inconsistent column names (e.g., removed trailing spaces from 'LOR ' and 'Chance of Admit ').
- Detected outliers in the target variable ('Chance of Admit') using IQR and imputed them with the median value. Other features did not show significant outliers requiring treatment.
- Standardized features using `StandardScaler` for use in `sklearn` models (Linear Regression, Lasso, Ridge, ElasticNet).
- Retained unscaled data for `statsmodels.OLS` assumption testing and VIF calculation.

### 3. 📈 Model Building
- Used `statsmodels.OLS` for detailed statistical inference (p-values, R-squared, assumption checks) and `sklearn.linear_model.LinearRegression` for predictive modeling and comparison with regularized models.
- **Feature Selection**: `SOP` was removed from the final model due to its high p-value in the initial OLS regression and to address multicollinearity (based on VIF analysis and its impact on adjusted R-squared).
- Compared performance with Lasso, Ridge, and ElasticNet regressions to observe effects of regularization.

### 4. 🧪 Regression Assumptions Checked (for the final OLS model after removing 'SOP')
- ✅ **Linearity**: Verified via residual vs fitted plots—no clear pattern observed, suggesting a linear relationship is appropriate.
- ✅ **Multicollinearity**: Variance Inflation Factor (VIF) was used. After removing 'SOP', all remaining features had VIF values below 5, indicating acceptable levels of multicollinearity.
- ✅ **Normality of Residuals**: Assessed using a histogram and a Q-Q plot of residuals. The residuals showed a near-normal distribution, with a slight right skew.
- ✅ **Homoscedasticity**: Residuals plotted against fitted values showed a relatively constant variance across the range of fitted values, satisfying this assumption.
- ✅ **Mean of Residuals**: Implicitly close to zero due to the inclusion of an intercept in the OLS model.

### 5. 📊 Model Performance (Final Model after removing 'SOP')
- **Adjusted R² (sklearn Linear Regression on test set)**: Approximately 0.810.
- **Adjusted R² (statsmodels OLS on training set, after removing 'SOP')**: 0.813.
- Evaluated Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), and R² on training, validation, and test sets for `sklearn` models.
- The model showed consistent performance across different data splits, with no significant signs of overfitting.

---

## 💡 Final Insights

- 🎯 **CGPA is the most influential predictor** for admission chances, demonstrating the highest positive impact.
- 📉 **Statement of Purpose (SOP) had minimal independent predictive impact** in the presence of other variables and was removed from the final model due to a high p-value and its contribution to multicollinearity without significantly improving model fit.
- 🔬 **Research experience has a strong positive effect** on admission probability. Applicants with research experience tend to have a higher chance of admission.
- 📝 **GRE scores, TOEFL scores, and LOR strength** are also important positive contributors to the chance of admission.
- 🏫 **University Rating has a moderate positive influence** but is generally secondary to core academic indicators like CGPA and research experience.

---

## 🎯 Recommendations for Students

1.  **Focus on CGPA**: Consistently strive for strong academic performance throughout your undergraduate studies, as this is the most critical factor.
2.  **Improve GRE & TOEFL Scores**: Aim for high scores on standardized tests to enhance your overall profile.
3.  **Gain Research Experience**: Actively seek opportunities to engage in research projects, internships, or co-author publications.
4.  **Secure Strong LORs**: Request Letters of Recommendation from faculty or professionals who know your work and capabilities well and can provide detailed, positive references.
5.  **Don’t Overemphasize University Rating Alone**: While a higher university rating is beneficial, a strong overall profile (high CGPA, good test scores, research) can significantly improve chances even for highly competitive programs.

---

## 🏢 Recommendations for Jamboree

-   **Update the Admission Probability Tool**: Refine the algorithm to give CGPA and Research Experience higher weight, reflecting their strong predictive power.
-   **Focus Coaching Services**: Tailor GRE/TOEFL preparation and profile-building guidance. Emphasize the importance of CGPA and research, and guide students on crafting SOPs that complement their strengths rather than relying on SOPs to cover significant gaps.
-   **Host Profile-Building Workshops**: Develop workshops that help students identify opportunities for research, academic improvement, and crafting compelling applications.
-   **Train Counselors with Data Insights**: Equip counselors with these data-backed insights to provide more effective and targeted student mentoring.
-   **Collect More Granular Data**: For future model iterations, consider collecting data on variables like the quality/impact of research, specifics of LORs (e.g., recommender's reputation), undergraduate institution tier, or extracurricular achievements.
-   **Build a Student-Facing Interactive Dashboard**: Create a tool that allows students to input their profiles and interactively visualize how changes in various factors (e.g., improving GRE score by X points) might impact their estimated admission chance.

---
## 📌 Final Notes

All analysis and business insights are available in the notebook.

> For detailed charts, data wrangling, and interpretation, please refer to the full [Jupyter Notebook](./Jamboree_Linear_Regression.ipynb).