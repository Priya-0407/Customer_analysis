# customer_analysis
An end-to-end data analytics project exploring transactional retail data to uncover spending patterns, customer segments, product preferences, and subscription behavior using Python, PostgreSQL, and Power BI.

---

## Project Overview

This project analyzes **3,900 customer transactions** across multiple product categories to answer key business questions about revenue drivers, customer loyalty, discount effectiveness, and product performance.

The analysis follows a full data pipeline:
> **Raw Data → Python (EDA & Cleaning) → PostgreSQL (SQL Analysis) → Power BI (Dashboard)**

---

## Dataset

| Attribute | Details |
|-----------|---------|
| Rows | 3,900 |
| Columns | 18 |
| Missing Values | 37 in `Review Rating` column |
| Source | Retail transactional dataset |

**Key Features:**

- **Demographics** — Age, Gender, Location, Subscription Status
- **Purchase Details** — Item Purchased, Category, Purchase Amount (USD), Season, Size, Color
- **Behavior** — Discount Applied, Previous Purchases, Frequency of Purchases, Review Rating, Shipping Type, Payment Method

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| Python (pandas) | Data loading, cleaning, feature engineering |
| PostgreSQL | Structured business queries |
| Power BI | Interactive dashboard |

---

## Project Workflow

### 1. Data Cleaning & EDA (Python)

- **Data Loading** — Imported dataset using `pandas`
- **Initial Exploration** — Used `df.info()` and `.describe()` to understand structure and distributions
- **Missing Data Handling** — Imputed 37 missing `Review Rating` values using the **median rating per product category**
- **Column Standardization** — Renamed all columns to `snake_case`
- **Feature Engineering**
  - Created `age_group` column by binning customer ages
  - Created `purchase_frequency_days` column from purchase frequency data
- **Redundancy Check** — Confirmed `discount_applied` and `promo_code_used` were redundant; dropped `promo_code_used`
- **Database Integration** — Loaded the cleaned DataFrame into PostgreSQL for SQL analysis

---

### 2. SQL Analysis (PostgreSQL)

Ten business questions were answered using structured SQL queries:

| # | Analysis | Insight |
|---|----------|---------|
| 1 | **Revenue by Gender** | Male: $157,890 vs Female: $75,191 |
| 2 | **High-Spending Discount Users** | 839 customers used discounts yet spent above average |
| 3 | **Top 5 Products by Rating** | Gloves (3.86), Sandals (3.84), Boots (3.82), Hat (3.80), Skirt (3.78) |
| 4 | **Shipping Type Comparison** | Express avg: $60.48 vs Standard avg: $58.46 |
| 5 | **Subscribers vs Non-Subscribers** | Avg spend nearly equal (~$59.49 vs $59.87); non-subscribers = 73% of customers |
| 6 | **Discount-Dependent Products** | Hat (50%), Sneakers (49.66%), Coat (49.07%), Sweater (48.17%), Pants (47.37%) |
| 7 | **Customer Segmentation** | Loyal: 3,116 · Returning: 701 · New: 83 |
| 8 | **Top 3 Products per Category** | Clothing: Blouse, Pants, Shirt · Footwear: Sandals, Shoes, Sneakers |
| 9 | **Repeat Buyers & Subscriptions** | 2,518 repeat buyers are non-subscribers vs 958 subscribers |
| 10 | **Revenue by Age Group** | Young Adult: $62,143 · Middle-aged: $59,197 · Adult: $55,978 · Senior: $55,763 |

---

### 3. Dashboard (Power BI)

An interactive dashboard was built with slicers for **Subscription Status, Gender, Category, and Shipping Type**, displaying:

- KPI cards: 3.9K customers · $59.76 avg purchase · 3.75 avg rating
- % of customers by subscription status (donut chart)
- Revenue and sales by category (bar charts)
- Revenue and sales by age group (horizontal bar charts)

---

## Key Findings

- **Male customers** generate significantly more revenue (~2× females), despite female customers existing in the dataset
- **73% of customers are non-subscribers**, yet their avg spend matches subscribers — a missed retention opportunity
- **Young Adults** are the top revenue segment ($62,143), followed closely by Middle-aged customers
- **839 customers** used discounts but still spent above average — discounts didn't suppress premium spending
- **Hat, Sneakers, and Coat** show the highest discount dependency (≈49–50%), indicating potential margin leakage
- **80% of customers are classified as Loyal** (3,116 of 3,900), suggesting a strong retention base

---

## Business Recommendations

1. **Boost Subscriptions** — Only 27% of customers subscribe. Launch exclusive perks (early access, free shipping) to convert the loyal non-subscriber base
2. **Loyalty Programs** — Reward repeat buyers to accelerate movement into the "Loyal" segment
3. **Review Discount Policy** — Products like Hat and Sneakers have ~50% discount rates; assess whether this drives incremental sales or only cannibalizes margin
4. **Product Campaigns** — Spotlight top-rated products (Gloves, Sandals, Boots) and best-sellers (Blouse, Jewelry, Jacket) in marketing
5. **Targeted Marketing** — Focus ad spend on Young Adults and Express Shipping users — both signal higher purchase intent and value
