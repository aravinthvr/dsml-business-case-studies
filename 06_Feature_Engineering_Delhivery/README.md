# 🚚 Delhivery - Logistics Data Analysis & Feature Engineering Case Study

## 📦 Business Context

Delhivery is India’s largest and fastest-growing fully integrated logistics company. With a vision to become the operating system for commerce, they aim to optimize operations by leveraging data, technology, and intelligent decision-making.

This case study focuses on cleaning, processing, and analyzing raw logistics data to extract meaningful features and insights. The goal is to prepare the data for potential downstream tasks like predictive modeling and to understand key operational patterns.

---

## 🎯 Problem Statement

The primary objectives are to:
- **Understand and preprocess raw delivery data**, where each trip is often represented by multiple rows (segments).
- **Clean the data** by handling missing values, irrelevant columns, and ensuring correct data types.
- **Engineer new features** from existing columns to provide more granular insights.
- **Aggregate segment-level data** to a trip level for a holistic view.
- **Perform exploratory data analysis (EDA)** to uncover patterns and trends.
- **Conduct hypothesis testing** to validate assumptions about key time and distance metrics.
- **Generate actionable business insights** to potentially improve delivery efficiency and route optimization.

---

## 📁 Dataset Overview

Dataset Name: `delhivery_data.csv`

Each row initially represents a **segment** of a trip. The analysis involves aggregating these segments to represent complete trips.

| Column                         | Description                                                                                                |
|--------------------------------|------------------------------------------------------------------------------------------------------------|
| data                           | Indicates if the row belongs to a test or training set (in the original context)                           |
| trip_creation_time             | Timestamp when the trip was created                                                                        |
| route_schedule_uuid            | Unique identifier for a scheduled route                                                                    |
| route_type                     | Type of transportation (FTL: Full Truck Load, Carting: System with small vehicles)                         |
| trip_uuid                      | Unique trip identifier                                                                                     |
| source_center                  | Source ID of trip origin                                                                                   |
| source_name                    | Source Name of trip origin (includes city/place and state)                                                 |
| destination_center             | Destination ID of trip                                                                                     |
| destination_name               | Destination Name of trip (includes city/place and state)                                                   |
| od_start_time                  | Trip start timestamp (Origin-Destination start)                                                            |
| od_end_time                    | Trip end timestamp (Origin-Destination end)                                                                |
| start_scan_to_end_scan         | Total time in minutes from the first scan to the last scan for the trip                                    |
| actual_distance_to_destination | Actual total distance in kilometers for the trip                                                           |
| actual_time                    | Actual time taken in minutes for the trip (cumulative for segments in raw data)                            |
| osrm_time                      | OSRM (Open Source Routing Machine) predicted time in minutes for the trip (cumulative for segments)        |
| osrm_distance                  | OSRM predicted distance in kilometers for the trip (cumulative for segments)                               |
| segment_actual_time            | Actual time taken in minutes for an individual segment of the trip                                         |
| segment_osrm_time              | OSRM predicted time in minutes for an individual segment                                                   |
| segment_osrm_distance          | OSRM predicted distance in kilometers for an individual segment                                            |
| *Unknown Fields (Dropped)*     | `is_cutoff`, `cutoff_factor`, `cutoff_timestamp`, `factor`, `segment_factor` (deemed irrelevant)           |

---

## 🔧 Steps Performed

### ✅ 1. Data Cleaning & Exploration

- **Initial Review**: Loaded data, checked shape, data types, and basic statistics.
- **Irrelevant Columns**: Dropped unknown/irrelevant columns: `is_cutoff`, `cutoff_factor`, `cutoff_timestamp`, `factor`, `segment_factor`.
- **Data Type Conversion**: Converted timestamp columns (`trip_creation_time`, `od_start_time`, `od_end_time`) to datetime objects and relevant categorical columns to `category` type.
- **Missing Values**: Identified missing values in `source_name` and `destination_name`. Since the percentage was very low (<0.2%), rows with these missing values were dropped.
- **Duplicate Check**: Checked for duplicate rows (none found after initial processing).

### ✅ 2. Feature Engineering

- **New Features Created** (primarily on aggregated data):
    - **`trip_time(mins)`**: Calculated as `(od_end_time - od_start_time)` in minutes.
    - **Location Features**:
        - `source_city`, `source_state`, `source_place`
        - `destination_city`, `destination_state`, `destination_place`
        - Extracted from `source_name` and `destination_name` using string manipulation and a predefined IATA code to city mapping for standardization.
    - **Temporal Features from `trip_creation_time`**:
        - `trip_creation_date`, `trip_creation_day` (of month), `trip_creation_month`, `trip_creation_week` (of year), `trip_creation_hour`.

### ✅ 3. Data Aggregation

- **Objective**: Consolidate multiple segment rows for a single trip into one representative row.
- **`agg_df`**: Grouped data by `trip|src|dest` (a composite key of `trip_uuid`, `source_center`, `destination_center`). Used `first` or `last` aggregation for most fields, assuming these are consistent per defined trip segment group. This dataframe was used for most EDA and feature creation.
- **`agg_df_2`**: Grouped data by `trip_uuid`. For segment-specific metrics (`segment_actual_time`, `segment_osrm_time`, `segment_osrm_distance`), `sum` was used to get trip-level totals. Other fields used `first` or `last`. This dataframe was primarily used for hypothesis testing involving trip-level sums.

### ✅ 4. Exploratory Data Analysis (EDA)

- **Univariate Analysis**:
    - **Route Types**: Slightly more `Carting` trips (~53%) than `FTL` trips (~47%).
- **Bivariate Analysis & Temporal Trends**:
    - **Geographic Focus**: Maharashtra and Karnataka emerged as prominent states for both trip origins and destinations. Bengaluru, Mumbai, and Chennai were among the top cities.
    - **Trip Creation Hour**: Peaks observed late in the evening (around 22:00 hours).
    - **Trip Creation Day of Month**: Highest volume around the middle of the month (e.g., 17th).
    - **Trip Creation Week of Year**: A notable peak in trip volume during the 38th week of the year in this dataset.
- **Correlation Analysis**:
    - Strong positive correlation between `trip_time(mins)` and `start_scan_to_end_scan`.
    - Positive correlations observed between actual distance/time and OSRM predicted distance/time.

### ✅ 5. Hypothesis Testing (using `agg_df` or `agg_df_2` as appropriate)

Non-parametric Kolmogorov-Smirnov (KS) test was used for comparing distributions due to non-normality of data (confirmed by Shapiro-Wilk tests and Q-Q plots), even after log transformations were attempted. Significance level (alpha) = 0.05.

- **`trip_time(mins)` vs. `start_scan_to_end_scan`** (on `agg_df`):
    - **Null Hypothesis**: The two distributions are the same.
    - **Result**: Failed to reject Null Hypothesis (p-value > 0.05). Distributions are statistically similar.
- **Aggregated `actual_time` vs. Aggregated `osrm_time`** (trip-level sum from `agg_df_2`):
    - **Null Hypothesis**: The two distributions are the same.
    - **Result**: Rejected Null Hypothesis (p-value < 0.05). Distributions are statistically different.
- **Aggregated `actual_time` vs. Sum of `segment_actual_time`** (trip-level from `agg_df_2`):
    - **Null Hypothesis**: The two distributions are the same.
    - **Result**: Failed to reject Null Hypothesis. Summing segment actual times is consistent with the provided trip-level actual time.
- **Aggregated `osrm_distance` vs. Sum of `segment_osrm_distance`** (trip-level from `agg_df_2`):
    - **Null Hypothesis**: The two distributions are the same.
    - **Result**: Failed to reject Null Hypothesis. Summing segment OSRM distances is consistent.
- **Aggregated `osrm_time` vs. Sum of `segment_osrm_time`** (trip-level from `agg_df_2`):
    - **Null Hypothesis**: The two distributions are the same.
    - **Result**: Failed to reject Null Hypothesis. Summing segment OSRM times is consistent.

### ✅ 6. Outlier Analysis

- **Detection**: Visualized using histograms and boxplots, showing right skewness in most numerical features. IQR method was used to quantify outliers.
- **Handling**: Outliers were identified but **retained** in the dataset, as they might represent genuine operational variations rather than errors.

---

## 💡 Business Insights

1.  **Data Integrity & Preparation**:
    *   Successfully cleaned raw data by removing irrelevant columns and handling minimal missing entries.
    *   Standardized location data (city, state) enhances consistency for analysis.
2.  **Feature Engineering Value**:
    *   Newly created features like `trip_time(mins)` and granular temporal features (`trip_creation_hour`, `day`, `week`) provide richer dimensions for analysis and potential modeling.
3.  **Operational Patterns**:
    *   **Route Dominance**: `Carting` trips are slightly more frequent than `FTL`.
    *   **Key Geographies**: Operations are heavily concentrated in Maharashtra and Karnataka.
    *   **Peak Times**: Trip initiation is highest in the late evening. Mid-month and specifically the 38th week (in this dataset) show higher activity.
4.  **Performance & Prediction Metrics**:
    *   `start_scan_to_end_scan` is a statistically validated measure for overall trip duration, being similar to the calculated `trip_time(mins)`.
    *   There's a statistically significant difference between OSRM's predicted trip times and actual trip times, suggesting OSRM alone may not capture all real-world delays or factors.
    *   Aggregating segment-level data (actual time, OSRM distance, OSRM time) by summing them up provides a reliable trip-level view, consistent with provided trip-level totals.
5.  **Outliers**:
    *   Numerical features exhibit outliers, likely reflecting the inherent variability in logistics operations (e.g., exceptionally long or short trips due to various factors). These were retained for analysis.

---

## ✅ Recommendations

1.  **Improve OSRM Accuracy/Utility**:
    *   Investigate the discrepancies between `actual_time` and `osrm_time`. Analyze trips with large deviations to identify contributing factors (e.g., specific routes, times of day, vehicle types, undocumented stops) not currently modeled by OSRM.
    *   Consider incorporating additional data sources (e.g., real-time traffic, weather) or calibrating OSRM parameters if possible.
2.  **Optimize Resource Allocation**:
    *   Align vehicle deployment, staffing, and warehouse operations with observed demand peaks: late evenings, mid-month periods, and historically busy weeks (like the 38th week).
3.  **Strategic Route & Network Focus**:
    *   Given the high trip volume in Maharashtra and Karnataka, prioritize route optimization efforts, infrastructure assessment, and potentially targeted service improvements in these states.
4.  **Data-Driven Reporting & Modeling**:
    *   Reliably use `start_scan_to_end_scan` (or the derived `trip_time(mins)`) for reporting and KPIs related to trip duration.
    *   When building predictive models (e.g., for ETA forecasting), be mindful of the OSRM deviations. Consider using actual historical times as a stronger baseline or feature.
    *   For models sensitive to outliers, evaluate robust statistical techniques or specific outlier treatment strategies if they are determined to be non-representative of the phenomena being modeled.
5.  **Further Investigation**:
    *   Deep-dive into the reasons for the trip surge in the 38th week (e.g., seasonal demand, specific campaigns, data collection period).
    *   Conduct a comparative performance analysis (e.g., time efficiency, cost-effectiveness if data available) between 'FTL' and 'Carting' route types across different regions or trip characteristics.

---
## 📌 Final Notes

All analysis and business insights are available in the notebook.

> For detailed charts, data wrangling, and interpretation, please refer to the full [Jupyter Notebook](./Delhivery_CaseStudy.ipynb).
