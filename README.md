# 🗄️ Databases & SQL for Analysts
### A 9-Day Series From First Concepts to Advanced Querying 


A structured, beginner-to-intermediate SQL series for **data analysts** . Every concept is covered through a single, consistent example database, an online store called `online_store` will be build from scratch on Day 3 and query all the way through Day 9. By the end, this practice will helps to answer real business questions with clean, production-quality SQL.

---

## What Will Learn

By working through all nine days, you will go from "what is a database?" to writing multi-table analytical queries with window functions and CTEs which is one of the skills listed alongside Python and statistics in data analyst job postings.

| Phase | Days | Focus |
|-------|------|-------|
| **Foundations** | 1 - 2 | Database concepts, relational model, SQL language families, data types |
| **Building** | 3 - 4 | DDL (CREATE / ALTER / DROP), DML (INSERT / UPDATE / DELETE), constraints |
| **Querying** | 5 - 9 | The full DQL toolkit - SELECT, filtering, aggregation, joins, subqueries, CTEs, CASE, window functions |

---

## The Example Database

All nine articles work on a single database: **`online_store`**.

```
customers ──< orders ──< order_items >── products >── categories
```

### Schema

```sql
customers     (customer_id PK, first_name, last_name, email, city, country, signup_date)
categories    (category_id PK, category_name)
products      (product_id PK, product_name, category_id FK, price, stock_quantity)
orders        (order_id PK, customer_id FK, order_date, status)
order_items   (order_item_id PK, order_id FK, product_id FK, quantity, unit_price)
```

### Relationships

- A **customer** places many **orders**.
- An **order** contains many **order items** (line items).
- Each **order item** references one **product**.
- A **product** belongs to one **category**.
- `order_items` is a bridge table that resolves the many-to-many relationship between orders and products.

### Sample Data (loaded on Day 4)

| Table | Rows | Highlights |
|-------|------|------------|
| `customers` | 10 | 1 customer with a `NULL` city; 1 customer with no orders — useful for `IS NULL` and `LEFT JOIN` exercises |
| `categories` | 5 | Electronics, Books, Clothing, Home & Kitchen, Sports |
| `products` | 15 | 1 out-of-stock product; 1 product never ordered — realistic edge cases |
| `orders` | 15 | Statuses: Completed, Pending, Cancelled; dates span Jan–Jun 2024 |
| `order_items` | 25 | Total verified revenue: ₹48,463 across all orders |

---

## 📚 Series Contents

| Day | Article | Topics Covered |
|-----|---------|---------------|
| **1** | Understanding Databases | Database vs DBMS vs RDBMS · relational vs NoSQL · tables, rows, columns · primary & foreign keys · normalization |
| **2** | The SQL Language and Our Example Database | DDL / DML / DQL / DCL / TCL · data types · NULL · practice environment setup · full schema walkthrough |
| **3** | DDL - Building the Structure of Our Database | `CREATE DATABASE` · `CREATE TABLE` · constraints (PK, FK, NOT NULL, UNIQUE, DEFAULT, CHECK, AUTO_INCREMENT) · `ALTER TABLE` · `DROP` · `TRUNCATE` |
| **4** | DML - Bringing the Database to Life | `INSERT` (single & multi-row) · `UPDATE` · `DELETE` · referential integrity · transactions (`COMMIT` / `ROLLBACK`) |
| **5** | DQL I - SELECT, Filtering & Sorting | `SELECT` · column aliases · `DISTINCT` · `WHERE` with `=`, `!=`, `>`, `<`, `AND`, `OR`, `NOT`, `BETWEEN`, `IN`, `LIKE`, `IS NULL` · `ORDER BY` · `LIMIT` / `OFFSET` |
| **6** | DQL II - Aggregation & Grouping | `COUNT` · `SUM` · `AVG` · `MIN` · `MAX` · `ROUND` · `GROUP BY` · `HAVING` · `DATE_FORMAT` · `MONTH` / `YEAR` · WHERE vs HAVING · execution order |
| **7** | DQL III - Joining Tables | Table aliases · `INNER JOIN` · `LEFT JOIN` · `RIGHT JOIN` · multi-table joins · self-join · cross join · FULL OUTER JOIN workaround · `UNION` / `UNION ALL` · ON vs WHERE with LEFT JOIN |
| **8** | DQL IV - Subqueries, CTEs & CASE | Scalar subqueries · multi-row subqueries (`IN` / `NOT IN`) · correlated subqueries · `EXISTS` · derived tables · `WITH` (CTE) · multiple CTEs · `CASE` (simple & searched) · `COALESCE` · conditional aggregation |
| **9** | DQL V - Window Functions & Capstone | `ROW_NUMBER` · `RANK` · `DENSE_RANK` · `LAG` / `LEAD` · `SUM OVER` running totals · `MAX OVER` · percentage share · frame clause · `CREATE VIEW` · best practices · 8-question capstone |

---
## ✅ Topics Covered

<details>
<summary><strong>Foundations (Days 1–2)</strong></summary>

- What a database is and why analysts need SQL
- Database vs DBMS vs RDBMS
- Relational vs non-relational databases
- Tables, rows, columns, schema
- Primary keys and foreign keys
- Relationships and normalization
- The five SQL command families: DDL, DML, DQL, DCL, TCL
- Data types: INT, DECIMAL, VARCHAR, TEXT, DATE, DATETIME, BOOLEAN
- NULL semantics
- The `online_store` schema walkthrough

</details>

<details>
<summary><strong>DDL - Data Definition Language (Day 3)</strong></summary>

- `CREATE DATABASE` and `USE`
- `CREATE TABLE` with column definitions
- Constraints: `PRIMARY KEY`, `FOREIGN KEY`, `NOT NULL`, `UNIQUE`, `DEFAULT`, `CHECK`
- `AUTO_INCREMENT` (MySQL)
- InnoDB and foreign key enforcement
- Dependency order for table creation
- `ALTER TABLE`: `ADD COLUMN`, `MODIFY COLUMN`, `RENAME COLUMN`, `DROP COLUMN`, `ADD CONSTRAINT`
- `DROP TABLE` / `DROP DATABASE` with `IF EXISTS`
- `TRUNCATE TABLE` vs `DELETE`
- Verification: `SHOW TABLES`, `DESCRIBE`, `SHOW CREATE TABLE`

</details>

<details>
<summary><strong>DML - Data Manipulation Language (Day 4)</strong></summary>

- `INSERT INTO ... VALUES` (single and multi-row)
- Inserting with `NULL` for optional columns
- Insert dependency order with foreign keys
- `UPDATE ... SET ... WHERE`
- Calculated updates (`SET price = price * 1.10`)
- The missing-`WHERE` danger — affects all rows
- `DELETE FROM ... WHERE`
- Referential integrity blocking invalid deletes
- Transactions: `START TRANSACTION`, `COMMIT`, `ROLLBACK`

</details>

<details>
<summary><strong>DQL - Data Query Language (Days 5-9)</strong></summary>

**SELECT fundamentals (Day 5)**
- `SELECT` specific columns, `SELECT *`
- Column aliases with `AS`
- `DISTINCT` for unique values
- `WHERE` with all comparison and logical operators
- `BETWEEN`, `IN`, `NOT IN`, `LIKE` (`%` and `_` wildcards)
- `IS NULL`, `IS NOT NULL`
- `ORDER BY` ASC / DESC, multiple columns
- `LIMIT` and `LIMIT ... OFFSET`
- SQL execution order: FROM → WHERE → SELECT → ORDER BY → LIMIT

**Aggregation and grouping (Day 6)**
- `COUNT(*)`, `COUNT(column)`, `COUNT(DISTINCT column)`
- `SUM`, `AVG`, `MIN`, `MAX`
- `ROUND(value, decimals)`
- `GROUP BY` - single and multiple columns
- The SELECT rule with GROUP BY (`ONLY_FULL_GROUP_BY`)
- `HAVING` - filtering groups after aggregation
- WHERE vs HAVING — when to use each
- Date functions: `MONTH()`, `YEAR()`, `DATE_FORMAT()`, `MONTHNAME()`
- Full execution order: FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT

**Joins (Day 7)**
- Table aliases and dot notation
- `INNER JOIN`
- `LEFT JOIN` and the `LEFT JOIN + IS NULL` pattern for finding non-matches
- `RIGHT JOIN`
- Multi-table joins (chaining 3, 4, 5 tables)
- `JOIN` with `GROUP BY` — the core analytical pattern
- Self join
- `CROSS JOIN`
- FULL OUTER JOIN workaround (LEFT + RIGHT + UNION)
- `UNION` vs `UNION ALL`
- ON vs WHERE placement with LEFT JOIN

**Subqueries, CTEs, CASE (Day 8)**
- Scalar subqueries in `WHERE` and `SELECT`
- Multi-row subqueries with `IN` and `NOT IN`
- Correlated subqueries (per-row computations)
- `EXISTS` vs `IN`
- Derived tables (subqueries in `FROM`)
- Common Table Expressions (`WITH cte AS (...)`)
- Multiple CTEs chained with commas
- Simple `CASE` (value matching)
- Searched `CASE` (condition-based)
- `COALESCE` for NULL defaults
- Conditional aggregation: `COUNT(CASE WHEN ... THEN 1 END)`, `SUM(CASE WHEN ... ELSE 0 END)`

**Window functions (Day 9)**
- `OVER()` clause: `PARTITION BY`, `ORDER BY`, frame specification
- `ROW_NUMBER()` — unique sequential rank
- `RANK()` — rank with gaps for ties
- `DENSE_RANK()` — rank without gaps
- `LAG(column, n)` and `LEAD(column, n)` for period-over-period comparison
- `SUM() OVER (ORDER BY ... ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)` — running totals
- `SUM() OVER ()` — grand total in every row (percentage share pattern)
- `MAX() OVER ()` — maximum across all rows for relative comparisons
- The "top-N per group" pattern: `ROW_NUMBER()` in CTE + `WHERE rn = 1`
- `CREATE VIEW` / `DROP VIEW`
- Query best practices

</details>

