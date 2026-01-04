#Singapore Population Ageing (1957–2023) — Data Science + Power BI Portfolio

An end-to-end **Data Science + Analytics Engineering** project that transforms official resident population data into **validated insights + forecasts** for ageing-related planning. Delivered as an **interactive Power BI dashboard** with statistical inference and time-series forecasting.

---

## 🧠 Project Overview

This project covers the full Data Science lifecycle:

- 📥 **Data Collection & Understanding**
- 🧹 **Data Cleaning / Preprocessing**
- 🔎 **Exploratory Data Analysis (EDA)**
- 🧩 **Feature Engineering**
- 🧠 **Statistical Inference / Hypothesis Testing**
- 🔮 **Time-Series Forecasting**
- ✅ **Model Validation (Time-aware CV)**
- 📊 **Data Visualization + Storytelling**
- 🧱 **Analytics Engineering (Power BI modeling + DAX)**
- 💼 **Business Insights + Recommendations**

---

## 📦 Dataset

**Singapore Residents by Age Group, Ethnic Group, and Gender (1957–2023)**  
Grain: **Year × Age Band × Gender × Ethnicity**

<img width="1898" height="689" alt="image" src="https://github.com/user-attachments/assets/c12aaeba-1781-4005-b6ee-ba09fb8dfb95" />


---

## 🧹 Data Cleaning & Preprocessing (Data Wrangling)

### What I did
- 🧽 Removed noisy headers/footers and standardized column headers
- 🔁 Replaced `"na"` with blanks (**preserved true missingness; avoided treating missing as zero**)
- 🔃 Reshaped data into **tidy format** (analytics-ready)
- ✅ Created curated tables:
  - **All Ethnic & Gender** (detailed 5-year age bands)
  - **All Gender & Ethnic 65+** (official elderly totals)

<img width="1115" height="583" alt="image" src="https://github.com/user-attachments/assets/73e720f2-99ee-48a2-a02c-5fed5ee36ba4" />


---

## 📊 Power BI Data Modeling + Power Query (EDA-friendly structure)

### Power Query Transformations
- **Unpivoted** year columns (wide → long format) so each row becomes:  
  **Year × Ethnic × Gender × AgeGroup → Population**
- Created helper numeric column **AgeStart** and mapped to policy-friendly buckets:
  - 0–14 (Youth)
  - 15–64 (Working Age)
  - 65+ (Elderly)

<img width="1907" height="903" alt="image" src="https://github.com/user-attachments/assets/b70e2d99-5238-46df-9a6c-50081bef4bf3" />


### Star Schema (Clean filtering + no leakage)
- Dimension: **Years** (Date table created/managed using **Bravo**)
- Facts:
  - All Ethnic & Gender
  - All Gender & Ethnic 65+
- Relationship:
  - Years[Year] → Fact[Year] (1:* single-direction)

✅ Single Year slicer filters everything correctly; avoids many-to-many issues.

<img width="1918" height="1034" alt="image" src="https://github.com/user-attachments/assets/8786b834-ba97-4f66-b7d4-6b27706447e1" />


---

## 🔎 Exploratory Data Analysis (EDA)

### EDA questions answered
- 📈 How is the **elderly share (65+)** changing over time?
- 📉 How is the **youth share (0–14)** trending?

<img width="1322" height="724" alt="image" src="https://github.com/user-attachments/assets/d099a54a-2dbb-4d09-afab-0d82a507598a" />


- 👩‍🦳👨‍🦳 How do patterns differ by **gender**?
- 🧬 How do patterns differ across **ethnic groups**?

<img width="1319" height="727" alt="image" src="https://github.com/user-attachments/assets/ad58047a-364b-4055-9135-60f068a5cdfc" />


---

## 🧩 Feature Engineering (KPI Engineering)

Built interpretable demographic features used in dashboards and models:

- 👵 **Elderly Share (65+)**
- 👶 **Youth Share (0–14)**
- 🧑‍💼 **Working-age Share (15–64)**
- 📈 **Ageing Index (AI)**
- 🧾 **Old-Age Dependency Ratio (OADR)**

<img width="1316" height="718" alt="image" src="https://github.com/user-attachments/assets/ef3d3a77-afef-4f58-9043-4c89b810f564" />


---

## 🧱 Analytics Engineering (Power BI Modeling + DAX)

### The real data challenge solved
Early decades had missing elderly sub-bands (e.g., 75–79, 80–84…), but an official **65+ total** existed.  
If we sum sub-bands, early-year elderly totals become wrong → KPIs break.

### Solution implemented
- ✅ Two-table fact design (detailed table + official 65+ totals table)
- ✅ Reliable **star schema**
- ✅ DAX measures to return correct values under filters (Year / Gender / Ethnicity)

---

## 🧪 Statistical Inference (Hypothesis Testing)

Validated demographic claims using statistical testing on population shares:

### ✅ H1: Elderly share increased over time
- OLS regression: **R² = 0.893**, slope **+0.0021/year**, **p < 0.001**

### ✅ H2: Ageing differs by ethnicity
- ANOVA: **F = 101.59**, **p < 0.001**

### ✅ H3: Youth share declined over time
- OLS regression: **R² = 0.921**, slope **−0.0052/year**, **p < 0.001**

### ✅ H4: Females dominate advanced elderly (75+)
- Welch t-test: **t = 3.25**, **p = 0.0018**
- Female mean (75+) > Male mean (75+)

---

## 🔮 Time-Series Forecasting (Predictive Analytics)

### Goal
Forecast **elderly share (65+)** and estimate when Singapore crosses **25% elderly** (super-aged threshold).

### Models compared
- ✅ ETS (Holt–Winters)
- ARIMA(1,1,1)
- Moving average baseline
- MLP lag model (robustness check)

### Model validation (time-aware)
- ✅ **Rolling-origin / TimeSeriesSplit cross-validation** (prevents leakage)

### Best model
- ✅ ETS performed best:
  - RMSE ≈ **0.010**
  - MAPE ≈ **~6%**
  - R² ≈ **~0.91**

### Planning insight
- ETS forecast for 2035 elderly share ≈ **25.3%**
- 95% interval ≈ **[25.1%, 25.5%]**
- ➡️ Forecast interval fully above 25% → likely **super-aged by ~2035**

Actual vs Prediction plot:
<img width="870" height="512" alt="image" src="https://github.com/user-attachments/assets/edafceac-7998-4598-92cf-59452e207024" />
<img width="903" height="539" alt="image" src="https://github.com/user-attachments/assets/0d248204-01eb-47da-aa9f-2cd08d807fa3" />

Forecast Plot (ETS vs ARIMA + 25% threshold) 
<img width="1068" height="615" alt="image" src="https://github.com/user-attachments/assets/773c2276-4d4a-4210-af7c-ca6b14c230de" />
<img width="1040" height="592" alt="image" src="https://github.com/user-attachments/assets/6b16cb81-4afe-4634-8a46-63b00c9c1639" />

---

## 📊 Visualization + Storytelling

Delivered insights through:
- 🔵 Power BI dashboard (interactive filters + KPI cards)
- 📈 Trend lines, breakdowns by ethnicity and gender
- 🧠 Clear narrative: “what changed, why it matters, what to do next”
<img width="1312" height="715" alt="image" src="https://github.com/user-attachments/assets/54350cc5-8f1b-4eb2-b625-1fc87ae28085" />

<img width="1316" height="718" alt="image" src="https://github.com/user-attachments/assets/33047806-c443-4390-b78c-7d69bbc41adb" />


---

## 💼 Business-Relevant Insights & Recommendations

### Insights
- 📈 Strong long-term ageing trend (statistically confirmed)
- 📉 Youth decline suggests future workforce replenishment pressure
- 🧬 Ethnic differences imply subgroup-specific planning needs
- 👩 Higher female share in 75+ implies long-term care demand skew

### Recommendations
- 🏥 Expand chronic + long-term care capacity and workforce
- 👷 Strengthen older-worker retention and reskilling strategies
- 🎯 Target programs by subgroup ageing intensity
- 📊 Maintain governance on missing values (never convert NA → 0 blindly)

---

## 🧰 Tech Stack

- 🐍 Python (stats + forecasting)
- 📊 Excel (cleaning + preprocessing)
- 🔵 Power BI (modeling + DAX + dashboard)

---

## 📂 Project Files

- 📓 **Forecasting Code (DS Pipeline):** `DSE_Final_Project_Time_Series_Analysis.ipynb`
- 📊 **Power BI Dashboard:** `Singapore Population Analysis - Ganesh.pbix`
- 🗂️ **Raw Dataset (CSV):** `Raw Uncleaned dataset.csv`
- ✅ **Cleaned Dataset (Excel):** `cleaned datasets.xlsx`
- 📄 **Documentation:** `README.md`


---

## ✅ How to Use
1. Clone this repo  
2. Open the `.pbix` in Power BI Desktop  
3. Refresh data (ensure dataset path is correct or place data in the expected folder)  
4. Explore the dashboard using slicers for Year, Gender, and Ethnicity  

---

## 👤 Author
**Ganesh Kumar Marimuthu**  
GitHub: https://github.com/mganesh1610
