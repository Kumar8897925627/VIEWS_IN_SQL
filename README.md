# VIEWS_IN_SQL
This project demonstrates the power of SQL Views in relational databases using practical examples based on Customer and Orders tables. It covers all 4 types of views — Simple, Complex, Materialized, and Inline — along with real-time use cases for abstraction, data security, performance optimization, and business insights.

# Objectives

✔ Apply complex SELECT queries to create analytical views
✔ Use views for data abstraction, restricted access & role-based security
✔ Generate customer purchase insights using aggregation, joins & CASE logic
✔ Implement materialized views for performance optimization
✔ Use inline views for temporary subqueries inside SELECT

# Types of SQL Views Covered
View Type	Description	Use Case
Simple View	Based on single table	Restricted data access
Complex View	Uses joins, aggregation, CASE	Business insights, reporting
Materialized View	Stored physically, faster retrieval	BI dashboards, analytics
Inline View	Subquery inside SELECT	Temporary analysis


├── customer_orders_schema.sql      -- Master & child table creation
├── view_simple_customer.sql        -- Simple View
├── view_customer_analysis.sql      -- Complex Analytical View
├── view_secure_customer.sql        -- Restricted Masked View
├── mv_customer_sales.sql           -- Materialized View
├── inline_view_sales.sql           -- Inline View example
├── README.md                       -- Project documentation

# USED FOR BUSINESS LOGICS
CREATE OR REPLACE VIEW vw_customer_order_analysis AS
SELECT 
    c.customer_id,
    c.customer_name,
    c.city,
    SUM(o.order_amount) AS total_spent,
    CASE
        WHEN SUM(o.order_amount) > 5000 THEN 'Platinum'
        WHEN SUM(o.order_amount) BETWEEN 2000 AND 5000 THEN 'Gold'
        ELSE 'Silver'
    END AS customer_category
FROM customer c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.customer_name, c.city;
