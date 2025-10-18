# 🛍️ Vendor Performance Analysis (Olist Brazilian E-Commerce Dataset)

## 📖 Overview
This project analyzes **vendor (seller) performance** within the **Olist Brazilian e-commerce marketplace dataset**.  
The primary goal is to identify **key factors driving sales, profitability, and efficiency**, providing actionable insights for **BrazilMart** (the hypothetical marketplace owner) to optimize vendor relationships and overall platform performance.

---

## 📦 Dataset
The analysis uses the **Olist Brazilian E-commerce dataset** (publicly available on [Kaggle](https://www.kaggle.com/olistbr/brazilian-ecommerce)), which includes **9 interrelated CSV files** containing information about:
- Orders  
- Customers  
- Sellers  
- Products  
- Payments  
- Reviews  
- Geolocation  

---

## ⚙️ Methodology

### 1. **ETL Process**
- Automated **Python ETL pipeline** built using **Pandas** and **SQLAlchemy**.  
- Extracted all 9 CSV files and loaded them into a centralized **SQLite database (`brazil_ecommerce.db`)**.  
- Implemented **logging** for monitoring and error handling.

### 2. **SQL Aggregation**
- Connected to SQLite and executed complex **INNER JOIN** operations on `order_items` and `products` tables.  
- Aggregated data using `SUM` and `COUNT`, grouped by:
  - `seller_id`
  - `product_id`
  - `product_category_name`  
- Created a consolidated **master analysis table (`master_df`)**.

### 3. **Exploratory Data Analysis (EDA) & Feature Engineering**
- Handled missing values (`NaN`) in `product_category_name` by dropping affected rows.  
- Engineered new key features:
  - `net_revenue` = `sales - freight`
  - `profit_margin` = `net_revenue / sales`
  - `unit_price` = `sales / quantity`
- Filtered dataset for **profitable sales (`net_revenue > 0`)** and **reasonable prices (< $2000)** to create `analysis_df`.

### 4. **Quadrant Analysis (Strategic Segmentation)**
- Calculated **median sales** and **profit margin** to define thresholds.  
- Classified products into four strategic categories:
  - ⭐ **Star** – High sales, high profit margin  
  - 💰 **Cash Cow** – High sales, low profit margin  
  - 💎 **Question Mark / Hidden Gem** – Low sales, high profit margin  
  - 🐾 **Dog** – Low sales, low profit margin  
- Visualized using a **scatter plot** with quadrant highlights.

### 5. **Targeted Analysis & Visualization**
- Identified **Top 10 vendors by total sales** (bar chart).  
- Analyzed **freight cost vs. profit margin** (scatter plot + regression line).  
- Identified **Bottom 10 vendors** with the lowest average sales quantity per product (bar chart).

### 6. **Statistical Hypothesis Testing (T-test)**
- Compared **profit margins of top 25% sellers** vs. **bottom 25% sellers**.  
- Used **`scipy.stats.ttest_ind`** for independent two-sample **T-test**.  
- Found **statistically significant difference (p < 0.05)** — indicating low-volume sellers often have higher per-item profit margins.

---

## 💡 Key Insights

| Question | Insight |
|-----------|----------|
| **Hidden Gems** | Products with high profit margins but low sales volume identified via Quadrant Analysis. |
| **Superstar Vendors** | Top 10 revenue-generating sellers highlighted. |
| **Freight Cost Impact** | Clear negative correlation between freight cost and profit margin. |
| **Low Sellers** | Bottom 10 vendors with lowest average sales per product identified. |
| **Profit Puzzle** | High-volume sellers aren’t necessarily the most profitable per item — confirmed statistically (p < 0.05). |

---

## 🧰 Technologies Used
- **Python**
- **Pandas**, **NumPy**
- **SQLAlchemy**, **SQLite**
- **Matplotlib**, **Seaborn**
- **SciPy (`stats.ttest_ind`)**
- **Jupyter Notebook**

---

## 📊 Reporting & Dashboard
The final cleaned and enriched dataset (`data_for_dashboard.csv`) was exported for **Power BI visualization**, enabling an **interactive business intelligence dashboard** for stakeholders.

---
├── data/
│   ├── raw/
│   └── processed/
├── notebooks/
│   └── vendor_analysis.ipynb
├── brazil_ecommerce.db
├── data_for_dashboard.csv
├── scripts/
│   └── etl_pipeline.py
└── README.md



---

## 🚀 Future Work
- Integrate **predictive modeling** for vendor performance forecasting.  
- Implement **automated vendor scoring** using machine learning.  
- Expand dashboard interactivity with **real-time metrics** and alerts.

---

## 🧾 Citation
Dataset Source: [Olist Brazilian E-commerce Dataset – Kaggle](https://www.kaggle.com/olistbr/brazilian-ecommerce)  
(cite: 1509, 1515, 1516, 1537, 1551–1802)


## 📁 Repository Structure
