# Apple Retail Analytics Project

An end-to-end data analytics project using a synthetic Apple retail dataset to answer real business questions around product reliability and warranty claim rates.

## Business Question
Which Apple products have the highest warranty claim rates, and are certain regions rejecting claims more than others?

## Dataset
1M+ rows across 5 CSV files: sales, warranty, products, categories, and stores.

Source: [Apple Retail Sales Dataset on Kaggle](https://www.kaggle.com/datasets/amangarg08/apple-retail-sales-dataset)

## Tools Used
- **DuckDB** — in-process SQL engine for querying CSV files directly without loading data into memory
- **Pandas** — holds aggregated query results for visualization
- **Matplotlib / Seaborn** — visualization
- **Jupyter Notebook** — analysis environment

## Project Structure
- `apple_analytics.ipynb` — main notebook containing all data exploration, cleaning, and analysis

## What I Did

### Day 1 — Data Exploration & Cleaning
- Connected to all 5 CSV files using DuckDB views
- Standardized column names to lowercase across all tables
- Checked every table for null values, duplicate primary keys, and invalid data
- Discovered that `Pending` and `In Progress` were being used interchangeably in the warranty data — merged them into a single status using a `CASE` statement baked into the view definition
- Built a 4-table join chain: sales → warranty → products → category

## Status
Work in progress — analysis and visualizations coming soon.
