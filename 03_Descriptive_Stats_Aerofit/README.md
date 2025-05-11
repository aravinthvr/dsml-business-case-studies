# 🏃‍♂️ Aerofit - Descriptive Statistics & Probability

## 📋 Overview

Aerofit is a prominent brand specializing in fitness equipment, offering a range of products including treadmills, exercise bikes, and gym accessories. This case study focuses on analyzing customer data related to treadmill purchases to better understand the target audience and improve product recommendations.

---

## 🎯 Business Objective

The objective is to create customer profiles for each treadmill product (KP281, KP481, KP781) by analyzing the characteristics of the customers who purchased them. Additionally, we explore probabilities and patterns to help the business align its marketing and product strategies effectively.

---

## 📦 Dataset Description

The dataset contains information on individuals who purchased a treadmill over the past three months. It includes the following features:

| Feature        | Description                                           |
|----------------|-------------------------------------------------------|
| `Product`      | Treadmill purchased: KP281, KP481, or KP781          |
| `Age`          | Age of the customer (in years)                        |
| `Gender`       | Gender of the customer                                |
| `Education`    | Years of education                                    |
| `MaritalStatus`| Marital status: Single or Partnered                   |
| `Usage`        | Expected weekly usage (number of times per week)     |
| `Income`       | Annual income (in USD)                                |
| `Fitness`      | Self-rated fitness (1 = Poor, 5 = Excellent)          |
| `Miles`        | Expected weekly distance (in miles)                   |

---

## 🧪 Analysis Steps

### ✅ Initial Data Exploration
- Dataset structure and shape
- Data types and basic statistical summary
- Missing values and outlier detection (boxplots, mean vs. median check)

### 📊 Univariate & Bivariate Visualizations
- Count plots, histograms, and boxplots for product-wise distributions
- Comparisons across gender, marital status, and income levels
- Correlation matrix and heatmaps for numerical features

### 🔢 Probability Analysis
- Marginal probabilities: % of customers purchasing each product
- Conditional probabilities: e.g., likelihood of a male customer buying KP781
- Contingency tables to observe associations between variables

### 👥 Customer Profiling
- Grouping customers based on usage, income, and fitness levels
- Treadmill product preference by demographic segments

---

## 💡 Key Insights

### Product Popularity:
- **KP281 (Entry-Level)**: Most popular treadmill, chosen by 44.4% of users.
- **KP481 (Mid-Range)**: Preferred by 33.3% of users.
- **KP781 (High-End)**: Chosen by 22.2% of users.

### Customer Demographics & Preferences:
- **Gender**: Males (57.7%) use treadmills more than females (42.2%). KP781 is significantly more popular among males (82% of its users are male).
- **Marital Status**: Partnered individuals (59.4%) use treadmills more than single individuals (40.6%).
- **Age Group**: Adults aged 34-44 years (50.3%) are the primary users, followed by young adults aged 18-24 (29.6%).
- **Education**: Undergraduates (50.8%) are the largest user group. Postgraduates show a strong preference for KP781 (85.2% of PG users).
- **Income**: Low-income individuals (46.1%) form the largest user base. High-income individuals exclusively prefer KP781.

### Usage Patterns:
- **Usage Frequency**: Most users (38.3%) use the treadmill 3 times a week.
- **Fitness Level**: Users rating themselves 3 out of 5 in fitness (53.9%) are the most common.
- **Miles**: Most users (60.3%) fall into the 'Regular' miles group (60–120 miles/week). Intensive users (240–360 miles/week) exclusively use KP781.

### Correlations:
- **Income** shows a positive correlation with **Age**, **Miles**, and **Education**.

### Outliers:
- **10%** of users are outliers in the **Income** field, mostly preferring KP781.
- **7.2%** of users are outliers in the **Miles** field, indicating intensive treadmill use.

---

## ✅ Recommendations

- **Targeted Marketing for KP481**: Encourage KP281 users to upgrade to KP481 with offers, especially those in the low to medium income brackets.
- **Boost KP781 Sales Among Females**: Develop strategies or marketing campaigns to increase KP781 adoption among female customers.
- **Address Low KP781 Usage by Infrequent Users**: Investigate why users with 2–3 weekly sessions avoid KP781, and design offers or messaging to appeal to them.
- **Engage Low Fitness Users**: Promote beginner-friendly content or fitness plans for users who rate their fitness as 1 or 2 to increase adoption.
- **Attract Older Demographics**: Survey older users to understand their reluctance and modify product design or messaging to improve adoption.
- **Promote KP281/KP481 to Postgraduates**: Most PGs go for KP781. Consider highlighting affordability or compactness of KP281/KP481 if they have different needs.
- **Feedback from Intensive Users**: Gather insights from high-mileage users to improve KP781’s features and services.
- **Tiered Upgrade Strategy**:
  - Encourage low-income KP281 users to upgrade to KP481.
  - Motivate medium-income KP481 users to move up to KP781 using financing or premium feature bundling.

---

## 📌 Final Notes

All analysis and business insights are available in the notebook.

> For detailed charts, data wrangling, and interpretation, please refer to the full [Jupyter Notebook](./Aerofit_Stats_Probability.ipynb).

