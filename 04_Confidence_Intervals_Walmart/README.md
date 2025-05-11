# 🛍️ Walmart Black Friday Case Study - Customer Spend Analysis

## 📋 Overview

Walmart Inc., one of the world’s largest retail chains, wants to analyze customer purchase behavior, particularly during Black Friday sales. The goal is to evaluate whether there are spending differences based on **gender**, **marital status**, and **age groups**, using statistical analysis and confidence intervals to make data-backed decisions.

---

## 🎯 Business Objective

To understand purchase patterns across different demographics to help Walmart:
- Personalize marketing strategies.
- Optimize inventory based on spending trends.
- Improve customer experience during major sales events.

---

## 📦 Dataset Description

The dataset contains transaction-level data from Walmart's Black Friday sale.

| Feature | Description |
|--------|-------------|
| `User_ID` | Unique customer identifier |
| `Product_ID` | Unique product identifier |
| `Gender` | Male or Female |
| `Age` | Age bin of the customer |
| `Occupation` | Masked occupation code |
| `City_Category` | Type of city (A, B, C) |
| `StayInCurrentCityYears` | Number of years in current city |
| `Marital_Status` | 0 = Unmarried, 1 = Married |
| `ProductCategory` | Masked product category |
| `Purchase` | Amount spent by the customer |

---

## 🧪 Analysis Plan

### 1. Data Preprocessing
- Import dataset and check structure (shape, dtypes, summary statistics).
- Detect and handle missing values.
- Detect outliers using boxplots and summary statistics.
- Convert applicable columns to categorical types.

### 2. Exploratory Data Analysis
- Track total and average purchase amount for:
  - Male vs Female
  - Married vs Unmarried
  - Different Age groups (e.g., 0-17, 18-25, 26-35, 36-50, 51+)
- Visualizations: countplots, histograms, boxplots
- Analyze distribution patterns in purchase amounts

### 3. Statistical Inference
- Use Central Limit Theorem (CLT) to generate sample distributions of purchase amounts.
- Construct **Confidence Intervals (CI)** for mean purchases:
  - Male vs Female
  - Married vs Unmarried
  - Different age bins
- Use different CI widths (90%, 95%, 99%) and observe overlap between groups.

### 4. Answer Business Questions
- Do women spend more per transaction than men?
- Are confidence intervals for male vs female purchase overlapping?
- What are the conclusions for marital status and age?
- How can Walmart leverage these insights?

---

## 💡 Key Insights

- **Gender**:
  - Male customers tend to spend more per transaction than female customers.
  - Confidence intervals show a statistically significant difference with larger sample sizes.

- **Marital Status**:
  - No significant difference in average spend between married and unmarried customers.
  - Their confidence intervals largely overlap.

- **Age Groups**:
  - Customers aged **51+ years** have the highest average spend per transaction.
  - The **26–35 age group** contributes the **most to total sales volume**.
  - Similar spending patterns observed within age clusters:
    - Group 1: 18–25, 26–35, 36–50
    - Group 2: 0–17, 51+

---

## ✅ Recommendations

- 🎯 **Target Male Shoppers**: Develop Black Friday campaigns specifically aimed at male customers who spend more on average.

- 👥 **Focus on Key Age Demographics**:
  - Prioritize 26–35 group for high-volume campaigns.
  - Engage 51+ users with premium offers or loyalty rewards.
  - Create youth-oriented promotions for the 0–17 segment to build future loyalty.

- 🧩 **Segmented Marketing by Age Clusters**:
  - Use behavioral clustering (e.g., 18–50 vs. 0–17/51+) to tailor offers and messaging.

- 💍 **Unified Strategy for Marital Status**:
  - As spending behavior is similar, marital status does not need targeted segmentation.

- 🔁 **Post-Black Friday Engagement**:
  - Use event data to re-target all segments for future promotions and loyalty programs.

---

## 📌 Final Notes

All analysis and business insights are available in the notebook.

> For detailed charts, data wrangling, and interpretation, please refer to the full [Jupyter Notebook](./Walmart_Confidence_CLT.ipynb).

