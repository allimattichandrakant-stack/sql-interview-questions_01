# SQL Interview Questions and Answers (Data Analyst)

A curated list of 100+ SQL interview questions with answers, covering basic to advanced concepts in SQL.

---

## 📌 Basic SQL Questions

### 1. What is SQL?
SQL (Structured Query Language) is used to store, retrieve, and manipulate data in relational databases.

### 2. What is a database?
A database is an organized collection of structured data stored electronically.

### 3. What is a table?
A table is a collection of rows and columns used to store data.

### 4. What is a primary key?
A primary key uniquely identifies each record in a table.

### 5. What is a foreign key?
A foreign key links one table to another.

### 6. What is the difference between WHERE and HAVING?
WHERE filters rows before grouping; HAVING filters after GROUP BY.

### 7. What is SELECT?
Used to retrieve data from a database.

### 8. What does DISTINCT do?
Removes duplicate values.

### 9. What is ORDER BY?
Sorts the result set.

### 10. What is LIMIT?
Restricts number of rows returned.

---

## ⚙️ Intermediate SQL Questions

### 11. What is a JOIN?
Used to combine rows from multiple tables.

### 12. Types of JOINs?
INNER, LEFT, RIGHT, FULL.

### 13. What is INNER JOIN?
Returns matching rows from both tables.

### 14. What is LEFT JOIN?
Returns all rows from left + matching from right.

### 15. What is GROUP BY?
Groups rows with same values.

### 16. What is an aggregate function?
Functions like COUNT(), SUM(), AVG().

### 17. What is COUNT(*)?
Counts total rows.

### 18. What is a subquery?
A query inside another query.

### 19. What is a view?
A virtual table based on query.

### 20. What is a UNION?
Combines results of two queries.

---

## 📊 Practical Query Questions

### 21. Find total number of customers
SELECT COUNT(*) FROM customers;

## SQL Interview Questions and Answers (Data Analyst)

### 22. Find highest salary
SELECT MAX(salary) FROM employees;

### 23. Find second highest salary
SELECT MAX(salary) FROM employees 
WHERE salary < (SELECT MAX(salary) FROM employees);

### 24. Find duplicate records
SELECT name, COUNT(*) 
FROM users 
GROUP BY name 
HAVING COUNT(*) > 1;

### 25. Find employees with salary greater than average
SELECT * FROM employees 
WHERE salary > (SELECT AVG(salary) FROM employees);

---

## Advanced SQL

### 26. What are window functions?
Window functions perform calculations across a set of rows related to the current row without collapsing results.

### 27. ROW_NUMBER()
SELECT name, salary,
ROW_NUMBER() OVER (ORDER BY salary DESC) AS rn
FROM employees;

### 28. RANK()
Assigns rank with gaps when ties exist.

### 29. DENSE_RANK()
Assigns rank without gaps even when ties exist.

### 30. PARTITION BY
Used to divide rows into groups for window functions.

---

## Data Analyst Scenarios

### 31. Running total
SELECT date, sales,
SUM(sales) OVER (ORDER BY date) AS running_total
FROM sales;

### 32. Top 3 products
SELECT * FROM products
ORDER BY sales DESC
LIMIT 3;

### 33. Monthly sales
SELECT MONTH(date), SUM(sales)
FROM sales
GROUP BY MONTH(date);

### 34. Customers with no orders
SELECT c.name
FROM customers c
LEFT JOIN orders o
ON c.id = o.customer_id
WHERE o.id IS NULL;

---

## Core Concepts

### 35. Normalization
Organizing data to reduce redundancy.

### 36. Denormalization
Adding redundancy for performance.

### 37. Indexing
Improves query speed.

### 38. ACID properties
Atomicity, Consistency, Isolation, Durability.

### 39. CTE
Common Table Expression used for temporary result sets.

### 40. Example CTE
WITH temp AS (
    SELECT * FROM employees WHERE salary > 50000
)
SELECT * FROM temp;


### 41. Find second highest salary
SELECT MAX(salary)
FROM employees
WHERE salary < (SELECT MAX(salary) FROM employees);

### 42. Find 3rd highest salary
SELECT DISTINCT salary
FROM employees e1
WHERE 3 = (
    SELECT COUNT(DISTINCT salary)
    FROM employees e2
    WHERE e2.salary >= e1.salary
);

### 43. Find duplicate emails
SELECT email, COUNT(*)
FROM users
GROUP BY email
HAVING COUNT(*) > 1;

### 44. Delete duplicates (keep one)
DELETE FROM users
WHERE id NOT IN (
    SELECT MIN(id)
    FROM users
    GROUP BY email
);

### 45. Customers with no orders
SELECT c.customer_id
FROM customers c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
WHERE o.customer_id IS NULL;

### 46. Top 3 salaries per department
SELECT *
FROM (
    SELECT *,
    RANK() OVER (PARTITION BY department ORDER BY salary DESC) rnk
    FROM employees
) t
WHERE rnk <= 3;

### 47. Running total of sales
SELECT order_date, amount,
SUM(amount) OVER (ORDER BY order_date) AS running_total
FROM sales;

### 48. Moving average (3 rows)
SELECT order_date, amount,
AVG(amount) OVER (
    ORDER BY order_date
    ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
) AS moving_avg
FROM sales;

### 49. Employees with same salary
SELECT salary, COUNT(*)
FROM employees
GROUP BY salary
HAVING COUNT(*) > 1;

### 50. Highest paid employee per department
SELECT *
FROM (
    SELECT *,
    ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) rn
    FROM employees
) t
WHERE rn = 1;

### 51. Monthly revenue
SELECT DATE_FORMAT(order_date, '%Y-%m') AS month,
SUM(amount) AS revenue
FROM orders
GROUP BY DATE_FORMAT(order_date, '%Y-%m');

### 52. Daily active users
SELECT login_date, COUNT(DISTINCT user_id)
FROM user_logins
GROUP BY login_date;

### 53. Conversion rate
SELECT 
(SELECT COUNT(DISTINCT user_id) FROM purchases) * 100.0 /
(SELECT COUNT(DISTINCT user_id) FROM visits) AS conversion_rate;

### 54. Repeat customers
SELECT customer_id
FROM orders
GROUP BY customer_id
HAVING COUNT(*) > 1;

### 55. Products never sold
SELECT p.product_id
FROM products p
LEFT JOIN sales s
ON p.product_id = s.product_id
WHERE s.product_id IS NULL;

### 56. % contribution of each product
SELECT product_id,
SUM(sales) * 100.0 / (SELECT SUM(sales) FROM sales) AS pct
FROM sales
GROUP BY product_id;

### 57. Rank employees by salary in dept
SELECT *,
RANK() OVER (PARTITION BY department ORDER BY salary DESC) rnk
FROM employees;

### 58. First purchase of each customer
SELECT *
FROM (
    SELECT *,
    ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY order_date) rn
    FROM orders
) t
WHERE rn = 1;

### 59. Last purchase of each customer
SELECT *
FROM (
    SELECT *,
    ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY order_date DESC) rn
    FROM orders
) t
WHERE rn = 1;

### 60. Find missing IDs (gap detection)
SELECT id + 1 AS missing_id
FROM employees e1
WHERE NOT EXISTS (
    SELECT 1 FROM employees e2 WHERE e2.id = e1.id + 1
);

### 61. Remove NULL salaries
SELECT *
FROM employees
WHERE salary IS NOT NULL;

### 62. Replace NULL with 0
SELECT COALESCE(salary, 0)
FROM employees;

### 63. Trim names
SELECT TRIM(name)
FROM users;

### 64. Lowercase emails
SELECT LOWER(email)
FROM users;

### 65. Invalid emails
SELECT *
FROM users
WHERE email NOT LIKE '%@%';

### 66. Cohort (first purchase month)
SELECT user_id,
MIN(order_date) AS first_purchase_month
FROM orders
GROUP BY user_id;

### 67. Active users after date
SELECT COUNT(DISTINCT user_id)
FROM orders
WHERE order_date > '2024-01-01';

### 68. Customer lifetime value
SELECT customer_id, SUM(amount) AS lifetime_value
FROM orders
GROUP BY customer_id;

### 69. Most frequent product
SELECT product_id, COUNT(*) AS cnt
FROM sales
GROUP BY product_id
ORDER BY cnt DESC
LIMIT 1;

### 70. Top product per category
SELECT *
FROM (
    SELECT *,
    RANK() OVER (PARTITION BY category ORDER BY sales DESC) rnk
    FROM products
) t
WHERE rnk = 1;


### 71. Find top 5 customers by total spend
SELECT customer_id, SUM(amount) AS total_spent
FROM orders
GROUP BY customer_id
ORDER BY total_spent DESC
LIMIT 5;

### 72. Find customers who placed orders on consecutive days
SELECT DISTINCT a.customer_id
FROM orders a
JOIN orders b
ON a.customer_id = b.customer_id
AND DATEDIFF(a.order_date, b.order_date) = 1;

### 73. Find employees who earn more than their manager
SELECT e.employee_id, e.salary
FROM employees e
JOIN employees m
ON e.manager_id = m.employee_id
WHERE e.salary > m.salary;

### 74. Find department-wise average salary
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department;

### 75. Find employees with salary above department average
SELECT e.*
FROM employees e
JOIN (
    SELECT department, AVG(salary) avg_sal
    FROM employees
    GROUP BY department
) d
ON e.department = d.department
WHERE e.salary > d.avg_sal;

### 76. Find product revenue ranking
SELECT product_id, SUM(amount) AS revenue,
RANK() OVER (ORDER BY SUM(amount) DESC) rnk
FROM sales
GROUP BY product_id;

### 77. Find first order date per customer
SELECT customer_id, MIN(order_date) AS first_order
FROM orders
GROUP BY customer_id;

### 78. Find customers with only one order
SELECT customer_id
FROM orders
GROUP BY customer_id
HAVING COUNT(*) = 1;

### 79. Find percentage of total sales per region
SELECT region,
SUM(sales) * 100.0 / (SELECT SUM(sales) FROM sales) AS pct_sales
FROM sales
GROUP BY region;

### 80. Find cumulative sum of each customer’s orders
SELECT customer_id, order_date, amount,
SUM(amount) OVER (PARTITION BY customer_id ORDER BY order_date) AS running_total
FROM orders;

### 81. Find employees hired in last 30 days
SELECT *
FROM employees
WHERE hire_date >= CURRENT_DATE - INTERVAL 30 DAY;

### 82. Find missing dates in sales table (simple logic)
SELECT DATE_ADD(a.date, INTERVAL 1 DAY) AS missing_date
FROM sales a
WHERE NOT EXISTS (
    SELECT 1 FROM sales b WHERE b.date = DATE_ADD(a.date, INTERVAL 1 DAY)
);

### 83. Find highest sales day
SELECT date, SUM(amount) AS total_sales
FROM sales
GROUP BY date
ORDER BY total_sales DESC
LIMIT 1;

### 84. Find average order value per customer
SELECT customer_id, AVG(amount) AS avg_order_value
FROM orders
GROUP BY customer_id;

### 85. Find customers who never placed order
SELECT c.customer_id
FROM customers c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
WHERE o.customer_id IS NULL;

### 86. Find product with highest units sold
SELECT product_id, SUM(quantity) AS total_qty
FROM sales
GROUP BY product_id
ORDER BY total_qty DESC
LIMIT 1;

### 87. Find employees with duplicate phone numbers
SELECT phone, COUNT(*)
FROM employees
GROUP BY phone
HAVING COUNT(*) > 1;

### 88. Find median salary (basic approach)
SELECT salary
FROM (
    SELECT salary,
    ROW_NUMBER() OVER (ORDER BY salary) rn,
    COUNT(*) OVER () cnt
    FROM employees
) t
WHERE rn IN (FLOOR((cnt + 1)/2), CEIL((cnt + 1)/2));

### 89. Find customers who increased spending over time
SELECT customer_id
FROM orders
GROUP BY customer_id
HAVING MAX(amount) > MIN(amount);

### 90. Find most recent order per customer
SELECT *
FROM (
    SELECT *,
    ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY order_date DESC) rn
    FROM orders
) t
WHERE rn = 1;

### 91. Find employees with no manager
SELECT *
FROM employees
WHERE manager_id IS NULL;

### 92. Find department with highest average salary
SELECT department
FROM employees
GROUP BY department
ORDER BY AVG(salary) DESC
LIMIT 1;

### 93. Find product return rate (simplified)
SELECT product_id,
SUM(CASE WHEN status = 'returned' THEN 1 ELSE 0 END) * 100.0 / COUNT(*) AS return_rate
FROM orders
GROUP BY product_id;

### 94. Find customers with highest order frequency
SELECT customer_id, COUNT(*) AS order_count
FROM orders
GROUP BY customer_id
ORDER BY order_count DESC
LIMIT 1;

### 95. Find employees earning top 10%
SELECT *
FROM employees e
WHERE salary >= (
    SELECT MIN(salary)
    FROM (
        SELECT salary
        FROM employees
        ORDER BY salary DESC
        LIMIT 10
    ) t
);

### 96. Find sales growth between two periods
SELECT 
SUM(CASE WHEN order_date < '2024-01-01' THEN amount ELSE 0 END) AS before,
SUM(CASE WHEN order_date >= '2024-01-01' THEN amount ELSE 0 END) AS after
FROM sales;

### 97. Find most common product category
SELECT category, COUNT(*) AS cnt
FROM products
GROUP BY category
ORDER BY cnt DESC
LIMIT 1;

### 98. Find customers who bought all products in a category
SELECT customer_id
FROM orders o
JOIN products p ON o.product_id = p.product_id
GROUP BY customer_id, category
HAVING COUNT(DISTINCT o.product_id) = (
    SELECT COUNT(*) FROM products WHERE category = p.category
);

### 99. Find employee tenure
SELECT employee_id,
DATEDIFF(CURRENT_DATE, hire_date) AS tenure_days
FROM employees;

### 100. Find revenue per day moving average (7-day)
SELECT date, amount,
AVG(amount) OVER (
    ORDER BY date
    ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
) AS moving_avg_7day
FROM sales;







