# Apple Retail Analytics Project

An end-to-end data analytics project using a synthetic Apple retail dataset to answer real business questions around product reliability, warranty claim rates, and regional performance.

## Dataset

1M+ rows across 5 CSV files: sales, warranty, products, categories, and stores.

Source: [Apple Retail Sales Dataset on Kaggle](https://www.kaggle.com/datasets/amangarg08/apple-retail-sales-dataset)

> Note: This is a synthetic dataset modeled after Apple retail data. It is used to practice answering business questions that would matter in a real-world analytics context.

---

## Tools Used

- **DuckDB** — in-process SQL engine that queries CSV files directly without loading data into memory, handling 1M+ rows efficiently
- **Pandas** — holds aggregated query results for visualization
- **Matplotlib / Seaborn** — visualization
- **Jupyter Notebook** — analysis environment

---

## Project Structure

```
apple_analytics.ipynb   — main notebook: data exploration, cleaning, and analysis
```

---

## Business Questions

This project answers a series of real business questions an Apple data analyst might face:

1. **Product Reliability & "The Cost of Quality"** ✅
2. More questions coming in future sessions

---

## What I Did

### Data Exploration & Cleaning

Before writing a single analytical query, every table was validated:

- Registered all 5 CSV files as DuckDB views — no data loaded into memory
- Checked every table for **null values**, **duplicate primary keys**, and **invalid data**
- Standardized all column names to **lowercase** across stores and products tables
- Discovered that `Pending` and `In Progress` were being used interchangeably in the warranty table — merged them into a single status using a `CASE` statement baked into the view definition
- Validated quantity values in sales — confirmed no zero or negative quantities
- **All 5 tables came back clean** with no data quality issues

### Business Question 1 — Product Reliability & "The Cost of Quality"

**Business Problem:** High warranty claim rates can destroy a product's profitability and ruin a brand's reputation. Apple needs to know which products are failing most often.

**Approach:** Three queries answering three dimensions of the question.

#### Query 1 — Claim Rate by Category
- Joined sales → warranty → products → category across 1M+ rows
- Calculated claim rate as: `total warranty claims / total units sold`
- **Finding:** Claim rates are nearly identical across all 10 categories (0.49%–0.53%). No single category stands out as dramatically worse. Smartphones and Accessories have the highest absolute claim counts due to higher sales volume.

#### Query 2 — Claim Rate by Product Model
- Same join structure, drilled down to individual product level
- **Finding:** Specific models emerge as outliers:
  - **MacBook Pro (Touch Bar)** — 0.60%
  - **iPhone 13 Pro** — 0.58%
  - **Beats Studio Headphones** — 0.57%
  - Multiple iPhone models appear in the top offenders, suggesting a potential quality issue across iPhone generations rather than a one-off defect

#### Query 3 — Regional Rejection Rate
- Joined warranty → sales → stores to get country-level data
- Calculated: rejected claims as a percentage of total claims per region
- **Finding:** Top 5 countries by rejection rate:
  - Colombia — 27.53%
  - Singapore — 26.38%
  - Netherlands — 26.17%
  - Austria — 25.67%
  - Italy — 25.60%
  - The geographic spread across South America, Asia, and Europe suggests rejections are not driven by a single regional policy — Apple's claims processing consistency across these regions warrants investigation

---

## Status

🔄 Work in progress — additional business questions coming in future sessions.

---

## Key Takeaways So Far

- Overall warranty claim rates are low (~0.5%) and consistent across product categories
- The real story is at the **product model level** — specific models significantly outpace the category average
- **Regional rejection rates** vary by up to 5 percentage points, suggesting inconsistency in how claims are processed globally
- DuckDB handled 1M+ rows seamlessly without ever loading raw data into Python memory
