# 📚 Bookstore Sales Analysis — SQL Project

A SQL-based analysis of a bookstore's sales data, covering data cleaning, business-question queries, and revenue/inventory insights using **PostgreSQL**.

## 📌 Project Overview

This project analyzes a bookstore's operations using three related datasets — **Books**, **Customers**, and **Orders** — to answer real business questions such as top-selling genres, highest-spending customers, remaining stock after order fulfillment, and revenue trends.

The goal was to do end to end SQL analysis: designing a relational schema, cleaning raw data, writing business-driven queries — the same workflow used in real data analyst roles.

## 🗂️ Dataset

This project is built on 3 relational tables — **books**, **customers**, and **orders** — connected through foreign keys (`orders.customer_id → customers.customer_id` and `orders.book_id → books.book_id`), allowing sales activity to be traced back to individual customers and specific books.

### 📕 books

| Column | Description |
|---|---|
| Book_id | Unique book ID (Primary Key) |
| Title | Book title |
| Author | Book author |
| Genre | Book genre |
| Published_year | Year of publication |
| Price | Price per unit |
| Stock | Units currently in stock |

### 👤 customers

| Column | Description |
|---|---|
| customer_id | Unique customer ID (Primary Key) |
| name | Customer name |
| email | Customer email |
| phone | Customer phone number |
| city | Customer city |
| country | Customer country |

### 🧾 orders

| Column | Description |
|---|---|
| order_id | Unique order ID (Primary Key) |
| customer_id | Links to customers table (Foreign Key) |
| book_id | Links to books table (Foreign Key) |
| order_date | Date the order was placed |
| quantity | Number of units ordered |
| total_amount | Total order value |

*Data files are in the [`/data`](./data) folder.*

## 🛠️ Tools Used

- **PostgreSQL** — database & query engine
- **pgAdmin 4** — GUI for schema creation and CSV import
- **SQL** — schema design, data cleaning, and analysis queries

## 🧹 Data Cleaning Process

Before analysis, the raw data was checked for:
- **Missing values** — verified no NULLs across key columns in all 3 tables
- **Duplicate records** — checked using `GROUP BY` + `HAVING COUNT(*) > 1` on full-row combinations
- **Duplicate primary keys** — verified `book_id`, `customer_id`, and `order_id` are all unique

Full cleaning queries are documented in the [Bookstore_sales_analysis.sql]

## ❓ Most Important Business Questions

Out of 21 total queries, these are the ones with the most direct business impact:

| # | Business Question | Answer | Why It Matters |
|---|---|---|---|
| 5 | Total stock of books available | **25,056 units** | Snapshot of overall inventory health |
| 11 | Total revenue from all orders | **$75,628.66** | Core top-line business metric |
| 12 | Books sold per genre | **Mystery leads with 504 units**; Fiction lowest at 225 | Reveals which genres actually drive sales |
| 14 | Customers with at least 3 orders | **41 customers** (top: Carrie Perez, 6 orders) | Identifies loyal, repeat customers |
| 15 | Most frequently ordered book | **3-way tie at 4 orders each** | Flags top-performing titles |
| 17 | Total quantity sold by each author | **Patrick Contreras leads with 28 units** | Helps decide which authors to stock more of |
| 19 | Highest-spending customer | **Kim Turner — $1,398.90** | Highlights a key account worth retaining |
| 20 | Stock remaining after fulfilling orders | **30 books show negative remaining stock** | Flags a data-quality issue, not just low stock |

*Full list of all 21 questions and their queries is in the [Bookstore_sales_analysis.sql]*

## 💡 Key Insights

- **Genre performance (Q12):** Sales are uneven across genres — **Mystery leads with 504 units sold**, while **Fiction trails at 225**, a 2.2x gap. Inventory and marketing budget would be better weighted toward Mystery, Sci-Fi, and Fantasy (all 440+ units) rather than spread evenly.
- **Customer loyalty (Q14 & Q19):** Only **41 out of 500 customers (~8%)** placed 3 or more orders, and the top spender, **Kim Turner, contributed $1,398.90** — noticeably ahead of the next highest ($1,080.95). This small repeat-customer segment is disproportionately valuable and worth a targeted retention effort.
- **Best-seller tie (Q15):** Rather than one runaway best-seller, three different titles are tied at 4 orders each — suggesting demand is fairly spread at the top rather than concentrated in a single hit title.
- **Data-quality finding (Q20):** 30 books show *negative* remaining stock (orders exceed recorded stock), worst case at −18 units. This means the stock numbers aren't being kept in sync with fulfilled orders — a real operational gap, not just a low-inventory warning.

## 🔗 Connect

**Author:** Soumen Biswas
*(https://www.linkedin.com/in/hereissoumenbiswas/)*

*A practice project to strengthen SQL skills - schema design, data cleaning, and business-question analysis.*
