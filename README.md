# plsql-window-functions-Marthina_Huberthe-TSAMBA
# MySQL Window Functions Project

## Problem
T2000 Market wants to analyze sales performance and customer purchasing trends using MySQL window functions.

## Schema
**Customers**  
- customer_id (INT, PK)  
- name (VARCHAR)  
- contact (VARCHAR)  

**Products**  
- product_id (INT, PK)  
- name (VARCHAR)  
- category (VARCHAR)  
- price (DECIMAL)  

**Sales**  
- sale_id (INT, PK)  
- customer_id (INT, FK)  
- product_id (INT, FK)  
- quantity (INT)  
- sale_date (DATE)  

---

## Queries & Functions

1. **Top Customers by Sales**
```sql
SELECT customer_id, SUM(quantity*price) AS total_sales,
       RANK() OVER (ORDER BY SUM(quantity*price) DESC) AS rank
FROM sales
JOIN products USING(product_id)
GROUP BY customer_id;

2. **Cumulative Sales per Customer**
SELECT customer_id, sale_date,
       SUM(quantity*price) OVER(PARTITION BY customer_id ORDER BY sale_date) AS cumulative_sales
FROM sales
JOIN products USING(product_id);

3.**Moving Average of Daily Sales**
SELECT sale_date,
       AVG(quantity*price) OVER(ORDER BY sale_date ROWS BETWEEN 6 PRECEDING AND CURRENT ROW) AS moving_avg
FROM sales
JOIN products USING(product_id);



