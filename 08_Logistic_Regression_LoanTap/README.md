# 🎓 LoanTap - Personal Loan Underwriting (Logistic Regression Case Study)

## 🧠 Mindset & Approach

LoanTap, an online platform for customized loans, is building a machine learning-driven underwriting model to assess the creditworthiness of individuals applying for personal loans. The goal of this case study is to develop a model that predicts the likelihood of a loan being fully repaid versus charged off, based on various borrower attributes, to inform credit extension decisions.

### Project Goals:
- Analyze the relationship between borrower attributes and loan repayment status (`loan_status`).
- Build a **Logistic Regression model** to predict `loan_status` (1 for Fully Paid, 0 for Charged Off).
- Evaluate model performance using metrics such as **Accuracy**, **ROC AUC**, **Precision**, **Recall**, and **F1-Score**.
- Provide actionable insights for improving LoanTap's underwriting process and risk assessment.

---

## 📁 Dataset Overview

**Dataset Name:** `logistic_regression.csv` (referred to as `df` in the notebook)  
**Source:** Provided by LoanTap (via Google Drive link in the notebook)  
[Dataset Link](https://drive.usercontent.google.com/u/0/uc?id=1ZPYj7CZCfxntE8p2Lze_4QO4MyEOy6_d&export=download)

### 🎯 Column Descriptions:

| Column Name                    | Description                                                       |
|---------------------------------|-------------------------------------------------------------------|
| loan_amnt                       | The listed amount of the loan applied for by the borrower.        |
| term                            | The number of payments on the loan (months, 36 or 60).            |
| int_rate                        | Interest Rate on the loan.                                        |
| installment                     | The monthly payment owed by the borrower if the loan originates.  |
| grade                           | LoanTap assigned loan grade.                                      |
| sub_grade                       | LoanTap assigned loan subgrade.                                   |
| emp_title                       | The job title supplied by the Borrower (dropped due to high cardinality). |
| emp_length                      | Employment length in years (0-10).                                |
| home_ownership                  | The home ownership status provided by the borrower.               |
| annual_inc                      | The self-reported annual income provided by the borrower.         |
| verification_status             | Indicates if income was verified by LoanTap.                      |
| issue_d                         | The month which the loan was funded (converted to year/month).    |
| loan_status                     | Current status of the loan (Target Variable: 1 for Fully Paid, 0 for Charged Off). |
| purpose                         | A category provided by the borrower for the loan request.         |
| title                           | The loan title provided by the borrower (dropped as similar to purpose but higher cardinality). |
| dti                             | Debt-to-income ratio.                                             |
| earliest_cr_line                | The month the borrower's earliest reported credit line was opened (converted to year/month). |
| open_acc                        | The number of open credit lines in the borrower's credit file.    |
| pub_rec                         | Number of derogatory public records (converted to a flag).        |
| revol_bal                       | Total credit revolving balance.                                   |
| revol_util                      | Revolving line utilization rate.                                  |
| total_acc                       | The total number of credit lines currently in the borrower's credit file. |
| initial_list_status             | The initial listing status of the loan (W, F).                    |
| application_type                | Indicates whether the loan is an individual or joint application. |
| mort_acc                        | Number of mortgage accounts (converted to a flag).                |
| pub_rec_bankruptcies            | Number of public record bankruptcies (converted to a flag).       |
| address                         | Address of the individual (used to extract zip_code, then dropped). |
| **Derived Features**            |                                                                   |
| pub_rec_bankruptcies_flag       | Flag: 1 if pub_rec_bankruptcies > 0, else 0.                      |
| pub_rec_flag                    | Flag: 1 if pub_rec > 0, else 0.                                   |
| mort_acc_flag                   | Flag: 1 if mort_acc > 0, else 0.                                  |
| issue_d_year, issue_d_month     | Year and month loan was funded.                                   |
| earliest_cr_line_year, earliest_cr_line_month | Year and month of earliest credit line.           |
| zip_code                        | Extracted from address (target encoded).                          |

---

## 🔍 Problem Statement

LoanTap aims to deploy an underwriting model to determine if a credit line should be extended to an individual applying for a Personal Loan. This involves assessing the risk of default. This case study focuses on:
- Developing a logistic regression model to predict `loan_status` (whether a loan will be 'Fully Paid' or 'Charged Off').
- Evaluating the model’s performance with a focus on metrics like ROC AUC, Precision, and Recall to balance identifying good borrowers and flagging potential defaulters.
- Providing data-driven insights and recommendations to optimize LoanTap’s loan approval process and manage credit risk.

---

## ✅ Steps Followed

### 1. 🔎 Exploratory Data Analysis (EDA)
- **Data Loading & Initial Inspection**: Loaded the dataset, examined its shape, data types, and initial missing value percentages.
- **Data Cleaning**:
    - Dropped high cardinality/redundant features: `emp_title`, `title`.
    - Extracted `zip_code` from `address` and then dropped `address`.
    - Cleaned `term` (removed " months") and `emp_length` (converted to numerical years).
- **Feature Engineering (Initial)**:
    - Created binary flag columns: `pub_rec_bankruptcies_flag`, `pub_rec_flag`, `mort_acc_flag` based on their original count values, then dropped the original count columns.
    - Extracted `year` and `month` components from `issue_d` and `earliest_cr_line`, then dropped the original date columns.
- **Type Conversion**: Converted columns to appropriate data types (category, int, float) to reduce memory usage and for proper analysis.
- **Missing Value Handling**:
    - Dropped rows with missing values in `pub_rec_bankruptcies_flag` and `revol_util` (small percentage of total).
    - Imputed missing `emp_length` and `mort_acc_flag` with their respective modes.
- **Univariate Analysis**: Examined distributions of categorical features (pie charts, count plots) and numerical features (box plots, histograms with KDE).
- **Bivariate & Multivariate Analysis**: Analyzed relationships between features and the target variable (`loan_status`) using count plots (with hue) and box plots. Investigated correlations between numerical features using pair plots and a heatmap.

### 2. 🧹 Data Preprocessing
- **Outlier Treatment**:
    - Identified that a significant portion of data could be considered outliers if using IQR.
    - Applied `np.log1p` transformation to numerical features to handle skewness.
    - Clipped `revol_util` and `dti` to plausible ranges (0-100, though log-transformed values were used).
    - Capped all numerical features at their 25th and 95th percentiles after transformation to mitigate extreme value effects.
- **Encoding Categorical Features**:
    - **Label Encoding**: Applied to ordinal/binary categorical columns (`term`, `initial_list_status`, `verification_status`, `application_type`, `grade`, `emp_length`, `sub_grade`).
    - **One-Hot Encoding**: Applied to nominal categorical columns with few unique values (`home_ownership`, `purpose`).
    - **Target Encoding**: Applied to `zip_code` (a high-cardinality categorical feature) using the mean of `loan_status` from the training set to prevent data leakage.
- **Data Splitting**: Divided the data into training, validation, and test sets (80-20 split for train-test, then 80-20 split of train for train-validation).
- **Feature Scaling**: Used `StandardScaler` to standardize the features before feeding them into the logistic regression model.

### 3. 📈 Model Building
- **Baseline Model**: Built an initial Logistic Regression model using `sklearn`.
- **Hyperparameter Tuning**: Tuned the `C` parameter (inverse of regularization strength) for L2 regularization using a range of values and evaluated performance on the validation set to find the optimal `C`.
- **Feature Selection**: Employed L1 regularization (Lasso) to identify features with non-zero coefficients, effectively performing feature selection.
- **Final Model**: Trained a Logistic Regression model with the best `C` value (L2 penalty) using the subset of features identified by L1 regularization.

### 4. 🧪 Model Evaluation
- **Performance Metrics**: Evaluated the final model on the test set using:
    - Accuracy.
    - Confusion Matrix: To understand True Positives, True Negatives, False Positives, and False Negatives.
    - Classification Report: Providing Precision, Recall, and F1-Score for both 'Fully Paid' (1) and 'Charged Off' (0) classes.
    - ROC AUC Score: To assess the model's ability to discriminate between the two classes.
    - Precision-Recall Curve and PR AUC Score: To analyze the trade-off, especially important for imbalanced classes.
- **Threshold Optimization**: Discussed the importance of selecting an optimal probability threshold based on business objectives (e.g., minimizing NPAs vs. maximizing loan approvals). The best threshold based on maximizing precision*recall on the PR curve was identified around 0.3998.

### 5. 📝 Insights & Recommendations Summary
- The model demonstrated good predictive capability in distinguishing between loans likely to be 'Fully Paid' versus 'Charged Off'.
- Key financial indicators (DTI, income, credit utilization) and loan characteristics (grade, interest rate) were significant.
- The choice of probability threshold is critical for balancing risk and business growth.

---

## 💡 Final Insights

- **Model Performance**: The final Logistic Regression model achieved a test accuracy of approximately **88.7%** and an **ROC AUC score of around 0.88**, indicating strong discriminative power.
- **Key Default Predictors**: Features like higher `int_rate`, lower `grade` and `sub_grade` (indicating higher risk), higher `dti`, higher `revol_util`, shorter `emp_length`, and specific `purpose` categories were associated with a higher likelihood of a loan being 'Charged Off'. Conversely, factors like higher `annual_inc`, `verification_status` (Verified), and longer `issue_d_year` (more recent loans, potentially reflecting better recent underwriting or economic conditions) tended to correlate with 'Fully Paid' status.
- **Impact of Credit History**: The presence of derogatory public records (`pub_rec_flag`) and having mortgage accounts (`mort_acc_flag`) were also important indicators.
- **Geographical Influence**: `zip_code`, after target encoding, showed relevance, suggesting that geographical factors can play a role in loan repayment behavior.
- **Correlation**: A very high positive correlation was observed between `loan_amnt` and `installment`.
- **Home Ownership**: The majority of applicants had `MORTGAGE` as their home ownership status.
- **Trade-offs**: The model evaluation highlighted the trade-off between Precision and Recall. For LoanTap, minimizing NPAs (correctly identifying 'Charged Off' loans - Class 0 Recall) is crucial, but this must be balanced against rejecting too many creditworthy applicants (Class 1 Precision).

---

## 🎯 Recommendations for LoanTap (Underwriting & Risk)

1.  **Implement Model-Driven Underwriting**: Utilize the logistic regression model's predicted probabilities to score applicants. A threshold (e.g., around 0.40, but tunable) can be set to segment applicants into approve/reject/manual review categories.
2.  **Focus on High-Impact Features**: During manual review or for refining automated rules, pay close attention to:
    *   **Debt-to-Income Ratio (DTI)**: Higher DTI often indicates higher risk.
    *   **Revolving Utilization (revol_util)**: High utilization can be a sign of financial distress.
    *   **Loan Grade/Subgrade & Interest Rate**: These are inherently risk indicators.
    *   **Annual Income & Verification Status**: Ensure income is sufficient and verified.
    *   **Employment Length**: Longer employment can indicate stability.
3.  **Dynamic Threshold Adjustment**: Based on business strategy (e.g., growth phase vs. risk-aversion phase), adjust the prediction threshold.
    *   To **minimize NPAs (prioritize catching defaulters)**: Consider a slightly lower threshold to be more sensitive to 'Charged Off' predictions (increases Recall for class 0).
    *   To **reduce lost opportunities (approve more good loans)**: Consider a slightly higher threshold (increases Precision for class 0, meaning fewer false alarms for defaulters).
4.  **Segmented Strategies**: Develop different underwriting strategies or loan terms for applicants based on their risk scores and profiles derived from the model.
5.  **Monitor `zip_code` Insights**: While target encoded, the `zip_code` feature's importance suggests monitoring regional default patterns and potentially adjusting strategies for specific areas if consistent trends emerge.

---

## 🏢 Recommendations for LoanTap's Business Model

-   **Refine Risk-Based Pricing**: Use the model's risk assessment to offer more tailored interest rates and loan terms. Higher-risk applicants (if approved) might receive higher rates or lower loan amounts.
-   **Enhance Data Collection & Feature Engineering**:
    *   For features like `emp_title` (dropped due to cardinality), explore creating broader job categories or using NLP if detailed job information is valuable.
    *   Continuously look for new predictive features that could improve model performance.
-   **Customer Feedback Loop**: For borderline cases or rejected applications, if feasible, gather feedback to understand reasons and potentially refine the model or customer communication.
-   **Regular Model Monitoring & Retraining**: Periodically retrain the model with new data to ensure it remains accurate and adapts to evolving economic conditions and borrower behaviors. Track key metrics like default rates across different segments.

---

## 📌 Final Notes

For a deeper dive into the data analysis, feature engineering, model building, and detailed evaluation, please refer to the full [Jupyter Notebook](./Loantap_Logistic_Regression.ipynb).