<h1 align="center"> 🚲 Yulu Electric Cycle Demand Analysis  
<h1 align="center"> Hypothesis Testing & Statistical Analysis

---

## 🔍 Problem Background
Yulu, India’s leading micro-mobility platform, has observed a **decline in revenue** and wants to understand the key factors influencing the **demand for shared electric cycles**.

The company is particularly interested in knowing:
- Which variables significantly affect demand
- Whether demand patterns vary across **working days, seasons, and weather conditions**
- How well these factors explain rental behavior in the Indian market

---

## 📌 Case Study Objective
To analyze Yulu’s rental data using **Exploratory Data Analysis (EDA)** and **Hypothesis Testing** in order to:
- Identify statistically significant factors affecting demand
- Validate business assumptions using data
- Provide actionable insights for operational planning

---

## 📎 Project Notebook
🔗 **Google Colab:**  
https://colab.research.google.com/drive/1YBoh1UnQ7FbaViKt3D8CgrY6MRwOa5kH#scrollTo=bxakFiMh8ORm

---

## 🗂 Dataset Overview
The dataset consists of **hourly bike rental data** with demand influenced by environmental and calendar-based factors.

### Key Attributes
- `datetime` – Timestamp (hourly granularity)
- `season` – Season (Spring, Summer, Fall, Winter)
- `holiday` – Whether the day is a holiday
- `workingday` – Working day indicator
- `weather` – Weather category (clear to heavy rain)
- `temp` – Temperature (°C)
- `atemp` – Feels-like temperature (°C)
- `humidity` – Humidity level
- `windspeed` – Wind speed
- `casual` – Casual users count
- `registered` – Registered users count
- `count` – Total rentals (target variable)

✅ No missing values in core columns

---

## 🧪 Analytical Approach

### 1️⃣ Exploratory Data Analysis
- Distribution analysis of continuous variables (temp, humidity, windspeed, count)
- Category-wise comparison for:
  - Working day vs non-working day
  - Weather types
  - Seasons
- Outlier detection and correlation analysis

---

### 2️⃣ Hypothesis Testing Framework

| Business Question | Statistical Test Used |
|-------------------|----------------------|
| Does working day affect demand? | 2-Sample t-Test |
| Is demand different across seasons? | Kruskal–Wallis Test |
| Is demand different across weather conditions? | Kruskal–Wallis Test |
| Are season and weather related? | Chi-Square Test |

---

## 📊 Hypothesis Test Results

### ✅ Working Day vs Non-Working Day
- **Test:** 2-Sample t-Test  
- **Result:** No statistically significant difference in average demand  
- **Inference:** Rentals per hour are similar on working and non-working days

---

### ✅ Holiday vs Non-Holiday
- **Test:** 2-Sample t-Test  
- **Result:** No significant difference  
- **Inference:** Holidays do not drastically impact average demand

---

### ✅ Weather Impact on Demand
- **Test:** Kruskal–Wallis (ANOVA assumptions violated)  
- **Result:** Statistically significant difference  
- **Inference:** Weather strongly affects electric cycle rentals

---

### ✅ Seasonal Impact on Demand
- **Test:** Kruskal–Wallis  
- **Result:** Statistically significant difference  
- **Inference:** Demand varies meaningfully across seasons

---

### ✅ Season vs Weather Dependency
- **Test:** Chi-Square Test of Independence  
- **Result:** Season and weather are dependent  
- **Inference:** Weather patterns change with seasons and should be jointly considered

---

## 💡 Key Insights
- Electric cycle demand is **highly weather-sensitive**
- **Clear weather and moderate temperatures (10–30°C)** drive maximum usage
- **Summer, fall, and winter** see higher rentals than spring
- Working days and holidays do **not** change average demand significantly
- Wind speed and humidity have optimal comfort ranges affecting usage

---

## 🚀 Business Recommendations
- Adjust fleet availability dynamically based on **weather forecasts**
- Increase bike supply during **clear weather and peak seasons**
- Reduce operational costs during heavy rain conditions
- Use season–weather dependency for **better demand forecasting**
- Maintain consistent availability across working and non-working days

---

## 🛠 Tools & Techniques
- Python (Pandas, NumPy)
- Seaborn & Matplotlib
- SciPy (t-test, Kruskal–Wallis, Chi-square)
- Exploratory Data Analysis
- Statistical Hypothesis Testing

---

## ✅ Project Outcome
This case study demonstrates how **statistical hypothesis testing** can convert raw operational data into **business evidence**, enabling Yulu to optimize inventory planning, improve utilization, and support revenue recovery strategies.

---

## 👤 Author
**Nikhil Somisetty**  
📅 June 2025
