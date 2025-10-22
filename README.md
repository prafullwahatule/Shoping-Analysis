# 🛍️ Customer Shopping Analysis Dashboard (Power BI)

## 📄 Project Summary
This Power BI project provides a consolidated view of **retail sales performance** across shopping malls, payment methods, and customer segments.  
It helps business analysts and retail managers monitor **revenue, customer behavior**, and **key performance indicators (KPIs)** in one interactive dashboard.

---

## 🎯 Problem Statement
Retail stakeholders need a single dashboard to answer:
- What is the total revenue and how is it distributed across online and offline channels?
- Which payment methods and categories contribute most to revenue?
- How do different malls perform in terms of revenue?
- What are the customer age group distributions and average basket sizes?

Without a unified dashboard, **decision-making for promotions, inventory, and channel strategy** becomes slow and inefficient.

---

## 🎯 Objectives
**Primary Objectives:**
- Display real-time KPIs like Total Revenue, Average Spending, Basket Size, and Channel Split.
- Enable filtering by **Category, Gender, Shopping Mall, and Payment Type**.
- Visualize data by **payment method, customer age group, and monthly revenue trend**.
- Provide actionable insights for **marketing and operations teams**.

---

## 📚 Table of Contents
| Sr. No. | Section Name |
|----------|---------------|
| 1 | Scope |
| 2 | Data Sources |
| 3 | Data Preparation & Cleaning |
| 4 | Dashboard Design & Layout |
| 5 | Metrics, Measures & Calculations |
| 6 | Filters and Interactions |
| 7 | Visualizations (page-wise) |
| 8 | Key Insights & Findings |
| 9 | Recommendations |
| 10 | Limitations |
| 11 | Future Work |
| 12 | Appendix: Data Dictionary & Files |
| 13 | Dashboard Screenshot |
| 14 | Appendix: Data Transformation Summary |
| 15 | Data Transformation & Wrangling |
| 16 | Data Cleaning Process |
| 17 | Storytelling, KPIs & Charts |
| 18 | Visuals / Charts |
| 19 | Filters / Slicers |
| 20 | Conclusion |

---

## 📘 Scope
### ✅ In Scope:
- Power BI dashboard with 1 main page (Shopping Report).
- Data ingestion and cleaning using **Power Query**.
- Visual KPIs, slicers, and charts for sales and customer insights.

### ❌ Out of Scope:
- Real-time streaming connectors.
- Data write-back to transactional systems.

---

## 🗂️ Data Sources
**Primary Source:**
- `customer_shopping_data.csv` — Transactional dataset containing:
  - Date, Total Amount, Payment Type, Shopping Mall, Category, Gender, Age, Quantity, Item, etc.

**Optional Master Data:**
- Product Catalog  
- Mall Metadata  
- Payment Method Lookup  

---

## 🧹 Data Preparation & Cleaning
Steps performed in **Power Query**:
1. Imported transactional CSV file.
2. Parsed date fields → added Year, Month, MonthNumber.
3. Standardized text fields using `Trim` and `Clean`.
4. Handled missing values → filled Gender as ‘Unknown’.
5. Created new columns:
   - **Age Group** = Teen / Youth / Adult / Senior  
   - **Basket Size** = Quantity per transaction
6. Created relationships between tables using key fields.

---

## 🎨 Dashboard Design & Layout
- **Theme:** Dark theme with high-contrast KPI cards.  
- **Layout:**
  - **Top Row:** KPIs – Total Revenue, Avg Spending, Basket Size, Online % & Offline %.
  - **Middle/Bottom Rows:** Visuals (donut, bar, line charts).
- **Left Panel:** Filters for dynamic data exploration.

---

## ⚙️ Metrics, Measures & Calculations (DAX)
| Sr. No. | Measure | DAX Formula | Description |
|----------|----------|-------------|--------------|
| 1 | **Total Revenue** | `SUM('Shopping_Data'[Total Amount])` | Total sales amount. |
| 2 | **Average Spending** | `DIVIDE([Total Revenue], DISTINCTCOUNT('Shopping_Data'[CustomerID]))` | Avg spend per customer. |
| 3 | **Average Basket Size** | `AVERAGE('Shopping_Data'[Quantity])` | Avg quantity per transaction. |
| 4 | **Online Sales %** | `DIVIDE(SUMX(FILTER('Shopping_Data', 'Shopping_Data'[Payment Type Category]="Online"), 'Shopping_Data'[Total Amount]), [Total Revenue])*100` | % revenue from online payments. |
| 5 | **Offline Sales %** | `100 - [Online Sales %]` | % revenue from offline (cash) payments. |

---

## 🎛️ Filters & Interactions
**Filters Available:**
- Category  
- Gender  
- Shopping Mall  
- Payment Type Category  

**Interactions:**
- Click charts → filter other visuals (cross-filter).  
- Select a month → update all KPIs and charts dynamically.

---

## 📊 Visuals & Charts
| Sr. No. | Chart Name | Columns Used | Visual Type | Purpose |
|----------|-------------|--------------|-------------|----------|
| 1 | Total Revenue by Mall | Shopping Mall, Total Amount | Column Chart | Identify top-performing malls. |
| 2 | Revenue by Category | Category, Total Amount | Donut / Pie Chart | Show revenue share by product category. |
| 3 | Age Group Distribution | Age Group, Customer ID | Bar Chart | Understand customer demographics. |
| 4 | Online vs Offline Sales % | Payment Type Category, Total Amount | Donut / Pie Chart | Compare online vs offline sales. |
| 5 | Monthly Revenue Trend | Invoice Date, Total Amount | Line Chart | Observe month-wise revenue trend. |
| 6 | Payment Method Analysis | Payment Method, Total Amount | Column Chart | Analyze preferred payment types. |

---

## 🔍 Key Insights & Findings
- Online channel contributes **~55% of total revenue** → invest in online promotions.  
- **Top categories:** Clothing & Shoes → prioritize inventory here.  
- Certain malls outperform others → explore store-level merchandising.  
- Revenue peaks in **January** → possible seasonal demand or campaigns.

---

## 💡 Recommendations
- Increase marketing budget for high-performing channels/categories.  
- Run campaigns for underperforming malls or months.  
- Improve **online payment UX** to boost conversions.  
- Integrate **customer demographics** for deeper segmentation analysis.

---

## ⚠️ Limitations
- Data accuracy depends on source completeness.  
- Age Group derived → possible inaccuracies if missing values exist.  
- Dashboard aggregates → no drill-down at store or product level.

---

## 🚀 Future Work
- Add drill-through pages (Customer or Product details).  
- Integrate **scheduled refresh / real-time streaming**.  
- Apply **forecasting & predictive analytics (Python/R)**.  
- Enable **role-based access** for analysts vs managers.

---

## 📑 Appendix: Data Dictionary (Sample)
| Column Name | Description |
|--------------|-------------|
| Invoice No | Unique transaction identifier |
| Customer ID | Unique ID per customer |
| Gender | Customer gender |
| Age | Age of customer |
| Category | Product category purchased |
| Quantity | Number of items per transaction |
| Price | Unit price per item |
| Payment Method | Cash, Credit Card, Debit Card |
| Payment Type Category | Online or Offline |
| Shopping Mall | Mall where purchase occurred |
| Total Amount | Quantity × Price |
| Age Group | Teen / Youth / Adult / Senior |

---

## 🧮 Data Cleaning Summary
| Step | Action | Result |
|------|---------|--------|
| 1 | Removed duplicates & blanks | 99,457 rows retained |
| 2 | Cleaned text & standardized columns | Improved consistency |
| 3 | Added new columns | Increased from 10 → 14 columns |
| 4 | Derived KPIs | Ready for visualization |

---

## 🧠 Storytelling: KPIs & Insights
- **KPIs Used:** Total Revenue, Avg Spending, Basket Size, Online %, Offline %.  
- **Purpose:** To monitor financial and behavioral trends interactively.  
- **Visualization Goal:** Help stakeholders understand “what drives revenue” at a glance.

---

## 🧩 Files Included
- `customer_shopping_data.csv`  
- `Shopping Analysis Dashboard.pbix`  
- `Shopping Analysis Report.xlsx`  
- `Shopping_Analysis_Documentation.docx`

---

## 🖼️ Dashboard Screenshot
![Uploading Screenshot 2025-10-21 224608.png…]()


---

## 🏁 Conclusion
This Power BI dashboard enables **data-driven retail decision-making** by consolidating customer, product, and transaction insights in one place.  
It showcases how **clean data, clear KPIs, and interactive visuals** can reveal meaningful business stories and support better strategic planning.

---

## 👨‍💻 Author
**Prafull Wahatule**  
📧 [prafull816@gmail.com]  
💼 [GitHub: prafull816](https://github.com/prafull816)
