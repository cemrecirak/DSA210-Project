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
- [Machine Learning Modeling](#machine-learning-modeling)
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
- The data was collected directly from the Trendyol seller portal through the seller's profile.
- It includes orders placed in **August 2024**.
- Format: Excel CSV files with detailed transaction-level information.

---

## Preprocessing and Cleaning
This Section has been explained further in the Data Processing part.
What I did in this section is:
- Translated the column names from Turkish to English.
- Removed irrelevant columns (e.g., barcode, delivery address, invoice number).
- Standardized column names to lowercase with underscores.
- Converted date columns to `datetime` objects.
- Extracted new features: `hour`, `day_of_week`, and `is_weekend` from `order_date`.
- Observed the columns with missing information.
- Age and gender data was not always available, for the missing gender data, I used a gender inference method which is explained below but since a lot of age data was missing I eliminated the missing data.
- Product categories were inferred from the product name using a custom mapping function.

---

## Gender Inference
- The dataset had missing values for customer gender (~50%).
- To fill missing values, I used large Turkish name frequency datasets (female, male, unisex) available on GitHub.
- A normalization function removed Turkish characters from names (e.g., "ş", "ç", "ö").
- A new column `guessed_gender` was added:
  - If a name exists in both male and female datasets, the higher frequency was used.
  - If not found, labeled as `"Unknown"`.
- As a result of this inference method only 4 names were labeled as `"Unknown"`, those entries either contained typos, non-Turkish names or did not belong to individuals.
- I also ran a chi-square hypothesis test to make sure this method was reliable. I compared the true gender vs the inferred gender and the results showed that the method was reliable.

---

## Exploratory Data Analysis (EDA)
This part had been explained further in the Data Visualization part.
I plotted various charts to visualize data to explore patterns to guide me throughout the hypothesis testing part.
- **Sales by Day:** Line chart showing total quantity sold per day.

- **Hourly Sales Trend:** Bar chart showing sales volume distribution over hours.


- **Category Distribution:** Count plot for top-selling product categories.
  
- **Sales by Gender:** Bar chart comparing purchase quantity by gender.
- **Sales by City:** Horizontal bar chart ranking cities by total quantity sold.
### 1. Daily Sales Trend
- ⁠This line chart shows the number of units sold each day throughout August.
- ⁠Peaks appear on August 4, 10, and 14, indicating high-activity days.
- ⁠Dips after peaks may suggest day-of-week variation or post-campaign cooling.
![image](https://github.com/user-attachments/assets/c8bd6b5b-672a-4980-b527-9deef8d17df4)

### 2. Total Quantity Sold per Product Category
- ⁠Dishwashers, Washing Machines, and Ovens lead in sales.
- ⁠Meat Grinders, Dust Bags, and 'Other' performed the lowest.
- ⁠Helps identify high-demand appliances.
![image](https://github.com/user-attachments/assets/74a218db-eece-4736-8324-d60dc17546ef)

### 3. Order Frequency by Hour
- ⁠Order volume increases after 9:00, peaks around 13:00 and 21:00.
- ⁠Early morning and late night hours show minimal activity.
- ⁠Useful for optimizing campaign timing.
![image](https://github.com/user-attachments/assets/5ec42366-77bd-49d8-812a-3d3137d956ef)

### 4. Product Category Distribution by Gender
- Males dominate sales in most categories.⁠
- Females show more interest in Kitchen Robots, Coffee Machines, Blenders.
- ⁠Suggests marketing differentiation by gender.
![image](https://github.com/user-attachments/assets/5cae239a-4356-44d7-8be6-f1230456f6c4)


### 5. Sales by City
- ⁠Istanbul, Ankara, and Antalya recorded the highest sales volumes.
- ⁠Regional insights support targeted marketing and logistics planning.
![image](https://github.com/user-attachments/assets/a7461d51-d829-40f8-b5b6-12905cf18240)


### 6. Product Category Distribution by Age
 - 31–40 age group shows high variety and volume of purchases.
 - Useful for age-based product targeting and positioning.
![image](https://github.com/user-attachments/assets/44a1cbe4-ad35-4cea-abe2-35b80d98793f)


### 7. Sales Heatmap by Day and Hour
- ⁠Visualizes temporal sales intensity.
- Highest activity seen during Friday evenings and Sunday afternoons.⁠
- Helps with operational planning and campaign scheduling.
![image](https://github.com/user-attachments/assets/a2992160-833f-4913-8811-aaed2ed8bd55)



---

## Hypothesis Testing
The code i used to run the statistical tests can be found in the Hypothesis Testing section.

### 1. Gender vs Product Category
- **Test:** Chi-Square Test of Independence
- **H₀:** Gender and product category are independent.
- **H₁:** Gender and product category are associated.
- **Result:** p = 0.0001 → p-value < 0.05 → **Reject H₀** → Gender and category are associated.

### 2. Weekday vs Weekend Sales
- **Test:** Independent t-test
- **H₀:** Mean sales quantity is the same on weekdays and weekends.
- **H₁:** Mean sales quantity differs on weekdays and weekends
- **Result:** p = 0.2928 → p-value > 0.05 → **Fail to reject H₀** → No significant difference.

### 3. Sales by Hour
- **Test:** One-Way ANOVA
- **H₀:** No difference in sales quantity across different hours.
- **H₁:** Hour has a significant effect on the sales quantity.
- **Result:** p = 0.6304 → p-value < 0.05 → **Fail to reject H₀** → No significant relationship between hour and sales quantity.

### 4. City vs Product Category
- **Test:** Chi-Square Test of Independence
- **H₀:** No relationship between city and product category.
- **H₁:** City and product category are associated.
- **Result:** p = 0.9778 → p-value < 0.05 → **Fail to reject H₀** → No significant relationship between province and product category.

---

## Machine Learning Modeling

In order to extend the analysis with predictive capabilities, I implemented a machine learning pipeline to predict the number of items sold per hour using features such as `hour`, `unit_price`, and `guessed_gender`. This prediction task was to better understand the shopping pattern of the customers to support campaign scheduling and inventory planning in the e-commerce operations. I applied three regression models:

* Linear Regression
* Random Forest Regressor
* Decision Tree Regressor

The models were evaluated using Leave-One-Out Cross-Validation (LOOCV), which is appropriate for smaller datasets and provides robust validation. The following metrics were calculated for each model:

* **Mean Squared Error (MSE)**
* **R² Score**

Additionally, scatter plots comparing actual versus predicted quantities were plotted for each model to visually assess performance. The ideal prediction line was used as a reference.

### Results Summary

* **Linear Regression:** R² = 0.43, MSE = 70.53
![image](https://github.com/user-attachments/assets/1e7613a3-6a58-4e28-99ca-eeff6161651e)

* **Random Forest:** R² = 0.79, MSE = 26.35
  ![image](https://github.com/user-attachments/assets/12ece959-cf55-42f6-b1e0-66a534be9ea9)

* **Decision Tree:** R² = 0.69, MSE = 38.09

  ![image](https://github.com/user-attachments/assets/f47b9b5c-d971-48e1-af76-cfaa3bed7dde)


The best performing model was **Random Forest**, achieving the highest R² score of 0.79. This indicates strong predictive accuracy in modeling hourly sales quantity.

Finally, the best performing model was selected based on the highest R² score. For the winning model (Random Forest or Decision Tree), feature importance was visualized to understand which variables most influenced the model’s predictions.

This modeling section adds predictive insight to the project and provides a scalable framework for future use.

---


## Findings

- **Top-Selling Categories**  
  Dishwashers, Washing Machines, and Refrigerators were the most purchased product categories, indicating strong demand for essential white goods.

- **Sales Timing Patterns**  
  Daily and hourly analysis revealed distinct sales peaks:
  - Peak hours were observed between **13:00 and 15:00**, and around **21:00**.
  - Notable sales spikes occurred on **August 4, 10, and 14**, suggesting the influence of specific campaigns or weekend shopping activity.

- **Regional Sales Insights**  
  - **Istanbul**, **Ankara**, and **Antalya** recorded the highest number of units sold.
  - These differences imply that regional demand varies and that location-based marketing and stock planning can improve efficiency.

- **Gender-Based Purchasing Behavior**  
  - Male customers led purchases in most product categories, especially large appliances.
  - Female customers showed more interest in Kitchen Robots, Coffee Machines, and Blenders.
  - These trends support the use of gender-targeted advertising and promotions.

- **Age-Based Product Preferences**  
  - The **31–40 age group** made the highest number of purchases across almost all categories.
  - This demographic appears to be the most active customer base and could be prioritized in targeted marketing strategies.

- **Temporal Buying Behavior**  
  - A sales heatmap revealed that **Friday evenings and Sunday afternoons** were peak shopping periods.
  - Sales volume was lowest during early mornings and late-night hours.

- **Hypothesis Test Results Summary**  
  - **Gender and Product Category:** Significant association (p = 0.0001)  
  - **Weekday vs. Weekend Sales:** No significant difference (p = 0.2928)  
  - **Sales by Hour:** No significant variation across hours (p = 0.6304)  
  - **City and Product Category:** No significant relationship (p = 0.9778)

- **Machine Learning Findings**

  * Predictive modeling was conducted to estimate hourly sales quantity using features like hour of day, unit price, and inferred gender.
  * Among three models tested, **Random Forest Regressor** performed best with an **R² score of 0.79** and lowest MSE of **26.35**.
  * This indicates a strong relationship between the selected features and actual sales behavior, demonstrating the viability of using regression-based ML approaches in demand forecasting.

---

## Limitations
- Many gender values were inferred, not directly provided.
- Age data was not always available or clean.
- The data was limited to one month so no seasonal trends could be observed.
- Incorporating more time-based features (e.g. campaign periods, holidays)
- Using a larger dataset to support deep learning or ensemble models
- Comparing alternative validation methods (e.g. time-series split)


---

## Technologies Used
- Python (pandas, matplotlib, seaborn, scipy)
- Google Colab
- GitHub



