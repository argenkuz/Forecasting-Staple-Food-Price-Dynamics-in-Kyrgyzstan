#### **Table of Contents**
1. **Introduction**
2. **Data Description**
3. **Data Analysis**
4. **Visualizations**
5. **Conclusion**
6. **References**
---

### **1. Introduction**

## Title
Forecasting Staple Food Price Dynamics in Kyrgyzstan: Time-Series Analysis of Monthly Consumer Price Indices (2003–2024)

## Abstract  
This study presents a comprehensive analysis of staple food price dynamics in Kyrgyzstan by examining official monthly Consumer Price Index (CPI) indicators from the National Statistical Committee of the Kyrgyz Republic. The dataset spans the years 2003 to 2024 and includes price-change metrics for major consumer food categories, including flour and grain products, meat, dairy, oils and fats, and fish. The main objective of this research is to evaluate long-term and short-term structural patterns in food price behavior and to build predictive models capable of forecasting future price fluctuations. This topic is socially and economically relevant for Kyrgyzstan, where food prices have a direct impact on purchasing power, household well-being, and overall inflation dynamics.

The analysis incorporates both statistical and machine-learning approaches, including moving-average smoothing, Linear Regression, Random Forest Regression, and ARIMA/Prophet-based time-series forecasting. In addition to numerical analysis, extensive exploratory data visualization is used, including seasonal trend graphs, rolling mean comparisons, and cross-category correlation matrices. The initial results indicate strong seasonal sensitivity in certain categories, with oils and fats demonstrating the highest volatility. Meat prices show a consistent upward trend over the long term, while flour and grain prices exhibit cyclical behavior corresponding to periods of global market disruption and domestic policy shifts. Forecasting experiments show that ARIMA and Prophet significantly outperform conventional regression models due to their robustness in capturing seasonality and trend-shift effects.

Ultimately, the findings contribute to a deeper understanding of food price evolution in Kyrgyzstan and offer practical forecasting tools for policymakers, retailers, and consumers. The ability to anticipate price movements in staple food products supports better economic planning, improves market transparency, and strengthens resilience against inflationary pressures affecting everyday life in the country.

---

**Authors:** Turdukulov Aidin and Kulzhanov Argen  
**Group:** MATDAIS-23

---
https://stat.gov.kg/en/

### **2. Data Description**

The dataset used in this analysis contains monthly CPI (Consumer Price Index) observations from Kyrgyzstan across multiple food product categories. It includes the following variables:

### Core Temporal Features
- **Year (`year`)**: The calendar year of observation (ranging from 2003 to 2025).
- **Month (`month`)**: The month of observation (from 1 to 12), allowing identification of seasonal price patterns.
- **Time Index (`time_index`)**: A continuous numerical index representing each month sequentially over the entire dataset, used for modeling temporal trends.
  
### CPI Price Features
- **Value (`value`)**: The CPI value for the specific food category during the given month. This indicates price level relative to the baseline (CPI = 100).
- **Previous Month Value (`previous_month_value`)**: The CPI value for the same category in the preceding month. This feature captures short-term inertia in price changes.
- **Yearly Trend (`yearly_trend`)**: Difference between the current CPI and the CPI of the same month one year earlier. This reflects long-term price deviation.

### Seasonality Features
- **Month Sin (`month_sin`)** and **Month Cos (`month_cos`)**: Cyclical encodings of the month variable that allow machine learning models to capture repeating annual seasonality patterns.

### Category One-Hot Encoded Variables
Binary columns indicating the product group:

- `category_bread`
- `category_fish`
- `category_fruits`
- `category_meat`
- `category_milk_egg_cheese`
- `category_soft_drinks`
- `category_sugar_chocolate`
- `category_vegetables`

These variables take values:
- `True` = row corresponds to this product category  
- `False` otherwise


---
## 1. Data Collection

To conduct a meaningful analysis of food price dynamics, it is essential to work with complete, long-term, and trustworthy datasets.  
For this project, I gathered publicly available **monthly CPI (Consumer Price Index)** data for Kyrgyzstan, focusing on staple food categories.  
The primary dataset covers more than two decades (2003–2024) and was obtained from the **National Statistical Committee of the Kyrgyz Republic**, ensuring reliability and consistency of the measurements.  

Additionally, auxiliary macroeconomic indicators such as inflation context, household income trends, and external market pressures were considered to better interpret the price fluctuations observed in consumer food categories.

---

### 🔹 Main Dataset

- **Source**: *Stat GOV / Real Estate Websites*  
- https://stat.gov.kg/en/
- **Filename**: `cpi_full_dataset.csv`  
- **Description**: Forecasting price dynamics for basic food products in Kyrgyzstan: time series analysis of monthly consumer price indices (2003–2025).  
  It includes the following features:


| Column Name | Description |
|------------|-------------|
| `year`     | The calendar year of CPI observation (2003–2024) |
| `month`    | The month of observation (1–12), used for identifying seasonal effects |
| `value`    | The CPI percentage change for the selected product category |
| `category` | The staple food category (e.g., Flour & Grains, Meat, Dairy, Oils & Fats, Fish) |



This dataset provides long-term economic price measurements for essential food categories in Kyrgyzstan,  
which is crucial for studying inflation patterns, identifying seasonal and crisis-driven price fluctuations,  
and developing accurate forecasting models for food price dynamics.
---


### **3. Data Analysis**

#### **Descriptive Statistics**
- **CPI Value**: Mean ≈ 100.74, Std. Dev. ≈ 4.82, Min = 66.6, Max = 132.0.
- **Year**: Range = 2003–2025 (22 years of temporal coverage).
- **Monthly Distribution**: All categories include 12 monthly observations per year.
- **Categories**: 8 food product groups encoded in one-hot format.

> The majority of CPI values are concentrated in the interval **98–102**, indicating moderate and stable price levels with occasional fluctuations.

---

#### **Category-Level Patterns**
- **Stable pricing behavior:**
  - `milk_egg_cheese`, `bread`, `meat`
  - exhibit gradual upward trends with low short-term variation
  
- **Seasonal behaviors:**
  - `fruits`, `vegetables`  
  - strong recurring seasonal fluctuations
  
- **Moderate volatility:**
  - `fish`, `soft_drinks`, `sugar_chocolate`  
  - occasional peaks and drops but without long-term irregularity

> Category separation reveals that different food groups are influenced by different seasonal and market forces.

---

#### **Correlation Analysis**

- Positive long-term relationship:
  - **Value** and **Year** → increasing CPI value over time due to inflation
  
- Strong short-term dependence:
  - **Value** and **Previous Month Value**
    → strong autocorrelation

- Seasonal circular features:
  - `month_sin` and `month_cos`
    → enable capture of annual cyclical patterns

> The correlation heatmap confirms that **temporal features (year, previous value)** and **seasonality encodings** play critical roles in modeling price evolution.

---

###  Temporal Trends
- CPI shows **consistent inflation trend** over 22 years.
- Seasonal dips are visible for plant-based categories during harvest seasons.
- Macroeconomic events contribute to short-term spikes (e.g., supply disruptions, inflation shocks).

---

###  Regression & Predictive Modeling Insights
Models incorporating:
- `year`,  
- `time_index`,  
- `previous_month_value`,  
- `month_sin`, `month_cos`,  
- and categorical one-hot encoding  

can effectively **predict future CPI values** and capture:
- both short-term month-to-month continuity  
- and long-term inflation movement  

---

###  Interpretation

- CPI values demonstrate **long-term upward movement**, reflecting inflationary pressures.
- Seasonal price distortions primarily occur in **vegetables and fruits**.
- Some categories remain almost unaffected by seasonality (**bread, dairy**), exhibiting stable pricing.
- Category separation dramatically improves model performance in forecasting.

> The analysis confirms that CPI is influenced by both global inflationary trends and category-specific seasonal effects.

---

###  Goal

To model and forecast consumer price changes accurately based on historical time-series trends and category-specific patterns.

---

###  Problem that this project helps to solve

1. **For Economists & Analysts**:  
   - Enables tracking of inflation trends over time  
   - Helps detect anomalies and economic shifts  

2. **For Government and Policy Makers**:  
   - Informs decisions for price regulation and subsidy planning  
   - Supports food-security and cost-of-living monitoring  

3. **For Businesses (Retail & Wholesale)**:  
   - Helps forecast price changes for procurement and warehousing  
   - Enables strategic buying/selling timing  

4. **For Researchers & Academia**:  
   - Provides a structured dataset for studying macroeconomic price behavior  
   - Supports time-series and forecasting research  

---

By analyzing CPI behavior across time and category, the project offers valuable insights into food pricing dynamics, inflation modeling, and economic stability assessment in Kyrgyzstan.


### **4. Visualizations**

1. **Line Plot – CPI Dynamics by Category (2003–2025)**  
   A multi-line chart showing how CPI changes over time for each food category.  
   This visualization highlights long-term inflation trends and differences in behavior between categories such as meat, bread, dairy, fruits, vegetables, etc.


2. **Boxplots – CPI Volatility by Category**  
   Boxplots illustrate the distribution of CPI values for each product group.  
   They reveal which categories are more volatile (e.g., vegetables and fruits with wider boxes and many outliers) and which are more stable (e.g., bread, dairy).


3. **Envelope Plot – CPI Range Across Categories Over Time**  
   A combined chart where the maximum and minimum CPI across all categories are plotted for each year, forming an “envelope” around the category lines.  
   This helps visualize how the overall spread between the cheapest and most expensive product categories evolves over time.


4. **CPI vs Presidential Terms (Annotated Line Chart)**  
   A line plot of average annual CPI overlaid with colored bands representing different presidential terms in Kyrgyzstan.  
   This visualization links macroeconomic price dynamics with political periods, helping to visually associate changes in CPI with shifts in government.


5. **Seasonality Heatmap – CPI by Month and Year**  
   A heatmap with years on the Y-axis and months on the X-axis, where each cell shows the average CPI value.  
   It clearly reveals seasonal patterns, such as mid-year dips or end-of-year increases, and how these patterns change over different years.


6. **Histogram – Distribution of CPI Values**  
   A histogram of all CPI observations that shows a strong concentration of values around the base level (≈100).  
   This confirms that most price changes are moderate, with relatively few extreme values.

Each visualization provides a different perspective on CPI behavior:  
from long-term trends and political context to category-specific volatility and seasonal effects, together giving a comprehensive understanding of price dynamics in Kyrgyzstan.


### **5. Conclusion**

This analysis reveals the main drivers of CPI variation in Kyrgyzstan’s food economy. Long-term inflation trends are clearly visible across all product categories, with certain groups such as fruits and vegetables exhibiting strong seasonal patterns, while staples like bread and dairy remain relatively stable. Temporal features, including previous month price and year index, proved to be highly predictive for modeling future CPI levels. The insights gained from this analysis can support policymakers, economists, and retailers in understanding price dynamics, forecasting inflation, and making informed decisions related to food pricing and market stability in Kyrgyzstan.

---

### **6. References**

1. Dataset: Publicly available real estate listings from Bishkek.
2. Tools: Python libraries such as Pandas, Matplotlib, Seaborn, and Statsmodels.
3. Additional Resources: Statistical analysis and machine learning documentation.

--- 
