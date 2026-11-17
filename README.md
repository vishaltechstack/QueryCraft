# 🧠 QueryCraft: Query Engineering & Problem-Solving Log

![MySQL](https://img.shields.io/badge/MySQL-8.0%2B-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-Query_Optimization-CC2927?style=for-the-badge&logo=databricks&logoColor=white)
![Status](https://img.shields.io/badge/Updates-Daily_Commits-2EA44F?style=for-the-badge&logo=githubactions&logoColor=white)
![Focus](https://img.shields.io/badge/Focus-Interview_&_Analytics-7C3AED?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-24292F?style=for-the-badge)

A continuously updated repository documenting my daily **MySQL 8.0+ problem-solving streak**. Each challenge tackles real-world data manipulation, analytical reporting, edge-case handling, and query performance tuning—written with clean, readable, and production-ready SQL.

---

## 🎯 Core Objectives

* **Daily Consistency:** Solve and document at least one SQL problem every day across beginner, intermediate, and advanced difficulty tiers.
* **Clean & Modular SQL:** Prioritize readable **Common Table Expressions (CTEs)** over deeply nested subqueries.
* **Edge-Case Resilience:** Explicitly handle `NULL` values, duplicate records, tie-breaking ranks, empty sets, and division-by-zero traps.
* **Performance First:** Write sargable `WHERE` predicates and analyze query execution plans using `EXPLAIN`.

---

## 🧩 Technical Topics & Patterns Covered

| Category | SQL Techniques & Clauses Practiced |
| :--- | :--- |
| **🔍 Filtering & Logic** | `CASE WHEN` conditional bucketing, `COALESCE()`, `NULLIF()`, pattern matching (`LIKE`, `REGEXP`), `EXISTS` vs. `IN` |
| **🔗 Relational Joins** | Self-joins (hierarchies & consecutive rows), `LEFT JOIN` anti-joins (`IS NULL`), non-equi range joins, multi-table aggregations |
| **📊 Window Analytics** | `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`, `NTILE()`, `LAG()`, `LEAD()`, moving averages, and running totals (`ROWS BETWEEN`) |
| **🧱 CTEs & Recursion** | Multi-step chained CTEs (`WITH`), Recursive CTEs (`WITH RECURSIVE`) for date series generation and org-chart traversal |
| **📅 Date & Time Math** | Retention cohorts, streak/gap island problems, `DATEDIFF()`, `TIMESTAMPDIFF()`, `DATE_FORMAT()`, fiscal quarter grouping |
| **🧪 Data Validation & QA** | Duplicate primary-key detection, orphaned foreign-key audits, schema reconciliation, and boundary-value checks |

---

## ⚙️ MySQL Logical Query Execution Order

Every solution in this repository is structured around how the MySQL engine actually processes a query under the hood (rather than the order it is written):

```text
1. FROM & JOINs    ──► Assemble base tables and filter join conditions (ON)
2. WHERE           ──► Filter individual raw rows before grouping
3. GROUP BY        ──► Collapse rows into summary buckets
4. HAVING          ──► Filter aggregated groups
5. WINDOW FUNCS    ──► Compute OVER (PARTITION BY ... ORDER BY ...) analytics
6. SELECT          ──► Evaluate expressions, aliases, and columns
7. DISTINCT        ──► Remove duplicate result rows
8. ORDER BY        ──► Sort the final result set
9. LIMIT / OFFSET  ──► Paginate and return output rows
```

---

## 🛠️ Standard Solution Template

Each challenge file in this repository follows a consistent engineering format:

1. **Problem Statement:** Business question, input table schema, and expected output format.
2. **Edge Cases Considered:** Ties, missing records (`NULL`), zero-count groups, or date boundaries.
3. **Optimized Solution:** Cleanly commented MySQL 8.0+ query with time/space complexity notes (`INDEX` recommendations).

---

## 🔗 Explore My Other SQL Repositories

[![MySQL Mastery Lab](https://img.shields.io/badge/MySQL--Mastery--Lab-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://github.com/vishaltechstack/MySQL-Mastery-Lab)
[![SQLForge](https://img.shields.io/badge/SQLForge-24292F?style=for-the-badge&logo=mysql&logoColor=white)](https://github.com/vishaltechstack/SQLForge)

---

## 👨‍💻 Author

**Vishal Sharma**  
*Software Development & Quality Engineering Enthusiast*

[![GitHub](https://img.shields.io/badge/GitHub-vishaltechstack-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/vishaltechstack)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/)
[![MySQL](https://img.shields.io/badge/SQL_&_Database_Validation-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](#)

---

⭐ *Follow along with the daily commits, and feel free to star the repository if you're practicing SQL!*
