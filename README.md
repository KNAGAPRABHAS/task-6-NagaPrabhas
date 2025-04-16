
---

# 📦 Task 6: Monthly Sales Analytics with SQLite

Welcome to Task 6 of the Sales Data Analysis Series. In this task, we use **SQLite** to extract meaningful **monthly insights** from an e-commerce order dataset.

This project showcases how to:
- Structure a transactional dataset
- Write SQL queries to group data by month
- Calculate total revenue and order volume per month
- Use **DB Browser for SQLite** for data exploration and analysis

---

## 🧰 Tech Stack

| Tool                     | Purpose                                 |
|--------------------------|-----------------------------------------|
| **SQLite**               | Lightweight embedded SQL database       |
| **DB Browser for SQLite**| GUI-based SQLite browser and editor     |
| **CSV (orders.csv)**     | Source data format                      |
| **SQL**                  | For aggregation, filtering & grouping   |

---

## 📂 Repository Structure

```
task-6-sales-analysis/
│
├── db/
│   ├── task--6.sqbpro            # SQLite project file
│   └── task--6.db                # SQLite database file
│
├── data/
│   └── orders.csv                # Source order dataset
│
├── screenshots/
│   ├── Screenshot (409).png      # Database structure preview
│   └── Screenshot (410).png      # Query execution + output preview
│
├── sql/
│   └── monthly_summary.sql       # SQL query for monthly aggregation
│
└── README.md                     # Project documentation
```

---

## 🧾 Dataset Description

The dataset (`orders.csv`) contains transaction-level sales data:

| Column Name | Description                          |
|-------------|--------------------------------------|
| `order_id`  | Unique ID for each order             |
| `order_date`| Date when the order occurred (TEXT)  |
| `product_id`| Identifier for the product ordered   |
| `quantity`  | Units sold                           |
| `total_price`| Total value of the order in ₹       |

---

## 🎯 Objectives

✔️ Convert raw transactional data into a summary view  
✔️ Extract year and month components from dates  
✔️ Calculate revenue and order count by month  
✔️ Visualize and validate outputs using DB Browser  

---

## 🔍 SQL Query Breakdown

Here’s the main SQL query used:

```sql
SELECT 
    STRFTIME('%Y', order_date) AS year,
    STRFTIME('%m', order_date) AS month,
    COUNT(DISTINCT order_id) AS volume,
    SUM(total_price) AS revenue
FROM orders
GROUP BY year, month
ORDER BY year, month
LIMIT 12;
```

### 🧠 What it does:

- `STRFTIME('%Y', order_date)` – Extracts year
- `STRFTIME('%m', order_date)` – Extracts month
- `COUNT(DISTINCT order_id)` – Counts unique orders (monthly volume)
- `SUM(total_price)` – Adds up revenue
- `GROUP BY` + `ORDER BY` – Groups and sorts chronologically

---

## 📸 Screenshots

### ✅ Database View  
> The `orders` table loaded correctly with expected schema:

![DB Schema View](./screenshots/Screenshot%20(409).png)

---

### ✅ Query Output  
> Sample output showing monthly revenue and volume:

![Query Output](./screenshots/Screenshot%20(410).png)

---

## 📌 How to Use This Project

1. **Clone the repo**:
   ```bash
   git clone https://github.com/your-username/task-6-sales-analysis.git
   cd task-6-sales-analysis
   ```

2. **Launch DB Browser for SQLite**

3. **Open the `.sqbpro` file**:
   - Go to `File > Open Project`
   - Select `task--6.sqbpro`

4. **Run SQL Query**:
   - Navigate to the `Execute SQL` tab
   - Paste or load the query from `sql/monthly_summary.sql`
   - Execute it to view the monthly summary

---

## 🛠 Troubleshooting

- If your query fails with:
  ```
  near "FROM": syntax error
  ```
  Make sure you're using `STRFTIME()` (not `EXTRACT()`) — SQLite doesn't support `EXTRACT`.

- Ensure column names match those in your `.csv` file when importing into SQLite.

---

## 📈 Sample Output Table

| Year | Month | Volume | Revenue   |
|------|-------|--------|-----------|
| 2023 | 01    | 6      | ₹8098.08  |
| 2023 | 02    | 11     | ₹16539.96 |
| 2023 | 03    | 9      | ₹11518.74 |
| ...  | ...   | ...    | ...       |

---

## 🙌 Acknowledgements

- [DB Browser for SQLite](https://sqlitebrowser.org/)
- [SQLite Documentation](https://www.sqlite.org/docs.html)
- E-commerce dataset for academic and learning purposes

---
