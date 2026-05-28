# 🛍️ Canadian Retail Trade Sales Analysis (2017–2026)

An end-to-end data analysis project examining monthly retail trade sales across Canada using open data from **Statistics Canada**. The project covers data cleaning, feature engineering, exploratory data analysis, and interactive Power BI visualization.

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Repository Structure](#repository-structure)
- [Dataset Description](#dataset-description)
- [Project Workflow](#project-workflow)
- [Key Analyses](#key-analyses)
- [Power BI Dashboard](#power-bi-dashboard)
- [Getting Started](#getting-started)
- [Requirements](#requirements)

---

## Project Overview

This project analyzes **monthly retail trade sales** in Canada from January 2017 to February 2026, broken down by:

- **Geography** — National, province, territory, and Census Metropolitan Area (CMA)
- **Industry** — 30 NAICS-based retail subsectors (e.g., Food & Beverage, Auto Dealers, E-Commerce)
- **Adjustment type** — Unadjusted vs. Seasonally Adjusted figures

**Business Goals:**
1. Monitor overall retail industry performance over time
2. Analyze geographic performance across provinces and cities
3. Understand seasonality patterns in retail sales
4. Measure e-commerce growth relative to total retail
5. Support forecasting and business planning

---

## Data Source

| Field | Details |
|-------|---------|
| **Publisher** | Statistics Canada (Government of Canada) |
| **Table** | [20-10-0056-01: Monthly Retail Trade Sales by Province and Territory](https://www150.statcan.gc.ca/t1/tbl1/en/tv.action?pid=2010005601) |
| **Frequency** | Monthly |
| **Coverage** | January 2017 – February 2026 |
| **Classification** | North American Industry Classification System (NAICS) |
| **Units** | Dollars × 1,000 (thousands of CAD) |
| **Direct Download** | [20100056-eng.zip](https://www150.statcan.gc.ca/n1/tbl/csv/20100056-eng.zip) |

---

## Repository Structure

```
├── Dataset/
│   ├── 20100056.csv                  # Raw data from Statistics Canada
│   └── retail_sales_cleaned.csv      # Cleaned & feature-engineered dataset
├── 20100056_MetaData.csv             # Dataset metadata (dimensions, members)
├── Data_cleaning.ipynb               # Data cleaning & feature engineering notebook
├── Data_Analysis.ipynb               # Exploratory data analysis notebook
├── Canadian_Retail_Trade_Sales_Visualization.pbix  # Power BI dashboard
└── README.md
```

---

## Dataset Description

### Cleaned Dataset Columns (`retail_sales_cleaned.csv`)

| Column | Type | Description |
|--------|------|-------------|
| `REF_DATE` | datetime | Reference month (e.g., `2017-01-01`) |
| `Year` | int | Calendar year extracted from `REF_DATE` |
| `Month` | int | Month number (1–12) |
| `Month_Name` | string | Full month name (e.g., January) |
| `Quarter` | int | Fiscal quarter (1–4) |
| `GEO` | string | Geographic area (e.g., Canada, Ontario, Toronto) |
| `Geo_Level` | string | Geographic tier: `National` / `Province` / `Territory` / `City` |
| `Industry` | string | Retail subsector name (NAICS codes stripped) |
| `Sales` | string | Sales type: `Total retail sales` or `Retail e-commerce sales` |
| `Adjustments` | string | `Unadjusted` or `Seasonally adjusted` |
| `VALUE` | int | Sales in thousands of CAD (as published by StatCan) |
| `Sales_Actual` | int | Sales in actual CAD (`VALUE × 1,000`) |

**Shape:** 66,494 rows × 12 columns  
**Geographies:** 23 (Canada + 10 provinces + 3 territories + 9 CMAs)  
**Industries:** 30 NAICS-based subsectors

---

## Project Workflow

### 1. Data Cleaning (`Data_cleaning.ipynb`)

- Loaded raw Statistics Canada CSV (17 columns)
- Inspected for nulls, duplicates, and whitespace issues
- Dropped redundant/internal columns (`DGUID`, `UOM`, `SCALAR_FACTOR`, `VECTOR`, `COORDINATE`, etc.)
- Converted `REF_DATE` from string to datetime
- Extracted time features: `Year`, `Month`, `Month_Name`, `Quarter`
- Stripped NAICS codes from industry names → clean `Industry` column
- Classified geographic entries into `Geo_Level` tiers (National / Province / Territory / City)
- Scaled `VALUE` (thousands) to `Sales_Actual` (actual dollars)
- Exported cleaned dataset to `retail_sales_cleaned.csv`

### 2. Exploratory Data Analysis (`Data_Analysis.ipynb`)

Structured around five business goals with dedicated KPI sections:

- **Section 1 — Sales KPIs:** All-time totals, average monthly sales, peak/trough months, MoM and YoY growth rates
- **Section 2 — Geographic Performance:** Provincial and CMA-level sales comparisons and rankings
- **Section 3 — Seasonality:** Monthly sales patterns, heatmaps, and unadjusted vs. seasonally adjusted comparisons
- **Section 4 — E-Commerce Growth:** E-commerce share of total retail sales over time
- **Section 5 — Industry Breakdown:** Revenue split across 10 top-level NAICS subsectors

---

## Key Analyses

- **National retail sales trend** (2017–2026) — unadjusted and seasonally adjusted
- **Month-over-month and year-over-year growth** rates
- **Seasonal heatmaps** by month and year
- **Provincial benchmarking** — Ontario, Quebec, BC, Alberta, and others
- **E-commerce penetration** tracking across the full period
- **Industry mix** — Motor Vehicles, Food & Beverage, General Merchandise, Cannabis, and more

---

## Power BI Dashboard

The `.pbix` file (`Canadian_Retail_Trade_Sales_Visualization.pbix`) contains an interactive dashboard built on the cleaned dataset.

**To open:** Requires [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free download).

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Ruchikasbn/canadian-retail-sales.git
cd canadian-retail-sales
```

### 2. Install dependencies

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

### 3. Download the raw data

Download the raw Statistics Canada CSV from the [direct link](https://www150.statcan.gc.ca/n1/tbl/csv/20100056-eng.zip), extract it, and place `20100056.csv` in a `Dataset/` folder.

Alternatively, use the pre-cleaned dataset (`retail_sales_cleaned.csv`) and skip directly to `Data_Analysis.ipynb`.

### 4. Run the notebooks

```bash
jupyter notebook
```

Open `Data_cleaning.ipynb` first, then `Data_Analysis.ipynb`.

---

## Requirements

| Package | Purpose |
|---------|---------|
| `pandas` | Data manipulation |
| `numpy` | Numerical operations |
| `matplotlib` | Static charts |
| `seaborn` | Statistical visualizations |
| `jupyter` | Notebook environment |
| Power BI Desktop | Interactive dashboard (`.pbix`) |

---

## License

Data sourced from Statistics Canada is reproduced and distributed on an "as is" basis under the [Statistics Canada Open Licence](https://www.statcan.gc.ca/en/reference/licence).
