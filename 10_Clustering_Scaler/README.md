# 📊 Scaler Learner Clustering - Data Science Project

## 🧠 Business Context & Goals

Scaler, a tech-focused ed-tech platform, seeks to better understand its learner base to optimize course offerings, career guidance, and employer partnerships. This project segments learners based on experience, compensation, job role, and employer characteristics to surface actionable insights.

### Goals:
- Segment learners using both manual (rule-based) and unsupervised (K-Means, Hierarchical) clustering.
- Understand compensation benchmarks by role, experience, and company.
- Identify learner personas and recommend tailored interventions.
- Inform curriculum design and career support strategies.

---

## 🧩 Problem Statement

Without clear segmentation, it’s difficult for Scaler to:
- Benchmark compensation across similar experience and roles.
- Identify high-potential or underserved learner groups.
- Provide personalized guidance on salary negotiation, job targeting, or upskilling.

This project solves this by using clustering to group learners into data-driven personas.

---

## 📁 Dataset Overview

**File:** `scaler_clustering.csv`
**Source:** Provided by Scaler (anonymized)

### Key Features:

| Feature                  | Description                                 |
|--------------------------|---------------------------------------------|
| `company_hash`           | Anonymized employer                         |
| `email_hash`             | Learner ID (used to count CTC updates)      |
| `orgyear`                | Year joined current company                 |
| `ctc`                    | Current CTC (salary in ₹ LPA)               |
| `job_position`           | Current job title                           |
| `ctc_updated_year`       | Last CTC update year                        |

### Derived Features:
- `year_of_exp`: 2025 - `orgyear` (Current year based on notebook execution context)
- `no_of_ctc_update`: Count of CTC changes per learner
- Frequency encoding: `company_hash`, `job_position`
- `ctc_log`: Log-transformed CTC
- Manual flags: `designation`, `class`, `tier` — based on peer-level comparisons

---

## ✅ Project Workflow

### 1. 🔎 Data Cleaning & EDA
- Removed duplicates, fixed invalid `orgyear` (by setting to NaN then imputing), imputed missing `job_position` using a multi-step mode-based approach.
- Cleaned `company_hash` with regex.
- Handled outliers (clipping/filtering) and applied type conversions.
- Created key features like `year_of_exp` and grouped rare companies ( < 5 records) into `less_occurred`.

### 2. 🛠 Manual Clustering
- Built three flags (`designation`, `class`, `tier`) comparing an individual's CTC against the mean CTC of their peer group:
  - `designation`: Peers with same `year_of_exp` + `job_position` + `company_hash`
  - `class`: Peers with same `job_position` + `company_hash`
  - `tier`: Peers within the same `company_hash`
- Used these flags to analyze segments like top/bottom performers and understand relative compensation.

### 3. 🤖 Unsupervised Clustering
- **Preprocessing**: Selected features, created `no_of_ctc_update`, applied frequency encoding to `company_hash` & `job_position`, log-transformed `ctc`, and standardized numerical features.
- **Optimal Cluster Selection**: Used the **Elbow Method** (KElbowVisualizer with K-Means inertia), which suggested k=5. Hopkins statistic indicated good clusterability.
- **Model Training**: Ran **K-Means** with k=5.
- **Validation**: Validated cluster structure using **Hierarchical Clustering (Ward's linkage)** on a data sample, which also supported 5 clusters.
- **Visualization**: Used **PCA** to reduce dimensions and visualize K-Means clusters.

---

## 🧠 Cluster Profiles

| Cluster | Summary                        | Avg. CTC | Exp (yrs) | CTC Updates | Common Roles (Top 3)             | Common Companies (Top 3 from notebook)         |
|--------:|--------------------------------|----------|-----------|-------------|----------------------------------|------------------------------------------------|
| 0       | Mid-Career Generalists         | ₹9.26L   | 8.3       | 1.40        | FullStack Engineer, Other, Frontend Engineer | `less_occurred`, RrCompany, Flipkart Internet  |
| 1       | Backend Specialists            | ₹14.70L  | 9.2       | 1.41        | Backend Engineer, FullStack Engineer, Other | `less_occurred`, Amazon, Walmart Labs          |
| 2       | Experienced, Modest CTC        | ₹9.44L   | 9.7       | 1.40        | Backend Engineer, FullStack Engineer, Other | `less_occurred`, Tata Consultancy Services, Cognizant Technology Solutions |
| 3       | Dynamic Earners (Frequent Sw.) | ₹12.84L  | 8.1       | 3.47        | Backend Engineer, FullStack Engineer, Other | `less_occurred`, Amazon, Microsoft             |
| 4       | Senior Leaders                 | ₹27.04L  | 17.5      | 1.35        | Engineering Manager, Other, Backend Engineer | `less_occurred`, Amazon, Microsoft             |

*(Note: "Common Companies" are based on the notebook's output, where `less_occurred` signifies a consolidation of companies with few individual records.)*

---

## 💡 Recommendations for Scaler

### 🎯 Curriculum Development
- **Backend Track Investment:** High returns and demand are evident for backend specialists (Cluster 1) and leadership roles often rooted in backend (Cluster 4). Continue to enhance and promote specialized backend tracks.
- **Leadership Pathways:** Develop and expand programs for aspiring or current tech leaders (targeting profiles similar to Cluster 4).
- **Career Agility Training:** The success of Cluster 3 (Dynamic Earners) highlights the value of job-switching and negotiation. Incorporate training on these skills.

### 🧭 Career Services
- **Guidance for Cluster 2 (Experienced, Modest CTC):** Offer targeted coaching to help these learners leverage their experience for better compensation, possibly by focusing on different company tiers or acquiring niche, in-demand skills.
- **Mid-Career Generalist Upskilling (Cluster 0):** Support these learners by outlining clear paths to specialization (e.g., advanced backend, data science, ML) that could lead to higher earning potential.
- **Salary Benchmarking:** Utilize the cluster data to provide learners with realistic and personalized CTC expectations based on their profile.

### 🤝 Employer Engagement
- **Target High-Hiring Companies:** Focus partnership efforts on companies that frequently hire for roles observed in the higher-CTC clusters (e.g., specialized backend, engineering management).
- **Highlight Backend Talent Pool:** Actively promote the strong pool of backend-focused talent (Clusters 1 & 3) to relevant employers.

---

## 📦 Tech Stack

- **Languages:** Python
- **Notebook:** Jupyter
- **Libraries:**
  - Data Manipulation & Analysis: `pandas`, `numpy`
  - Visualization: `matplotlib`, `seaborn`
  - Data Cleaning: `re` (Regular Expressions)
  - Date/Time: `datetime`
  - Machine Learning & Clustering: `sklearn` (KMeans, PCA, StandardScaler, KNNImputer, SimpleImputer, NearestNeighbors)
  - Hierarchical Clustering: `scipy.cluster.hierarchy` (linkage, dendrogram, fcluster)
  - Cluster Evaluation Aids: `yellowbrick.cluster` (KElbowVisualizer)
  - Utilities: `collections.Counter`, `warnings`

---

## ✅ Outcome

This project delivers a data-backed segmentation of Scaler's learners, enabling:
- More targeted and effective curriculum design and career service offerings.
- Provision of realistic compensation guidance to learners.
- More strategic and informed employer partnership development.

These insights can directly contribute to improved learner success, satisfaction, and enhance Scaler's competitive positioning in the ed-tech market.

---

## 📌 Final Notes

For a detailed walkthrough of the data analysis, feature engineering, clustering process, and interpretation, please refer to the full Jupyter Notebook:
[`scaler_clustering.ipynb`](./scaler_clustering.ipynb)

---