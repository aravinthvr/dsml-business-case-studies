# 📊 Business Case Studies in Data Science & Machine Learning

Welcome to my collection of business case studies focused on real-world applications of Data Science, Analytics, and Machine Learning. Each project dives into a different business domain, applying statistical and ML techniques to solve practical problems using Python, SQL, and data visualization tools.

---

## 🗂️ Case Studies Overview

| #  | Case Study                          | Company             | Focus Area                                |
|----|------------------------------------|---------------------|--------------------------------------------|
| 01 | SQL Analysis                       | Target              | SQL Queries & Business Insights            |
| 02 | Data Exploration & Visualization   | Netflix             | EDA & Data Visualization                   |
| 03 | Descriptive Stats & Probability    | Aerofit             | Summary Stats & Probability Distributions  |
| 04 | Confidence Interval & CLT          | Walmart             | Inferential Statistics                     |
| 05 | Hypothesis Testing                 | Yulu                | A/B Testing & Hypothesis Testing           |
| 06 | Feature Engineering                | Delhivery           | Feature Creation & Data Preparation        |
| 07 | Linear Regression                  | Jamboree Education  | Predictive Modeling                        |
| 08 | Logistic Regression                | LoanTap             | Classification & Risk Modeling             |
| 09 | Ensemble Learning                  | OLA                 | Boosting, Bagging, Random Forests          |
| 10 | Clustering                         | Scaler              | Unsupervised Learning & Segmentation       |

---

## 🚀 Project Highlights & Key Learnings

Below is a summary of each case study, highlighting its objectives and key insights/outcomes.

### 01: SQL Analysis - Target Brazil E-commerce Operations
*   **Objective:** Perform SQL-based analysis on 100,000+ e-commerce orders (2016-2018) to understand customer behavior, logistics, payments, and product performance for Target's Brazil operations.
*   **Key Insights & Outcomes:**
    *   Identified trends in order volume growth, seasonal/hourly patterns, and customer distribution across cities/states.
    *   Analyzed popular payment methods, revenue growth (2017-2018), and average order values by state.
    *   Evaluated logistics by comparing delivery times against estimates, analyzing freight costs, and identifying states with fastest/slowest delivery.
    *   Assessed customer satisfaction through review score distribution and its correlation with delivery times.

### 02: Data Exploration & Visualization - Netflix Content Strategy
*   **Objective:** Explore Netflix's catalog (mid-2021) to understand content distribution, identify trends (genre, type, country, rating), and generate insights for future content production and regional growth.
*   **Key Insights & Outcomes:**
    *   Content Mix: ~70% Movies, ~30% TV Shows, with a sharp increase in additions post-2015.
    *   Popular Genres: "International Movies" (Movies), "International TV Shows" & "TV Dramas" (TV Shows).
    *   Top Contributors: USA (overall), India (movies), South Korea (TV shows).
    *   Recommendations: Diversify content ratings, invest in niche genres (e.g., Sports Movies), focus on content acquisition from key regions like India and South Korea, and optimize release timing based on seasonal peaks.

### 03: Descriptive Stats & Probability - Aerofit Treadmill Customer Profiling
*   **Objective:** Create customer profiles for three treadmill models (KP281, KP481, KP781) by analyzing purchase data, and use descriptive statistics and probability to inform marketing and product strategies.
*   **Key Insights & Outcomes:**
    *   KP281 (entry-level) is most popular. Customer profiles vary significantly by product:
        *   KP781 (high-end) preferred by males, higher-income, higher-education, and more fitness-oriented users.
    *   Identified distinct demographic (age, gender, marital status) and behavioral (usage, fitness level, income) segments for each product.
    *   Recommendations: Targeted marketing for upgrades (KP281 to KP481), strategies to boost KP781 sales among underrepresented demographics (e.g., females), and engagement plans for low-fitness users.

### 04: Confidence Interval & CLT - Walmart Black Friday Spending Analysis
*   **Objective:** Analyze customer purchase behavior during Walmart's Black Friday sales, focusing on spending differences based on gender, marital status, and age groups, using confidence intervals and CLT for data-backed decisions.
*   **Key Insights & Outcomes:**
    *   Gender: Male customers spend significantly more per transaction than female customers.
    *   Marital Status: No significant difference in average spending between married and unmarried customers.
    *   Age Groups: Customers aged 51+ have the highest average spend, while the 26-35 age group contributes most to total sales volume. Spending patterns show distinct age clusters.
    *   Recommendations: Target male shoppers with specific campaigns, prioritize key age demographics (26-35 for volume, 51+ for premium offers), and implement segmented marketing for age clusters.

### 05: Hypothesis Testing - Yulu Bike Sharing Demand Analysis
*   **Objective:** Identify significant variables predicting demand for Yulu's shared electric cycles and understand their impact, specifically investigating the effects of working days, seasons, and weather conditions on rental counts.
*   **Key Insights & Outcomes:**
    *   Working days have significantly higher rental counts than non-working days/holidays.
    *   Rental demand varies significantly across seasons (Fall highest, Spring lowest).
    *   Weather conditions significantly impact rentals (Clear weather highest, Rainy/Stormy lowest).
    *   A dependency exists between weather conditions and seasons.
    *   Temperature and "feels like" temperature positively correlate with rental counts, while humidity shows a negative correlation.

### 06: Feature Engineering - Delhivery Logistics Optimization
*   **Objective:** Clean, preprocess, and analyze raw logistics data for Delhivery. Engineer new features from existing columns, aggregate segment-level data to a trip level, and perform EDA to uncover patterns for improving delivery efficiency and route optimization.
*   **Key Insights & Outcomes:**
    *   Successfully aggregated multi-segment trip data into single trip records.
    *   Engineered crucial features like `actual_time_per_km`, `osrm_time_per_km`, `time_diff_osrm_actual`, `source_state`, `destination_state`, and various time-based features (hour, day, month).
    *   Analysis revealed discrepancies between actual and OSRM (estimated) logistics metrics, providing a basis for route and time estimation improvements.
    *   Identified patterns in delivery performance based on route types, time of day, and geographical factors.

### 07: Linear Regression - Jamboree Education Admission Prediction
*   **Objective:** Identify key factors influencing graduate school admissions, build a Linear Regression model to predict a student's "Chance of Admit," validate model assumptions, and provide actionable insights for students and Jamboree.
*   **Key Insights & Outcomes:**
    *   Significant predictors for "Chance of Admit" include GRE Score, TOEFL Score, University Rating, LOR strength, Undergraduate CGPA, and Research experience.
    *   Developed a Linear Regression model with an R-squared of ~0.82, indicating good predictive power.
    *   'SOP' (Statement of Purpose strength) was found to be less significant and potentially multicollinear, leading to its exclusion from the final model.
    *   Model assumptions (linearity, normality of residuals, multicollinearity via VIF) were validated.
    *   Recommendations: Students should focus on improving scores in identified key areas. Jamboree can use the model to enhance its admission prediction tool.

### 08: Logistic Regression - LoanTap Loan Default Prediction
*   **Objective:** Analyze borrower attributes to predict loan repayment status (`loan_status`: Fully Paid vs. Charged Off) for LoanTap. Build and evaluate a Logistic Regression model to inform credit underwriting and risk assessment.
*   **Key Insights & Outcomes:**
    *   Identified key financial and demographic features influencing loan default probability.
    *   Developed a Logistic Regression model achieving good performance (e.g., ROC AUC ~0.90 on test, F1-score ~0.88 for 'Fully Paid' class after threshold tuning).
    *   Feature engineering included extracting year/month from dates, creating flags for public records/bankruptcies, and one-hot encoding categorical variables.
    *   Insights enable LoanTap to refine its underwriting criteria, better assess risk, and potentially reduce charge-offs.

### 09: Ensemble Learning - OLA Driver Churn Prediction
*   **Objective:** Apply ensemble machine learning techniques to predict driver attrition at OLA by analyzing driver demographics, performance, financial metrics, and activity data, enabling data-driven retention strategies.
*   **Key Insights & Outcomes:**
    *   Strongest predictors of churn: Total Business Value, Income, Age, Quarterly Rating improvements, and Activity Level.
    *   XGBoost with SMOTE (to handle class imbalance) yielded the best performance (F1 Score: 0.9383, ROC-AUC: 0.9628).
    *   Identified city-specific churn variations and the impact of tenure on attrition.
    *   Recommendations: Implement targeted retention programs (city-specific, tenure-based), income stabilization measures, performance management, and deploy the model as an early-warning system for proactive intervention.

### 10: Clustering - Scaler Learner Segmentation
*   **Objective:** Segment Scaler's learners based on experience, compensation, job role, and employer characteristics using manual (rule-based) and unsupervised (K-Means, Hierarchical) clustering to understand compensation benchmarks, identify learner personas, and inform tailored interventions.
*   **Key Insights & Outcomes:**
    *   Successfully segmented learners into 5 distinct personas (e.g., Mid-Career Generalists, Backend Specialists, Experienced with Modest CTC, Dynamic Earners with Frequent Switches) using K-Means clustering.
    *   Derived features like `year_of_exp` and `no_of_ctc_update` proved valuable.
    *   Manual clustering based on peer-level CTC comparisons provided initial segmentation insights.
    *   PCA was used for visualizing clusters.
    *   Outcomes enable Scaler to provide personalized career guidance, optimize curriculum, and tailor support strategies based on data-driven learner personas.

---

## 🔧 Technologies Used

- **Languages**: Python, SQL
- **Libraries**: Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, Statsmodels, XGBoost, imblearn, Yellowbrick
- **Tools & Platforms**: Jupyter Notebook, Git, GitHub, Google BigQuery, MySQL

---

## 📁 Folder Structure

Each folder contains:
- `README.md` with case-specific description
- `.ipynb` notebook with full analysis and code


--- 

## 📬 Contact
If you have any questions or feedback, feel free to reach out via <a href="https://www.linkedin.com/in/aravinthvr/">LinkedIn</a> or <a href="mailto:aravinthvr@gmail.com">Email</a>.