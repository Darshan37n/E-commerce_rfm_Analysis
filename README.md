<div align="center">

# 🛒 Customer Segmentation Using RFM Analysis in E-Commerce

**An end-to-end data analysis project applying the RFM framework to segment customers and drive targeted marketing strategies.**

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas)
![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi&logoColor=black)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

</div>

---

## 📌 Problem Statement

E-commerce businesses generate vast amounts of transactional data but often struggle to leverage it for actionable customer segmentation. Understanding purchasing patterns is crucial for predicting behavior, improving retention, reducing churn, and maximizing customer lifetime value. A structured approach is needed to identify high-value customers, detect trends, and optimize targeted marketing strategies.

---

## 🎯 Objectives

- Utilize the **RFM (Recency, Frequency, Monetary)** framework to segment e-commerce customers
- Analyze purchasing patterns to identify high-value customers and at-risk segments
- Apply the **Pareto Principle** to understand revenue and volume concentration
- Create **targeted marketing strategies** for each customer segment to improve retention and satisfaction

---

## 📁 Project Structure

```
ecommerce-rfm-analysis/
│
├── README.md
├── .gitignore
├── requirements.txt
│
├── data/
│   └── README.md                          ← How to download the dataset
│
├── notebooks/
│   └── Ecommerce_Data_Analysis.ipynb      ← Full analysis (cleaning → RFM → segmentation)
│
├── presentation/
│   └── Customer_Segmentation_RFM_Analysis.pptx
│
└── dashboard/
    └── Ecommerce_Dashboard.pbix           ← Interactive Power BI dashboard
```

---

## 📊 Dataset

| Detail | Info |
|---|---|
| **Source** | [Kaggle – E-Commerce Data](https://www.kaggle.com/datasets/carrie1/ecommerce-data) |
| **Raw Size** | 541,909 rows × 8 columns |
| **Timeframe** | 01 Dec 2010 – 09 Dec 2011 |

**Columns:**

| Column | Description |
|---|---|
| `InvoiceNo` | Unique transaction ID (prefix `C` = cancelled order) |
| `StockCode` | Unique product identifier |
| `Description` | Product name/description |
| `Quantity` | Number of units purchased |
| `InvoiceDate` | Date and time of transaction |
| `UnitPrice` | Price per unit in GBP (£) |
| `CustomerID` | Unique customer identifier |
| `Country` | Customer's country of residence |

> ⚠️ The raw dataset is **not included** in this repository. Download it from Kaggle and place it in `data/data.csv`. See [`data/README.md`](data/README.md) for instructions.

---

## 🔧 Tools & Technologies

| Tool | Purpose |
|---|---|
| **Python** | Core analysis and RFM computation |
| **Pandas & NumPy** | Data wrangling and transformation |
| **Matplotlib & Seaborn** | Data visualization |
| **Power BI** | Interactive dashboard |
| **PowerPoint** | Project presentation |

---

## 🚀 Project Workflow

### 1. 🧹 Data Cleaning & Preparation

The raw dataset required significant cleaning before analysis:

| Issue | Action Taken |
|---|---|
| **24.93% missing CustomerIDs** | Dropped — CustomerID is essential for RFM analysis |
| **5,525 duplicate rows** | Removed, keeping first occurrence |
| **8,872 cancelled orders** | Removed rows where `InvoiceNo` starts with `'C'` (negative quantities) |
| **Non-product StockCodes** | Removed entries like `POST`, `C2`, `M`, `DOT`, `BANK CHARGES` |
| **StockCode anomalies** | Kept only codes with length 5–7 characters |
| **Data type fixes** | Converted `InvoiceDate` from string to datetime |

**Final cleaned dataset shape:** ~392,000 rows ready for analysis.

---

### 2. 📈 Exploratory Data Analysis (EDA)

**Time Series Analysis:**
- Plotted **daily and monthly sales trends** over the full 13-month period
- Computed average monthly sales as a benchmark
- Analysed **sales by day of week** — discovered zero sales on Saturdays

**Key Insight:** Sales show a strong upward spike toward **Nov–Dec 2011**, suggesting seasonal demand patterns.

---

### 3. ⚖️ Pareto Principle Analysis

Validated the 80/20 rule across multiple dimensions:

| Dimension | Finding |
|---|---|
| **Customers vs Revenue** | **26%** of customers contribute to **80%** of total revenue |
| **Products vs Revenue** | **21%** of products contribute to **80%** of total revenue |
| **Products vs Volume** | A similar minority of products drive the majority of sales volume |

---

### 4. 📐 RFM Score Calculation

Each customer was scored on three dimensions using **quantile-based binning (1–5 scale)**:

| Metric | Description | Scoring |
|---|---|---|
| **Recency (R)** | Days since last purchase | Lower days = Higher score |
| **Frequency (F)** | Number of unique invoices | Higher count = Higher score |
| **Monetary (M)** | Total spend (Quantity × UnitPrice) | Higher spend = Higher score |

Rank-based scoring was used for Frequency to handle ties correctly. Final `RFM_Score = R + F + M`.

---

### 5. 🧩 Customer Segmentation

Customers were grouped into **4 segments** based on R and F scores:

| Segment | Behaviour | R Score | F Score |
|---|---|---|---|
| 🏆 **High Value** | Recent + very frequent buyers | 5 | 5 |
| 💛 **Loyal** | Consistent, moderately active | ≥ 4 | ≥ 4 |
| ⚠️ **At-Risk** | Declining engagement | ≥ 2 (any) | ≥ 2 (any) |
| 😴 **Dormant** | Inactive, potential churn | 1 | 1 |

An **RFM heatmap** was plotted to visualise average monetary scores across R and F score combinations.

---

### 6. 📣 Marketing Recommendations

| Segment | Strategy |
|---|---|
| 🏆 **High Value** | Loyalty programs, VIP exclusives, early access to new products |
| 💛 **Loyal** | Upsell and cross-sell campaigns to increase basket size |
| ⚠️ **At-Risk** | Personalised emails and limited-time promotions to re-engage |
| 😴 **Dormant** | Win-back campaigns or satisfaction surveys to address churn |

---

### 7. 📊 Customer Retention Analysis (Bonus)

As an extension of the RFM analysis, customers were further classified into:
- **New Customers** — first-time buyers in a given month
- **Returning Customers** — repeat buyers within the active period
- **Churned Customers** — no purchase in the last 90 days

Monthly trends for each type were plotted to track **retention and churn patterns over time**.

---

## ▶️ How to Run

**1. Clone the repository**
```bash
git clone https://github.com/your-username/ecommerce-rfm-analysis.git
cd ecommerce-rfm-analysis
```

**2. Install dependencies**
```bash
pip install -r requirements.txt
```

**3. Add the dataset**

Download `data.csv` from [Kaggle](https://www.kaggle.com/datasets/carrie1/ecommerce-data) and place it in the `data/` folder. Then update the file path in the notebook:

```python
# Change this line in the notebook:
df = pd.read_csv("../data/data.csv", encoding="ISO-8859-1")
```

**4. Run the notebook**
```bash
jupyter notebook notebooks/Ecommerce_Data_Analysis.ipynb
```

**5. View the Dashboard**

Open `dashboard/Ecommerce_Dashboard.pbix` in **Power BI Desktop**.

---

## 📌 Key Takeaways

- A small fraction of customers and products drive the majority of revenue — confirming the **Pareto Principle**
- **RFM segmentation** enables precise, data-driven targeting rather than blanket marketing
- **Dormant and At-Risk customers** represent a significant recovery opportunity with the right re-engagement strategy
- Seasonal sales spikes indicate potential for **inventory and campaign pre-planning** in Q4

---

## 📬 Connect

Feel free to raise an issue or connect if you have questions about the project!
