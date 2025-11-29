# 🚲 Yulu Bike Sharing – Hypothesis Testing & EDA

## 📌 Project Overview
This project analyzes **Yulu’s shared electric cycle demand** using **exploratory data analysis (EDA)** and **hypothesis testing**.  
The goal is to understand which factors (season, weather, working day, etc.) significantly impact the **number of rentals (`count`)** and how they relate to each other.

---

## 🎯 Business Objective
Yulu wants to know:

1. **Which variables significantly affect the demand** for shared electric cycles.
2. **How well these variables explain the variation in demand**.

This project focuses on:
- Working day vs non-working day impact  
- Seasonal and weather impact on rentals  
- Relationship between season and weather

---

## 🗂 Dataset Description

- **Rows:** 10,886  
- **Columns:** 12 (original), with additional engineered categorical bins  
- **Granularity:** Hourly rental data  
- **Period Covered:** 2011-01-01 00:00:00 to 2012-12-19 23:00:00  

### Main Columns

| Column       | Description                                                                            |
|-------------|----------------------------------------------------------------------------------------|
| `datetime`  | Date & time of observation (hourly)                                                    |
| `season`    | Season (1: Spring, 2: Summer, 3: Fall, 4: Winter)                                      |
| `holiday`   | 1 if day is a holiday, else 0                                                          |
| `workingday`| 1 if day is a working day (not weekend/holiday), else 0                                |
| `weather`   | 1–4, from clear to heavy rain/snow                                                     |
| `temp`      | Temperature in °C                                                                      |
| `atemp`     | “Feels like” temperature in °C                                                         |
| `humidity`  | Humidity (%)                                                                           |
| `windspeed` | Wind speed                                                                            |
| `casual`    | Number of casual (non-registered) users                                                |
| `registered`| Number of registered users                                                             |
| `count`     | Total rentals (`casual + registered`)                                                  |

🔹 No missing values were found in the core dataset.  
🔹 Additional binned categorical features were created:

- `wind_bins` → windspeed ranges (low, medium, high…)  
- `temp_bins` → temperature ranges (very low, normal, high…)  
- `humidity_bins` → humidity ranges (low, good, high, very high)

---

## 🔍 EDA Highlights

- **Seasonal trends:** Rentals highest in **fall**, followed by **summer** and **winter**; spring has comparatively lower demand.
- **Weather:**  
  - Clear weather → **highest rentals**  
  - Mist → moderate rentals  
  - Light snow → low rentals  
  - Heavy rain → almost **no rentals**
- **Holidays vs non-holidays:**  
  - Total rentals are much higher on non-holidays (more days), but averages are comparable.
- **Working days vs non-working days:**  
  - Total rentals on working days are ~2x non-working days, but **average demand per hour is similar**.
- **Comfort ranges for demand:**  
  - Temperature: **10–30°C** (normal temp bin) → highest rentals  
  - Windspeed: **0–20 units** → highest rentals  
  - Humidity: **30–80%** → highest rentals
- **Outliers:**  
  - Some high outliers in `windspeed`; **temp, atemp, humidity** are relatively well-behaved.
- **Correlation:**  
  - `temp` and `atemp` are **strongly positively correlated** (~0.98).

---

## 🧪 Hypothesis Testing

### 1️⃣ Working Day Effect – 2-Sample t-Test

- **H₀:** Mean rentals on working days = mean rentals on non-working days  
- **H₁:** Mean rentals on working days ≠ mean rentals on non-working days  

Using **independent 2-sample t-test**:

- **p-value ≈ 0.226** (> 0.05)  
✅ **Fail to reject H₀** → No statistically significant difference in *average* rentals between working and non-working days.

---

### 2️⃣ Holiday Effect – 2-Sample t-Test (additional)

- **H₀:** Mean rentals on holidays = mean rentals on non-holidays  
- **H₁:** Mean rentals on holidays ≠ mean rentals on non-holidays  

Result:

- **p-value ≈ 0.574** (> 0.05)  
✅ **Fail to reject H₀** → Average demand is not significantly different on holidays vs non-holidays.

---

### 3️⃣ Weather Impact – Non-Parametric Test (Kruskal–Wallis)

Normality and equal variance assumptions for ANOVA **do not hold** for `weather` groups, so a **Kruskal–Wallis test** is used.

- **H₀:** Median rentals are the same across all weather categories  
- **H₁:** At least one weather category has a different median rental count  

Result:

- **p-value ≈ 3.5e-44** (< 0.05)  
❌ Reject H₀ → **Weather has a significant impact on rentals.**

---

### 4️⃣ Season Impact – Non-Parametric Test (Kruskal–Wallis)

Again, ANOVA assumptions fail for `season`, so use Kruskal–Wallis.

- **H₀:** Median rentals are the same across seasons  
- **H₁:** At least one season has a different median rental count  

Result:

- **p-value ≈ 2.48e-151** (< 0.05)  
❌ Reject H₀ → **Season significantly affects rentals.**

---

### 5️⃣ Relationship Between Season & Weather – Chi-Square Test

- **H₀:** Season and weather are independent  
- **H₁:** Season and weather are dependent  

Performed Chi-square test on a contingency table (`season` × `weather`), excluding rare weather category 4 to avoid sparsity.

- **p-value < 0.05**  
❌ Reject H₀ → **Season and weather are dependent** (not independent).

---

## 💡 Key Business Insights

1. **Working days vs non-working days:**  
   - Average demand is **similar**, so **cycle availability can be kept consistent** across both.
2. **Holidays:**  
   - No major change in average demand → **no need for drastic inventory changes** on holidays.
3. **Weather:**  
   - **Clear weather:** Stock **more cycles**.  
   - **Misty conditions:** Keep **moderate inventory**.  
   - **Heavy rain:** Demand drops sharply → **minimal cycles** needed.
4. **Season:**  
   - **Summer, fall, winter:** Higher demand → **stock more cycles**.  
   - **Spring:** Slightly lower demand → **inventory can be reduced** a bit.
5. **Comfort conditions:**  
   - Highest demand when **temp = 10–30°C**, **windspeed = 0–20**, **humidity = 30–80%**.  
   - These conditions can guide **demand forecasting** and **dynamic pricing/inventory planning**.

---

## 🛠 Tech Stack

- Python  
- Pandas, NumPy  
- Seaborn, Matplotlib  
- SciPy (`ttest_ind`, `shapiro`, `levene`, `kruskal`, `chi2_contingency`)

---

## ✅ Outcome

This project demonstrates how **EDA + hypothesis testing** can be used to:

- Quantify the impact of **season**, **weather**, and **calendar effects** on demand  
- Validate or reject assumptions using statistical tests  
- Provide **clear, data-backed recommendations** for inventory planning and operations for a micro-mobility platform like Yulu.

