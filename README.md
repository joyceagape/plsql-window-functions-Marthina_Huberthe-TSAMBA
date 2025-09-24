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

