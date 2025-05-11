# 📊 Netflix Data Exploration & Visualization

This project analyzes a dataset containing details of all movies and TV shows available on Netflix as of mid-2021. The goal is to uncover trends, insights, and patterns to help Netflix make informed decisions about content production and business growth.


---

## 🧠 Problem Statement

Assume you're a data analyst at Netflix. Your task is to explore the Netflix catalog dataset to:

- Understand the distribution and evolution of content.
- Identify trends by genre, type, country, and rating.
- Generate insights to guide future content production.
- Recommend strategies to grow the business in different regions.

---

## 📦 Dataset Overview

The dataset contains the following columns:

| Column Name     | Description |
|----------------|-------------|
| `show_id`       | Unique ID for each title |
| `type`          | Movie or TV Show |
| `title`         | Title of the content |
| `director`      | Director's name |
| `cast`          | Leading actors |
| `country`       | Country of origin |
| `date_added`    | Date it was added to Netflix |
| `release_year`  | Release year of the content |
| `rating`        | TV Rating (e.g. TV-MA, PG) |
| `duration`      | Runtime or number of seasons |
| `listed_in`     | Genre(s) |
| `description`   | Short summary |

---

## 🔍 Key Insights

- **Content Mix:** Netflix’s catalog is ~70% Movies and ~30% TV Shows.
- **Content Growth:** Sharp increase in content additions post-2015.
  - Movie additions peaked around **Nov–Dec 2019**
  - TV Shows peaked around **Jul–Aug 2021**
- **Popular Genres:**
  - **Movies:** “International Movies” are most common; “Sports Movies” are rare.
  - **TV Shows:** Dominated by “International TV Shows” and “TV Dramas”.
- **Top Contributing Countries:**
  - **USA** leads in both movies and shows.
  - **India** is 2nd for movies.
  - **South Korea** is a major source for TV shows.
- **Content Duration:**
  - Most movies are around **100 minutes**.
  - TV shows generally have **1–2 seasons**.
- **Ratings Distribution:** “TV-MA” is the most frequent rating.
- **Data Quality:** Handled missing values in `director`, `cast`, `country`, `date_added`. Flattened multi-entry columns (e.g. genres, cast) for analysis.

---

## ✅ Recommendations

- **Diversify Ratings Portfolio:** Expand content in underrepresented rating categories to serve broader audiences.
- **Invest in Niche Genres:** Consider producing more **Sports Movies** and **TV Sci-Fi & Fantasy** to fill current gaps.
- **Continue Strong Content Acquisition:** Maintain high addition rates, especially aligned with observed seasonal peaks.
- **Regional Focus:**
  - Strengthen collaboration with content creators in **India** (Movies) and **South Korea** (TV).
- **Optimize Release Timing:** Leverage past addition patterns to plan strategic content releases in peak periods.

---

## 📊 Visualizations

The Jupyter notebook includes:
- Distribution plots
- Time series visualizations
- Genre and rating heatmaps
- Country-wise comparisons
- Correlation analysis

---

## 📂 How to Run

1. Clone the repository
2. Install required libraries: `pandas`, `matplotlib`, `seaborn`
3. Open and run the `Netflix_Data_Exploration.ipynb` notebook

---

## 📌 Final Notes

All analysis and business insights are available in the notebook.

> For detailed charts, data wrangling, and interpretation, please refer to the full [Jupyter Notebook](./Netflix_Data_Exploration.ipynb).
