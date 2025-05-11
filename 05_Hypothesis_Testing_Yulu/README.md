# 🚲 Yulu Bikes - Hypothesis Testing Case Study

## 📋 Business Context

Yulu is India’s leading micro-mobility service provider, offering unique vehicles for the daily commute. Their mission is to eliminate traffic congestion in India by providing a safe, user-friendly, and sustainable commute solution. Yulu zones are strategically placed to make first and last-mile travel smooth, affordable, and convenient.

Recently, Yulu has experienced considerable dips in its revenues. They aim to understand the **factors on which the demand for these shared electric cycles depends**, particularly in the Indian market. This analysis will help in making data-driven decisions to improve their service and revenue.

---

## 🎯 Problem Statement

The company wants to determine:
- Which variables are significant in predicting the demand for shared electric cycles in the Indian market?
- How well do these variables describe the electric cycle demands?

Specifically, this analysis will investigate:
- Does the day being a working day affect the number of rentals?
- Is the number of cycles rented similar or different across various seasons?
- Is the number of cycles rented similar or different in different weather conditions?
- Is there a dependency between weather conditions and the season?

---

## 📁 Dataset Overview

Dataset: `bike_sharing.csv` (loaded from [this URL](https://d2beiqkhq929f0.cloudfront.net/public_assets/assets/000/001/428/original/bike_sharing.csv?1642089089))

| Column     | Description                                             | Data Type (Original/Processed) |
|------------|---------------------------------------------------------|--------------------------------|
| datetime   | Timestamp of data capture (hourly)                      | object / datetime64[ns]        |
| season     | Season (1:Spring, 2:Summer, 3:Fall, 4:Winter)           | int64 / category               |
| holiday    | Whether the day is a holiday or not (0:No, 1:Yes)       | int64 / category               |
| workingday | Whether the day is a working day or not (0:No, 1:Yes)   | int64 / category               |
| weather    | Weather condition (1:Clear, 2:Cloudy, 3:Rainy, 4:Heavy Rain) | int64 / category               |
| temp       | Actual temperature in Celsius                           | float64                        |
| atemp      | "Feels like" temperature in Celsius                     | float64                        |
| humidity   | Relative humidity                                       | int64                          |
| windspeed  | Wind speed                                              | float64                        |
| casual     | Number of non-registered user rentals initiated         | int64                          |
| registered | Number of registered user rentals initiated             | int64                          |
| count      | Total number of rentals (casual + registered)           | int64                          |
| year       | Year extracted from datetime                            | category (New)                 |
| month      | Month extracted from datetime                           | category (New)                 |
| day        | Day of the month extracted from datetime                | category (New)                 |
| hour       | Hour of the day extracted from datetime                 | category (New)                 |

---

## 🔍 Exploratory Data Analysis (EDA)

- ✅ **Data Type Conversion**: `datetime` converted to datetime objects; `season`, `holiday`, `workingday`, `weather` converted to categorical types.
- ✨ **Feature Engineering**: Extracted `year`, `month`, `day`, and `hour` from the `datetime` column.
- 🔄 **Value Mapping**: Numerical representations for `season`, `weather`, `holiday`, and `workingday` were mapped to their descriptive string values (e.g., 1 -> 'Spring').
- 📊 **Descriptive Statistics**: Analyzed mean, median, and skewness for numerical features. `casual`, `registered`, and `count` showed right-skewness.
- 🚫 **Missing Values & Duplicates**: Confirmed no missing values or duplicate rows in the dataset.
- 📈 **Univariate & Bivariate Analysis**:
    - Visualized counts for categorical features (season, weather, holiday, workingday, year, month, hour).
    - Analyzed average rental `count` across different categories using bar plots.
        - Fall season showed the highest rentals.
        - Clear weather had the most rentals.
        - More rentals on working days and in the year 2012.
    - KDE plots showed non-normal distributions for most numerical features, confirmed by Shapiro-Wilk tests.
- 📦 **Outlier Treatment**: Identified outliers in numerical columns using boxplots and imputed them using the IQR method.
- 🔥 **Correlation Analysis**: A heatmap revealed:
    - Strong positive correlation between `temp` and `atemp`.
    - Strong positive correlation of `casual` and `registered` with `count`.
    - `humidity` was negatively correlated with `count`.

---

## 🧪 Hypothesis Testing

Significance Level (α) = 0.05 for all tests.

### 1️⃣ Working Day vs. Number of Electric Cycles Rented

- **Hypothesis**:
    - **H0**: Working Day has no effect on the number of electric cycles rented (mean rentals are equal).
    - **H1**: Working Day has an effect on the number of electric cycles rented (mean rentals are different).
- **Tests Performed**:
    - Shapiro-Wilk Test (Normality): Data for both groups (working day 'Yes'/'No') is not normally distributed.
    - Levene's Test (Homogeneity of Variances): Variances are homogeneous.
    - **Two-Sample T-Test**: p-value > 0.05.
    - **Kruskal-Wallis Test** (Non-parametric alternative): p-value > 0.05.
- **Result**: Failed to reject H0 for both T-Test and Kruskal-Wallis Test.
- ✅ **Conclusion**: Statistically, **Working Day has no significant effect** on the number of electric cycles rented.

### 2️⃣ Season vs. Number of Electric Cycles Rented

- **Hypothesis**:
    - **H0**: Season has no effect on the number of electric cycles rented (mean rentals are equal across seasons).
    - **H1**: Season has an effect on the number of electric cycles rented (mean rentals are different across at least one season).
- **Tests Performed**:
    - Shapiro-Wilk Test (Normality): Data for each season is not normally distributed.
    - Levene's Test (Homogeneity of Variances): Variances are not homogeneous.
    - **One-Way ANOVA**: p-value < 0.05.
    - **Kruskal-Wallis Test** (Non-parametric alternative): p-value < 0.05.
- **Result**: Rejected H0 for both ANOVA and Kruskal-Wallis Test.
- ✅ **Conclusion**: Statistically, **Season has a significant effect** on the number of electric cycles rented.

### 3️⃣ Weather vs. Number of Electric Cycles Rented

- **Hypothesis**:
    - **H0**: Weather has no effect on the number of electric cycles rented (mean rentals are equal across weather conditions).
    - **H1**: Weather has an effect on the number of electric cycles rented (mean rentals are different across at least one weather condition).
- **Tests Performed**:
    - Shapiro-Wilk Test (Normality): Data for each weather condition is not normally distributed (except for 'Heavy Rain' which had insufficient data for a reliable test).
    - Levene's Test (Homogeneity of Variances): Variances are not homogeneous.
    - **One-Way ANOVA**: p-value < 0.05.
    - **Kruskal-Wallis Test** (Non-parametric alternative): p-value < 0.05.
- **Result**: Rejected H0 for both ANOVA and Kruskal-Wallis Test.
- ✅ **Conclusion**: Statistically, **Weather has a significant effect** on the number of electric cycles rented.

### 4️⃣ Dependency between Weather and Season

- **Hypothesis**:
    - **H0**: Weather is independent of Season.
    - **H1**: Weather is dependent on Season.
- **Test Performed**:
    - **Chi-Square Test of Independence**.
- **Result**: p-value < 0.05. Rejected H0.
- ✅ **Conclusion**: Statistically, **Weather is dependent on Season**.

---

## 💡 Key Insights from Hypothesis Testing & EDA

- **Working Day**: Does not significantly impact the total number of bike rentals.
- **Season**: Significantly affects rental demand. EDA shows rentals peak in Fall and Summer, and are lowest in Spring.
- **Weather**: Significantly influences rental demand. EDA shows clear weather has the highest rentals, while adverse conditions (Rainy, Heavy Rain) see fewer rentals.
- **Interdependency**: There's a statistical dependency between weather conditions and the season.
- **User Behavior**:
    - Casual riders tend to be more active on non-working days (weekends/holidays).
    - Registered users show higher activity on working days.
- **Overall Demand Patterns**:
    - Rentals are generally higher in 2012 compared to 2011.
    - Peak rental hours are typically morning (7-9 AM) and evening (5-7 PM).
    - June, July, and August show high monthly rentals.

---

## ✅ Recommendations for Yulu

1.  **Seasonal Marketing & Operations**:
    - Focus marketing campaigns and resource allocation (bike availability) during peak seasons (Fall, Summer).
    - Introduce seasonal offers or subscription plans to capitalize on high-demand periods.

2.  **Weather-Responsive Strategies**:
    - Implement dynamic pricing or promotions based on weather forecasts (e.g., discounts on clear days, special offers during light rain if bikes are equipped).
    - Consider providing weather-related information or tips within the app.

3.  **Targeted User Engagement**:
    - Since working days don't impact overall demand significantly, maintain consistent service levels.
    - Develop strategies to convert casual riders (more active on weekends) into registered users.
    - Offer loyalty programs or incentives for registered users who are active on weekdays.

4.  **Fleet Management & Distribution**:
    - Optimize bike distribution based on hourly demand patterns (morning and evening peaks).
    - Adjust fleet size and maintenance schedules based on seasonal and weather-driven demand fluctuations to manage costs effectively.

5.  **Product Enhancements (Consideration)**:
    - Explore offering bikes with features better suited for varied weather conditions (e.g., better grip for rainy days, mudguards) if feasible, to mitigate the drop in rentals during unfavorable weather.

---

## 📌 Final Notes

All analysis and business insights are available in the notebook.

> For detailed charts, data wrangling, and interpretation, please refer to the full [Jupyter Notebook](./Yulu_Hypothesis_Testing.ipynb).

