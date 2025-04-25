# Trendyol Sales Performance Analysis

## Project Overview
I am a student from Sabancı University, **Cemre Çırak**, and this is my DSA210 term project. The aim of this project is to analyze the sales performance of a white goods seller on the Trendyol platform and identify patterns in customer behavior and product performance. The project includes data cleaning, preprocessing, exploratory data analysis, hypothesis testing, and visualizations.

## Contents
- [Motivation](#motivation)
- [Data Source](#data-source)
- [Preprocessing and Cleaning](#preprocessing-and-cleaning)
- [Gender Inference](#gender-inference)
- [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
- [Hypothesis Testing](#hypothesis-testing)
- [Findings](#findings)
- [Limitations and Future Work](#limitations-and-future-work)

---

## Motivation
- Understand which product categories are sold most frequently.
- Identify peak hours and days for sales performance.
- Analyze customer demographics (age, gender, location) and their relationship with product preference.
- Gain actionable insights to optimize pricing, targeting, and inventory management strategies.

---

## Data Source
- The data was collected from the Trendyol seller portal.
- It includes orders placed between **July and August 2024**.
- Format: Excel CSV files with detailed transaction-level information.

---

## Preprocessing and Cleaning
- Removed irrelevant columns (e.g., barcode, delivery address, invoice number).
- Standardized column names to lowercase with underscores.
- Converted date columns to `datetime` objects.
- Extracted new features: `hour`, `day_of_week`, and `is_weekend` from `order_date`.
- Product categories were inferred from the product name using a custom mapping function.

---

## Gender Inference
- The dataset had missing values for customer gender (~50%).
- To fill missing values, I used Turkish name frequency datasets (female, male, unisex) from GitHub.
- A normalization function removed Turkish characters from names.
- A new column `guessed_gender` was added:
  - If a name exists in both male and female datasets, the higher frequency was used.
  - If not found, labeled as `"Unknown"`.

---

## Exploratory Data Analysis (EDA)
- **Sales by Day:** Line chart showing total quantity sold per day.
- **Hourly Sales Trend:** Bar chart showing sales volume distribution over hours.
- **Category Distribution:** Count plot for top-selling product categories.
- **Sales by Gender:** Bar chart comparing purchase quantity by gender.
- **Sales by City:** Horizontal bar chart ranking cities by total quantity sold.

---

## Hypothesis Testing

### 1. Gender vs Product Category
- **Test:** Chi-Square Test of Independence
- **H₀:** Gender and product category are independent.
- **Result:** p-value < 0.05 → **Reject H₀** → Gender and category are associated.

### 2. Weekday vs Weekend Sales
- **Test:** Independent t-test
- **H₀:** Mean sales quantity is the same on weekdays and weekends.
- **Result:** p-value > 0.05 → **Fail to reject H₀** → No significant difference.

### 3. Sales by Hour
- **Test:** One-Way ANOVA
- **H₀:** No difference in sales quantity across different hours.
- **Result:** p-value < 0.05 → **Reject H₀** → Hour has a significant effect.

### 4. City vs Product Category
- **Test:** Chi-Square Test of Independence
- **H₀:** No relationship between city and product category.
- **Result:** p-value < 0.05 → **Reject H₀** → City and category are associated.

---

## Findings
- **Refrigerators, Dishwashers, and Washing Machines** are the most purchased categories.
- **Peak sales hours** are between 13:00 and 15:00.
- **Istanbul, Izmir, and Ankara** had the highest purchase volumes.
- Gender seems to influence the type of product purchased.

---

## Limitations and Future Work
- Many gender values were inferred, not directly provided.
- Age data was not always available or clean.
- No direct pricing optimization or machine learning model implemented yet.
- Future steps:
  - Use clustering to find customer segments.
  - Add pricing trend analysis.
  - Expand to a broader dataset covering a full year.

---

## Technologies Used
- Python (pandas, matplotlib, seaborn, scipy)
- Google Colab
- GitHub for version control and submission

---

## Repository Structure
```
.
├── data/                   # Raw and cleaned datasets
├── notebooks/             # Colab notebooks for EDA, preprocessing, and testing
├── images/                # All generated plots
├── README.md              # Project overview and documentation
└── requirements.txt       # Python dependencies
```

---

## Acknowledgements
Thanks to DSA210 instructors and Trendyol's seller platform for the data access.

