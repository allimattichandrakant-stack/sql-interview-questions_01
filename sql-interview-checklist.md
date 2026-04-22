# SQL Interview Preparation Checklist (Data Analyst)

This file contains everything you should know before attending an SQL/Data Analyst interview.

---

## 🧠 1. Core SQL Basics (MUST KNOW)

- SELECT, FROM, WHERE
- DISTINCT
- ORDER BY
- LIMIT
- BETWEEN, IN, LIKE
- NULL handling (IS NULL, IS NOT NULL)
- COALESCE

---

## 📊 2. Aggregations (VERY IMPORTANT)

- COUNT()
- SUM()
- AVG()
- MIN / MAX
- GROUP BY
- HAVING vs WHERE difference

👉 You should be able to:
- Find total sales
- Find average salary per department
- Find duplicates using GROUP BY

---

## 🔗 3. Joins (CRITICAL TOPIC)

- INNER JOIN
- LEFT JOIN
- RIGHT JOIN
- FULL OUTER JOIN
- SELF JOIN

👉 Must practice:
- Customers with no orders
- Employees with manager info
- Combining 2+ tables

---

## ⚡ 4. Subqueries

- Single-row subquery
- Multi-row subquery
- Correlated subquery

👉 Common questions:
- Second highest salary
- Above average salary
- Top N records

---

## 📈 5. Window Functions (HIGH PRIORITY)

- ROW_NUMBER()
- RANK()
- DENSE_RANK()
- LAG()
- LEAD()
- SUM() OVER()
- AVG() OVER()

👉 Must know:
- Running total
- Moving average
- Top 3 per group
- First/last record per customer

---

## 🧹 6. Data Cleaning (VERY IMPORTANT FOR DATA ANALYST)

- Handling NULL values
- Removing duplicates
- TRIM, UPPER, LOWER
- Data type conversion
- COALESCE usage

---

## 📊 7. Analytical SQL Concepts

- Cohort analysis basics
- Retention calculation
- Churn analysis
- Funnel analysis
- Percentage contribution queries

---

## 🏗️ 8. Database Design Basics

- Primary Key
- Foreign Key
- Composite Key
- Surrogate Key
- Normalization (1NF, 2NF, 3NF)
- Denormalization

---

## 🚀 9. Performance Concepts (SENIOR EDGE)

- Indexing basics
- Query optimization
- Execution plan idea
- Avoiding full table scans

---

## 📦 10. Real Interview Patterns (MOST IMPORTANT)

You should be able to solve:

- Second highest salary
- Nth highest salary
- Top N per group
- Customers with no orders
- Employees earning more than manager
- Running total sales
- Moving average
- Duplicate detection
- Most frequent value
- Cohort / retention queries

---

## ❌ COMMON MISTAKES TO AVOID

- Confusing WHERE vs HAVING
- Not understanding JOIN logic
- Overusing subqueries instead of joins
- Forgetting NULL behavior
- Not using window functions where needed

---

## 🎯 FINAL INTERVIEW GOAL

You should be able to:
- Write queries without help
- Explain your logic clearly
- Optimize basic queries
- Solve real business problems

---

## 🔥 BONUS TIP

If you can solve:
- Joins + Window functions + Aggregation together  
👉 You are already at strong Data Analyst level
