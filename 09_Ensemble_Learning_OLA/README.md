# 🚕 Ola Driver Churn Prediction - Insights & Recommendations

## 📘 Project Overview

This project applies **ensemble machine learning techniques** to predict **driver attrition** at Ola — a critical business issue that impacts operations, customer experience, and acquisition costs. By analyzing driver demographics, performance, financial metrics, and activity data, the goal is to identify drivers likely to leave the platform and enable **data-driven retention strategies**.

---

## 🔍 Key Insights

### 👤 Driver Profiling

- **Financial Metrics**  
  Total Business Value and Income emerged as the **strongest predictors** of driver retention.

- **Demographics**  
  Age plays a **significant role**, with varying churn patterns across different age groups.

- **Geographic Variations**  
  Certain cities exhibited **substantially higher churn**, indicating localized operational or market issues.

- **Performance Correlation**  
  Drivers with **improving quarterly ratings** were significantly less likely to leave.

- **Activity Level**  
  The **number of active records** (i.e., consistent engagement) strongly predicted retention.

---

## 🧠 Model Performance

The best results were achieved using **XGBoost** with **SMOTE** for class imbalance handling.

| Metric       | Score     |
|--------------|-----------|
| **F1 Score** | 0.9383    |
| **ROC-AUC**  | 0.9628    |
| **Precision**| 0.9333    |
| **Recall**   | 0.9434    |

- **Threshold tuning** further optimized the model for real-world deployment scenarios.
- **SMOTE** significantly improved predictive power by balancing attrition and retention classes.

---

## 📊 Feature Importance

| Feature               | Description |
|------------------------|-------------|
| **Total Business Value** | Key indicator of economic activity and loyalty |
| **Income**               | Stable earnings correlated with retention |
| **Age**                  | Different age segments showed distinct attrition trends |
| **Quarterly Rating**     | Performance ratings linked with long-term engagement |
| **Activity Level**       | Active driver records indicated commitment |

---

## 💼 Business Recommendations

### 1. 🎯 Targeted Retention Programs
- Launch **city-specific initiatives** in high-churn zones
- Introduce **tenure-based incentives** around key attrition risk periods
- Develop **career paths and progression plans** based on performance

### 2. 💰 Income Stabilization
- Provide **minimum income guarantees** during slow business periods
- Offer **consistent earnings structures**
- Create **tenure-linked bonuses** to reward long-term commitment

### 3. 📈 Performance Management
- Identify and address **low-rating drivers** with support and training
- Promote **continuous learning and upskilling**
- Launch **recognition programs** for top-performing drivers

### 4. 🛑 Proactive Churn Prevention
- Deploy the **predictive model** as an **early-warning system**
- Set up **automated intervention protocols** for at-risk drivers
- Use **real-time feedback loops** to capture and act on churn signals

### 5. 🏗 Operational Improvements
- Optimize **driver allocation** to improve total business value
- Solve **city-specific operational frictions**
- Reevaluate **promotion and grade policies** based on churn trends

---

## ⚙️ Technical Approach

- Extensive **feature engineering**:
  - Income growth trends
  - Rating improvements
  - Derived activity/tenure features

- Used **ensemble learning methods**:
  - `Random Forest`
  - `Gradient Boosting`
  - `XGBoost` (best performer)

- Tackled **class imbalance** with **SMOTE**

- Applied **hyperparameter tuning** and **threshold optimization** for deployment-readiness

---

## ✅ Conclusion

This case study shows how advanced machine learning can effectively tackle business-critical problems like **driver attrition**. By combining **predictive modeling**, **feature engineering**, and **actionable insights**, Ola can take strategic steps to improve driver retention, reduce acquisition costs, and enhance operational efficiency.

---

## 📌 Final Notes

For a deeper dive into the data analysis, feature engineering, model building, and detailed evaluation, please refer to the full [Jupyter Notebook](./Ola_Ensemble_Learning.ipynb).