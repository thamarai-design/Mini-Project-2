# 🍔 Online Food Delivery Analytics & Decision Support Dashboard

An end-to-end data analytics, SQL warehousing, and business intelligence project analyzing **100,000 online food delivery orders** across major Indian metropolitan cities to uncover revenue drivers, delivery bottlenecks, discount margin impacts, and cancellation root causes.

---

## 📌 Project Overview
This project implements a complete data analytics workflow—from raw dataset auditing and domain-aware preprocessing in Python to relational **SQLite** warehousing, **15 analytical SQL queries**, and an interactive **Streamlit** dashboard (`app.py`) for real-time operational decision-making.

---

## 🛠️ Tech Stack & Tools
- **Data Processing & EDA:** Python (`Pandas`, `NumPy`, `Matplotlib`, `Seaborn`)
- **Database & Querying:** `SQLite` (`food_delivery.db`)
- **Dashboard & Visualization:** `Streamlit`, `Plotly Express`, `LocalTunnel`
- **Documentation:** PowerPoint (`Online_Food_Delivery_Project_Documentation.pptx`)

---

## 🔄 End-to-End Pipeline Architecture
1. **Data Ingestion & Quality Audit:**
   - Profiled **100,000 order records across 25 attributes** spanning temporal, customer demographic, geographic, financial, and fulfillment domains.
   - Identified significant pre-cleaning sparsity (`Final_Amount` 55.70% null, `Customer_Age` 50.09% null, `Distance_km` 33.47% null, `Delivery_Time_Min` 33.36% null) and preserved 100% of records through domain-aware imputation instead of destructive row deletion.
2. **Data Cleaning & Feature Engineering (Pandas):**
   - Imputed skewed numerical fields (`Customer_Age`, `Delivery_Time_Min`, `Distance_km`, `Order_Value`, `Delivery_Rating`) using column medians and filled missing `Discount_Applied` entries with `0`.
   - Reconstructed 55,697 missing `Final_Amount` records via `Order_Value - Discount_Applied`.
   - Standardized missing categorical labels (`Unknown` for City/Area/Gender, `Mixed` for Cuisine, `Cash` for Payment, `None` for Cancellation Reason) and enforced boundary validation (`[1, 5]` rating clipping and `.abs()` checks).
   - Engineered 6 analytical features: `Profit_Amount`, `Profit_Margin_Pct`, `Delivery_Performance_Category`, `Customer_Age_Group`, `Order_Day_Type`, and `Peak_Hour_Indicator`.
3. **Relational Warehousing (SQLite):**
   - Loaded the cleaned dataset into `food_delivery.db` (`food_orders` table) for structured multi-dimensional SQL querying.
4. **SQL Analytics (15 Business Queries):**
   - Executed 15 structured queries across 5 business modules: **Customer & Order Analysis**, **Revenue & Profit Analysis**, **Delivery Performance**, **Restaurant Performance**, and **Operational Insights**.
5. **Interactive BI Dashboard (Streamlit):**
   - Built `app.py` with 4 dynamic sidebar filters (`City`, `Order Month`, `Order Day Type`, `Peak Hour`), 7 executive KPI cards, and 6 interactive Plotly visualizations.

---

## 📊 Key Analytical Findings
- **Platform Scale & Top-Line:** Generated **₹17.09 Crore** across **100,000 orders** with an average final order value of **₹1,708.71**.
- **Seasonality & Weekday Reliance:** Monthly revenue averages **₹14.10M**, peaking in **July (₹14.72M)** and **January (₹14.55M)**. Weekdays drive **71.37%** of total order volume (71,370 orders), signaling strong daily meal dependency.
- **Customer Cohort Economics:** Middle-aged customers (**36–50**) generate **67.6%** of total orders, while Adults (**26–35**) achieve the highest average order value (**₹1,803.05**).
- **Blanket Discount Leakage:** Discounted orders produce a lower final basket size (**₹1,665.71** vs. **₹1,794.58**) and lower unit profit (**₹266.81** vs. **₹270.48**), indicating un-targeted discounting subsidizes smaller carts.
- **Regional & Cuisine Performance:** **Bangalore** leads revenue (**₹28.78M**), followed closely by **Hyderabad (₹28.67M)** and **Delhi (₹28.39M)**. **Italian** cuisine commands the highest profit margin (**15.16%**) and customer rating (**4.21★**).
- **Systemic 2-Hour Delivery Bottleneck:** Mean delivery time sits at **125.0 minutes** across all cities (1.0 km trips average 124.2 min vs. 40.0 km trips at 130.3 min), pointing to kitchen prep or batching delays rather than transit distance.
- **Cancellation Root Causes:** **15.04% of orders (15,036)** were cancelled (~₹25.7M lost GMV), driven by **Late Delivery (20.34%)**, **Customer Cancellation (19.91%)**, and **Restaurant Issues (19.81%)**, alongside **39.94%** unlogged reasons (`None`).

---

## 💡 Strategic Business Recommendations
1. **Fulfillment & Kitchen SLAs:** Cap standard delivery radius at 8–10 km (down from 14.3 km avg) and enforce 15-minute restaurant prep-time SLAs to cut mean delivery times by 35–40%.
2. **Vendor Quality Governance:** Place high-cancellation outliers (`>21.4%` cancellation rate, e.g., `Restaurant_391` & `Restaurant_390`) on performance probation while replicating workflows from `5.0★` top partners.
3. **Precision Discounting:** Replace flat discounts with minimum cart thresholds (e.g., discounts unlocked above ₹1,999) and launch weekday corporate meal passes.
4. **App Telemetry & Digital Checkout:** Enforce mandatory cancellation reason codes in the app UI and incentivize UPI/Wallet payments to reduce the **39.89%** COD/Cash exposure.

---

## 📂 Repository Contents
- `app.py` — Interactive Streamlit & Plotly Business Intelligence dashboard.
- `Online_Food_Delivery_Project_Documentation.pptx` — 10-slide executive presentation covering dataset audit, preprocessing, SQL insights, dashboard architecture, and recommendations.
- `Online_Food_Delivery_Analysis.ipynb` — End-to-end Python, EDA, and SQLite analysis notebook.
- `README.md` — Project documentation and setup guide.

---

## 🚀 How to Run the Dashboard Locally
```bash
# 1. Install required dependencies
pip install pandas numpy matplotlib seaborn streamlit plotly

# 2. Launch the Streamlit application
streamlit run app.py
