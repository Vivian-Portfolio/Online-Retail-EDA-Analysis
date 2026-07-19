# Online Retail EDA Analysis 
*This project analysizes an online retail dataset to uncover sales trends, customer behaviour and business insights using Exploratory Analysis (EDA)*

---

## ⚙️ Project Type Flags
- [x] Exploratory Data Analysis (EDA)
- [ ] SQL Analysis / Querying
- [x] Dashboard / Data Visualization
- [ ] Data Pipeline / ETL
- [ ] Predictive Modelling / Machine Learning
- [x] Data Cleaning / Wrangling
- [ ] End-to-End (multiple of the above)
- [ ] Other: ___________

---

## Table of Contents
1. [Project Overview](#1-project-overview)
2. [Objectives](#2-objectives)
3. [Project Scope & Tools](#3-project-scope--tools)
4. [Repository Structure](#4-repository-structure)
5. [Data Workflow](#5-data-workflow)
6. [Analysis & Metrics](#6-analysis--metrics)
7. [Key Insights](#7-key-insights)
8. [Recommendations](#8-recommendations)
9. [Assumptions & Limitations](#9-assumptions--limitations)
10. [Deliverables](#10-deliverables)
11. [Author](#111-author)

---

## 1. Project Overview

**Context:** Online retailers generate large volumes of transactional data, but raw exports are rarely clean or analysis-ready - contains,  missing IDs , uplicate records and formatting issues that can distort revenue figures if left unaddressed.

**Problem Statement:** The goal is to understand the retailer's sales performance, customer purchasing behavior, and seasonal trends after cleaning the dataset.

**Approach:** Cleaned the dataset in Python — handling missing values, removing duplicates, standardizing text fields, and excluding invalid transactions — then explored revenue trends by month, country, and customer to surface actionable business insights.

**Outcome:** The cleaned dataset revealed that the UK generated most of the revenue, sales peaked in November, and a small number of products and customers contributed a large share of total sales.

---

## 2. Objectives

- **Primary Objective:** Clean and explore the Online Retail dataset to uncover patterns in revenue, seasonality and customer behavior.
- **Secondary Objective 1:** Identify monthly sales trends and seasonal peaks.
- **Secondary Objective 2:** Determine which countries and customers contribute most to total revenue.
- **Secondary Objective 3:**  Identify best-selling products by quantity and order frequency.
- **Secondary Objective 4:** Quantify the impact of data quality issues (missing values, duplicates, cancellations) on the usable dataset.

---

## 3. Project Scope & Tools

### Scope

| Dimension | Details |
|-----------|---------|
| **In Scope** | 541,909 transaction records covering invoice details, product descriptions, quantities, unit prices, customer IDs, invoice dates, and countries |
| **Out of Scope** | Customer demographic data, marketing/campaign data, and any transactions outside Dec 2010–Dec 2011 |
| **Time Period** | December 2010 - December 2011 |
| **Granularity** | Row-level transaction data (one row per invoice line item) |

### Tools & Technologies

| Category | Tool(s) Used |
|----------|-------------|
| Data Storage | CSV (sourced via Kaggle) |
| Data Processing | Python (pandas) - handling nulls, duplicates, datetime conversion, text standardization |
| Analysis |Python (pandas) - groupby, value_counts, aggregation |
| Visualization | Python (matplotlib) |
| Version Control | Git / GitHub |
| Documentation || Markdown, GitHub  |
| Other | Google Colab |

---

## 4. Repository Structure

```
Online-Retail-EDA-Analysis/
│
├── data/
│   └── raw/              # Note: raw file not hosted here (exceeds GitHub's 25MB limit) — see Data Source below
│
├── notebooks/            # Colab notebook with full cleaning, analysis, and visualizations
│
├── reports/               # Written summary report of findings
│
├── visuals/               # Exported charts and graphs
│
├── README.md              # You are here
└── project_metadata.yml   # Project metadata
```

---

## 5. Data Workflow

1. **Source:** Online Retail dataset downloaded via kagglehub (source: vijayuv/onlineretail on Kaggle), containing 541,909 records across 8 columns.
2. **Ingestion:**  Dataset read into a pandas DataFrame using pd.read_csv().
3. **Cleaning:** - Removed 1,454 rows with missing Description values, since product descriptions are essential for product-level analysis.
   - Filled 135,080 missing CustomerID values with "Unknown" to preserve transaction records while flagging that the customer link is unavailable.
   - Identified and removed 5,268 duplicate records to prevent repeated transactions from skewing the analysis.
   - Converted InvoiceDate from text to proper datetime format for time-based analysis.
   - Standardized text fields - converted Description to uppercase and stripped extra whitespace from Country and column names for consistency.
   - Excluded records with negative quantities (cancelled/returned orders, 8,872 rows) and zero unit prices from revenue calculations to avoid distortion.
4. **Transformation:** CreateD A 'year_added'- equivalent time grouping from 'InvoiceDate' for monthly revenue trends and aggregated reveune (Quantity *UnitPrice) at the country, product and customer level to support the analysis.
5. **Analysis:** Used pandas (groupby, value_counts, aggregation) to break down revenue by month, country, product, and customer.
6. **Output:** A cleaned dataset (392,692 records), a set of visual charts (seasonality, geographic revenue, top products, top customers) and a written summary report of key findings. 

---

## 6. Analysis & Metrics

### Analytical Approach

This was primarily exploratory - examining the cleaned transaction data to uncover patterns in revenue over time, by geography, and by customer, in order to surface business-relevant trends rather than test a specific hypothesis.

### Key Metrics Defined

| Metric | Plain-Language Definition | Why It Matters |
|--------|--------------------------|----------------|
| `Monthly revenue` | Total revenue summed by month | Reveals seasonal demand patterns |
| `Revenue by country` | Total revenue summed by customer country | Shows geographic concentration of the business|
| `Top products` | Products ranked by quantity sold and order frequency  | Identifies high-value customers and wholesale buyers |
| `Revenue by customer` | Total revenue summed by CustomerID | Identifies high-value customers and wholesale buyers |


### Methods Used

- Descriptive statistics - distribution and central tendency (mean, median, min, max, std) for Quantity and UnitPrice
- Trend analysis across months (Dec 2010 - Dec 2011)
- Segmentation / group comparison by country, product, and customer

---

## 7. Key Insights

**Insight 1: The UK dominates the customer base**
The United Kingdom generated 82% of total revenue, with all other countries combined accounting for only 18%. This shows the business, despite operating internationally, is fundamentally UK-anchored - relevant for anyone assessing where to focus inventory or marketing spend.

**Insight 2: Sales peak sharply ahead of the holidays**
Revenue rose steadily through the year, peaking sharply in November 2011 at £1.5M, consistent with pre-holiday shopping demand. This points to the value of planning inventory and staffing around a predictable seasonal surge rather than treating demand as flat.

**Insight 3: A small set of products drives disproportionate sales**
Items like "PAPER CRAFT, LITTLE BIRDIE" and "WHITE HANGING HEART T-LIGHT HOLDER" consistently ranked at the top in both quantity sold and order frequency. This concentration suggests a small core catalog carries much of the business's sales volume.

**Insight 4: Revenue is concentrated among a few high-value customers**
The top customer (ID 14646) alone generated over £280,000 in revenue - far exceeding typical spend - suggesting this is a wholesale or high-value business buyer rather than a typical retail customer, and worth managing separately from the broader customer base.

---

## 8. Recommendations

| Priority | Recommendation | Based On | Suggested Owner |
|----------|---------------|----------|-----------------|
|High | Build inventory and staffing plans around the November sales peak to avoid stockouts or service delays during the busiest period | Insight 2 - November seasonal peak | Operations / Inventory team |
| Medium | Investigate the top wholesale-style customers (e.g., ID 14646) to see if a dedicated account management or bulk-pricing approach would strengthen retention | Insight 4 - customer concentration | Sales / Account Management team |
| Low | Explore whether the international customer base (18% of revenue) could be grown through targeted marketing, given how UK-concentrated the business currently is | Insight 1 - UK revenue dominance | Marketing team |

---

## 9. Assumptions & Limitations

### Assumptions
- Transaction records were assumed to be complete and accurate as extracted, with no independent validation against the retailer's original systems.
- Missing CustomerID values were assumed to represent genuinely untracked customers (e.g., guest checkouts) rather than data entry errors, and were preserved as "Unknown" rather than dropped.

### Limitations
- 135,080 transactions have no linked CustomerID, limiting the completeness of customer-level analysis (e.g., repeat purchase behavior) for that portion of the data.
- Cancelled/returned orders (negative quantities) were excluded from revenue analysis, so this dataset reflects completed sales only, not full transaction volume including returns.
- The dataset covers a single 13-month window (Dec 2010–Dec 2011), so findings may reflect that specific period rather than a longer-term trend.

---

## 10. Deliverables

| Deliverable | Description | Location |
|-------------|--------------|----------|
| Cleaned dataset | Transaction data with nulls handled, duplicates removed, and datetime fields formatted (392,692 records) | `Not hosted in repo - see Data Source`|
| Analysis notebook | Full cleaning, analysis, and visualization code | `notebooks/Online_Retail_EDA_Analysis.ipynb `|
| Live notebook (Colab) | Interactive version, viewable/run directly in-browser | `[Open in Colab](https://colab.research.google.com/drive/1DNEcS6iHDUCJ1iL-gQB5uu6wfhYWK41V?usp=sharing)` |
| Summary report | Written findings and insights | `reports/` |
| Visualizations | Charts illustrating key trends | `visuals/` |

---

## 11. Author

**Vivian Okwara**
Data Analyst|lagos Nigeria 

- 🔗 https://LinkedIn.com/in/okwara-vivian
- 💼 https://Vivian-Portfoliogithub.io
- 📧 okwaravivian26@gmail.com

---

*Last updated: July 2026*
