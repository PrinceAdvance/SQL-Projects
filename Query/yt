# SQL Practice Queries 📊

A comprehensive collection of SQL practice problems covering fundamental to intermediate concepts including aggregations, joins, window functions, and CTEs.

## 📋 Table of Contents

| Question | Description | Concepts |
|----------|-------------|----------|
| [Q1](#q1-find-total-sales-revenue-per-order) | Find total sales revenue per order | Basic SELECT, Arithmetic |
| [Q2](#q2-get-total-revenue-per-category) | Get total revenue per category | GROUP BY, SUM |
| [Q3](#q3-find-customers-who-placed-more-than-1-order) | Find customers with multiple orders | GROUP BY, HAVING |
| [Q4](#q4-find-the-most-expensive-single-product-sold) | Find the most expensive product | MAX, LIMIT |
| [Q5](#q5-find-total-revenue-for-january-8-2024) | Revenue for specific date | WHERE, Date filtering |
| [Q6](#q6-show-the-number-of-orders-per-day) | Count orders by date | COUNT, GROUP BY |
| [Q7](#q7-show-total-quantity-sold-for-each-product) | Product quantity analysis | SUM, ORDER BY |
| [Q8](#q8-find-distinct-product-categories) | List unique categories | DISTINCT |
| [Q9](#q9-find-orders-with-revenue-greater-than-500) | Filter high-value orders | WHERE conditions |
| [Q10](#q10-find-the-cheapest-product-sold) | Find lowest priced product | ORDER BY ASC, LIMIT |
| [Q11](#q11-show-total-revenue-per-customer-with-names) | Customer revenue with names | JOIN, GROUP BY |
| [Q12](#q12-find-the-first-order-date-for-each-customer) | Customer first order analysis | MIN, GROUP BY |
| [Q13](#q13-show-cumulative-revenue-per-day) | Running revenue totals | Window Functions, SUM OVER |
| [Q14](#q14-find-the-top-selling-product-in-each-category) | Top product per category | CTE, RANK, Window Functions |
| [Q15](#q15-show-orders-from-new-customers) | Orders from customers who joined after Jan 1, 2024 | JOIN, Date filtering |
| [Q16](#q16-find-revenue-split-between-categories) | Revenue comparison between categories | CASE WHEN, Conditional SUM |
| [Q17](#q17-find-customers-who-never-bought-electronics) | Customers excluding specific category | NOT IN, Subqueries |

## 📚 Prerequisites

- Basic understanding of SQL syntax
- Knowledge of relational database concepts
- Familiarity with tables: `sales_data`, `customers_data`

## 🗄️ Database Schema

### Sales Table Structure
```sql
sales_data (
    order_id,
    customer_id,
    product,
    category,
    quantity,
    price_per_unit,
    order_date
)
```

### Customers Table Structure
```sql
customers_data (
    customer_id,
    customer_name,
    join_date
)
```

---

## Questions and Solutions

### Q1. Find total sales revenue per order
**Scenario:** You want to calculate the total money earned for each order (quantity × price_per_unit).

**Concepts:** Basic arithmetic, SELECT statement

```sql
SELECT 
    order_id,
    quantity * price_per_unit AS total_revenue
FROM sales;
```

---

### Q2. Get total revenue per category
**Scenario:** Management wants to know how much each product category earned in total.

**Concepts:** GROUP BY, SUM aggregation

```sql
SELECT 
    category,
    SUM(quantity * price_per_unit) AS revenue
FROM sales_schema.`sales_data (1)`
GROUP BY category;
```

---

### Q3. Find customers who placed more than 1 order
**Scenario:** The marketing team wants to target repeat customers.

**Concepts:** GROUP BY, HAVING clause, COUNT

```sql
SELECT
    customer_id,
    COUNT(order_id) AS order_count
FROM sales_schema.`sales_data (1)`
GROUP BY customer_id
HAVING COUNT(order_id) > 1;
```

---

### Q4. Find the most expensive single product sold
**Scenario:** You need to know which product had the highest price_per_unit.

**Concepts:** MAX function, LIMIT, ORDER BY

```sql
-- Method 1: Using MAX with GROUP BY
SELECT 
    product,
    MAX(price_per_unit) AS highest_price
FROM sales_schema.`sales_data (1)`
GROUP BY product
ORDER BY highest_price DESC
LIMIT 1;

-- Method 2: Using ORDER BY DESC
SELECT 
    product,
    price_per_unit
FROM sales_schema.`sales_data (1)`
ORDER BY price_per_unit DESC
LIMIT 1;
```

---

### Q5. Find total revenue for January 8, 2024
**Scenario:** A special campaign ran on Jan 8. You need total revenue for that date.

**Concepts:** WHERE clause, date filtering, SUM

```sql
SELECT 
    order_date,
    SUM(quantity * price_per_unit) AS total_revenue
FROM sales
WHERE order_date = '2024-01-08'
GROUP BY order_date;
```

---

### Q6. Show the number of orders per day
**Scenario:** Management wants to see how many orders were placed each day.

**Concepts:** COUNT, GROUP BY, ORDER BY

```sql
SELECT 
    order_date,
    COUNT(order_id) AS order_count
FROM sales_schema.`sales_data (1)`
GROUP BY order_date
ORDER BY order_date;
```

---

### Q7. Show total quantity sold for each product
**Scenario:** You want to know which products sell the most in terms of quantity.

**Concepts:** SUM, GROUP BY, ORDER BY DESC

```sql
SELECT
    product,
    SUM(quantity) AS total_quantities
FROM sales_schema.`sales_data (1)`
GROUP BY product
ORDER BY total_quantities DESC;
```

---

### Q8. Find distinct product categories
**Scenario:** You want a simple list of all categories available in the sales table.

**Concepts:** DISTINCT keyword

```sql
SELECT DISTINCT category
FROM sales_schema.`sales_data (1)`;
```

---

### Q9. Find orders with revenue greater than 500
**Scenario:** The finance team wants to see only big-ticket orders.

**Concepts:** WHERE clause with calculated fields

```sql
SELECT
    order_id,
    quantity * price_per_unit AS revenue
FROM sales_schema.`sales_data (1)`
WHERE (quantity * price_per_unit) > 500;
```

---

### Q10. Find the cheapest product sold
**Scenario:** The procurement team wants to know the lowest price_per_unit item.

**Concepts:** ORDER BY ASC, LIMIT

```sql
SELECT 
    product,
    price_per_unit
FROM sales
ORDER BY price_per_unit ASC
LIMIT 1;
```

---

### Q11. Show total revenue per customer with names
**Scenario:** Management wants to see each customer's name and their total revenue.

**Concepts:** JOIN, GROUP BY, SUM

```sql
SELECT  
    c.customer_name,
    SUM(s.quantity * s.price_per_unit) AS total_revenue
FROM sales_schema.`sales_data (1)` s
JOIN sales_schema.customers_data c
    ON s.customer_id = c.customer_id
GROUP BY c.customer_name
ORDER BY total_revenue DESC;
```

---

### Q12. Find the first order date for each customer
**Scenario:** You want to know when each customer placed their first order.

**Concepts:** MIN function, GROUP BY

```sql
SELECT
    customer_id,
    MIN(order_date) AS first_order
FROM sales_schema.`sales_data (1)`
GROUP BY customer_id;
```

---

### Q13. Show cumulative revenue per day
**Scenario:** Management wants a running total of revenue by date to track growth over time.

**Concepts:** Window functions, SUM OVER, cumulative calculations

```sql
SELECT 
    order_date,
    SUM(quantity * price_per_unit) AS daily_revenue,
    SUM(SUM(quantity * price_per_unit)) OVER (
        ORDER BY order_date
    ) AS cumulative_revenue
FROM sales_schema.`sales_data (1)`
GROUP BY order_date
ORDER BY order_date;
```

---

### Q14. Find the top-selling product in each category
**Scenario:** You want the product with the highest total quantity sold within each category.

**Concepts:** CTE (Common Table Expression), RANK window function, PARTITION BY

```sql
WITH product_totals AS (
    SELECT
        category,
        product,
        SUM(quantity) AS total_quantity
    FROM sales_schema.`sales_data (1)`
    GROUP BY category, product
)
SELECT
    category,
    product,
    total_quantity
FROM (
    SELECT
        category,
        product,
        total_quantity,
        RANK() OVER (PARTITION BY category ORDER BY total_quantity DESC) AS rnk
    FROM product_totals
) ranked
WHERE rnk = 1;
```

---

### Q15. Show orders from new customers
**Scenario:** The marketing team is studying the behavior of customers who joined after Jan 1, 2024.

**Concepts:** JOIN, WHERE with date conditions

```sql
SELECT 
    s.order_id,
    s.order_date,
    c.customer_name,
    c.join_date
FROM sales_schema.`sales_data (1)` s
JOIN sales_schema.customers_data c
    ON s.customer_id = c.customer_id
WHERE c.join_date > '2024-01-01';
```

---

### Q16. Find revenue split between categories
**Scenario:** Management wants to see total revenue for Electronics vs Furniture in one row.

**Concepts:** CASE WHEN, conditional aggregation

```sql
SELECT 
    SUM(CASE WHEN category = 'Electronics' THEN quantity * price_per_unit ELSE 0 END) AS electronics_revenue,
    SUM(CASE WHEN category = 'Furniture' THEN quantity * price_per_unit ELSE 0 END) AS furniture_revenue
FROM sales_schema.`sales_data (1)`;
```

---

### Q17. Find customers who never bought Electronics
**Scenario:** The marketing team wants to identify customers who only bought Furniture.

**Concepts:** NOT IN, subqueries, exclusion logic

```sql
-- Method 1: Show customers with their non-Electronics purchases
SELECT
    s.customer_id,
    c.customer_name,
    s.category
FROM sales_schema.`sales_data (1)` s 
JOIN sales_schema.customers_data c 
    ON s.customer_id = c.customer_id
WHERE s.category != 'Electronics';

-- Method 2: Customers who never bought Electronics
SELECT 
    c.customer_name
FROM sales_schema.customers_data c
WHERE c.customer_id NOT IN (
    SELECT DISTINCT customer_id
    FROM sales_schema.`sales_data (1)`
    WHERE category = 'Electronics'
);
```

---

## 🎯 Key Learning Outcomes

After completing these exercises, you'll have practiced:

- **Basic SQL Operations**: SELECT, WHERE, ORDER BY, LIMIT
- **Aggregation Functions**: SUM, COUNT, MAX, MIN
- **Grouping and Filtering**: GROUP BY, HAVING
- **Table Joins**: INNER JOIN for combining related data
- **Window Functions**: Ranking and cumulative calculations
- **Advanced Techniques**: CTEs, CASE statements, subqueries
- **Date Operations**: Filtering and comparing dates
- **Conditional Logic**: CASE WHEN for conditional aggregations

## 🚀 Next Steps

1. Try modifying these queries with different conditions
2. Experiment with additional aggregate functions (AVG, STDDEV)
3. Practice with LEFT/RIGHT JOINs
4. Explore more complex window functions (LAG, LEAD, NTILE)
5. Work with real datasets to apply these concepts

## 📝 Contributing

Feel free to submit additional practice problems or improvements to existing queries via pull requests!
