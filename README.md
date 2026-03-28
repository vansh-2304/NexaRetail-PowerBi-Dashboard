# NexaRetail Global Business Performance Dashboard

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

> **A 5-page enterprise analytics dashboard built in Power BI Desktop**  
> Global Superstore Dataset · 51,290 Orders · 147 Countries · 4-Year Trend Analysis

---

## Business Problem

Retail executives need a single source of truth to monitor revenue health, regional performance, product profitability, and customer behaviour — without switching between multiple reports. This dashboard consolidates all critical KPIs into an interactive 5-page Power BI report that enables fast, data-driven decision making at every level of the organisation.

---

## Dashboard Pages

| # | Page | Purpose |
|---|------|---------|
| 1 | **Executive Overview** | Top-level KPIs, revenue trend, regional breakdown, world map, and category split |
| 2 | **Regional Performance** | Region and year slicers, monthly column chart, country table, filled map, YoY bar chart |
| 3 | **Product Analysis** | Treemap, scatter plot, stacked bar, top 10 products table with drill-through |
| 4 | **Customer Insights** | Segment donut, customer growth, top 10 customers table, customer location map |
| 5 | **Trend & Forecast** | 6-month revenue forecast, YoY comparison, waterfall chart, area chart |

> Two additional hidden pages power advanced features:
> - **Product Detail (Drill-Through)** — Right-click any product on Page 3 to navigate here
> - **Tooltip - Region** — Hover over any country on the map for an instant KPI popup

---

## Key Insights Discovered

1. **APAC showed the highest revenue growth YoY (+18%) but the lowest profit margin** — the aggressive discount strategy was buying revenue at the cost of profitability, signalling a pricing strategy review is needed.

2. **Technology drives the highest revenue share (37.59%) but Office Supplies has the most consistent margin** — suggesting a portfolio rebalancing opportunity to protect overall profitability.

3. **The Central region consistently outperforms all other regions in revenue (0.94M)** — while EMEA and LATAM remain significantly under-indexed, representing the largest untapped growth opportunity.

---

## Data Model

Star schema with 4 tables:

```
DateTable (Dimension)
    │
    ├──── orders_cleaned (Fact Table) ────── returns (Dimension)
                                       └──── people (Dimension)
```

| Table | Type | Rows | Description |
|-------|------|------|-------------|
| `orders_cleaned` | Fact | 51,290 | Core transaction data — orders, sales, profit, shipping |
| `DateTable` | Dimension | 5,479 | DAX-generated calendar (2011–2025) with Year, Month, Quarter columns |
| `returns` | Dimension | 1,173 | Returned order IDs linked to orders_cleaned |
| `people` | Dimension | 24 | Regional manager names linked by Region |

---

## DAX Measures (15 Total)

### Core Metrics
| Measure | Formula Summary |
|---------|----------------|
| `Total Revenue` | SUM of Sales column |
| `Total Profit` | SUM of Profit column |
| `Gross Margin %` | Total Profit ÷ Total Revenue |
| `Total Orders` | DISTINCTCOUNT of Order ID |
| `Total Customers` | DISTINCTCOUNT of Customer ID |
| `Average Order Value` | Total Revenue ÷ Total Orders |
| `Return Rate` | COUNT of returns ÷ Total Orders |
| `Revenue Per Customer` | Total Revenue ÷ Total Customers |

### Time Intelligence
| Measure | Formula Summary |
|---------|----------------|
| `Revenue YTD` | TOTALYTD on Total Revenue |
| `Revenue MTD` | TOTALMTD on Total Revenue |
| `Revenue Last Year` | CALCULATE with SAMEPERIODLASTYEAR |
| `Revenue YoY %` | (This Year − Last Year) ÷ Last Year |
| `Profit YoY %` | Same pattern applied to Total Profit |

---

## Tools & Technologies
- **Power BI Desktop** — Report building, data modelling, DAX
- **DAX** — 15 custom measures including time intelligence
- **Microsoft Excel / Power Query** — Data cleaning and transformation
- **Dataset** — Global Superstore (Kaggle) — 51,290 orders across 147 countries

---

## Advanced Features

- **Drill-Through Navigation** — Right-click any sub-category on the Product Analysis page to jump to a detailed product breakdown page
- **Custom Tooltip** — Hover over any country bubble on the world map to see a mini KPI popup showing Revenue, Gross Margin %, and Revenue by Category for that country
- **Synced Slicers** — Year slicer on Page 1 filters all 5 pages simultaneously
- **Conditional Formatting** — Gross Margin % KPI card turns green (>40%), orange (30–40%), or red (<30%) automatically
- **6-Month Forecast** — Built-in Power BI forecast with 95% confidence interval on the Trend page

---

## Project Structure

```
nexaretail-dashboard/
│
├── data/
│   ├── raw/                    ← Original downloaded files (never edited)
│   └── cleaned/
│       ├── orders_cleaned.csv
│       ├── returns.csv
│       └── people.csv
│
├── dashboard/
│   └── NexaRetail-Dashboard.pbix
│
├── screenshots/
│   ├── 01_executive_overview.png
│   ├── 02_regional_performance.png
│   ├── 03_product_analysis.png
│   ├── 04_customer_insights.png
│   ├── 05_trend_forecast.png
│   ├── 06_data_model.png
│   └── 07_drill_through_demo.png
│
├── docs/
│   └── data_dictionary.md
│
└── README.md
```

---

## How to Use This Dashboard

1. Download and open `NexaRetail-Dashboard.pbix` in **Power BI Desktop** (free)
2. Use the **Year slicer** on any page to filter the entire report by year
3. On **Page 2**, use the Region slicer to isolate a specific market
4. On **Page 3**, right-click any product bar → **Drill through → Product Detail** for a deep dive
5. On **Page 1**, hover over any country on the map for an instant regional KPI tooltip

---

## Dataset Source

**Global Superstore Dataset** — available on [Kaggle](https://www.kaggle.com/)  
Original data: 51,290 orders · 10,000+ customers · 2011–2014 · 147 countries · 3 product categories

---

## Connect

Built as a portfolio project to demonstrate end-to-end Power BI development including data modelling, DAX, and enterprise dashboard design.

> Open to **Data Analyst** and **Business Intelligence** roles.  
