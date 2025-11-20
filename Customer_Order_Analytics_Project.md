# Customer Order Analytics System — PostgreSQL, API Integration & Power BI

A real-time mini project that combines API integration, PostgreSQL SQL skills, Postman testing, and a Power BI dashboard. Designed to look professional for Cognizant GenC.

## Project Overview
- Build a small customer orders platform backed by PostgreSQL
- Expose basic REST APIs to insert and fetch data
- Validate APIs with Postman, then analyze with SQL
- Create an insights dashboard in Power BI (direct query/import)

## Tech Stack
- Database: PostgreSQL
- API: REST (Node/Express or Python/FastAPI – any is fine)
- Testing: Postman
- Analytics: SQL queries
- Visualization: Power BI

## Your Role (what you did)
- Wrote PostgreSQL DDL and DML for core tables
- Designed SQL analytics queries for KPIs
- Tested API endpoints with Postman
- Modeled data in Power BI and built a dashboard

## Architecture (data flow)
API → PostgreSQL (tables: customers, products, orders, order_items) → SQL analytics → Power BI dashboard

## Real-time SQL Use Cases
- Order volume by month and by product
- Revenue and average order value (AOV)
- Top customers and repeat purchase rate
- Category performance and best-selling items

## Challenges & Solutions
- Data consistency: used foreign keys and explicit statuses
- Slow queries: added indexes on common filters (date, customer)
- API validation: tested edge cases with Postman examples

## API Endpoints (tested via Postman)
- `POST /orders` — create an order with items
- `GET /orders?from=YYYY-MM-DD&to=YYYY-MM-DD` — list orders
- `GET /analytics/top-customers?limit=10` — top customers by revenue
- Variables (Postman): `{{baseUrl}}`, `{{apiKey}}` (if auth is required)

## Power BI Data Model
- Import tables from PostgreSQL (or DirectQuery)
- Relationships: customers→orders (1:N), orders→order_items (1:N), products→order_items (1:N)
- Measures: Total Revenue, AOV, Orders per Customer, Monthly Revenue
- Visuals: KPI cards, clustered bar, line by month, table of top customers

## SQL Scripts (attached in /sql)
- `schema.sql` — CREATE TABLE with keys and indexes
- `sample_data.sql` — small dataset for demo
- `analytics_queries.sql` — joins, aggregations, and KPIs

## Screenshots (placeholders to add)
- Postman: success response for `POST /orders`
- Power BI: dashboard overview and monthly revenue
- SQL: result preview for Top Customers query

## How to Use This Single Doc
- Copy this entire file into Google Docs
- Format headings if needed
- Insert your own screenshots where noted
- Download as PDF and attach to your application

---

# Appendix: Quick SQL Snippets

### Example: Monthly Revenue
```sql
SELECT DATE_TRUNC('month', o.order_date) AS month,
       SUM(oi.quantity * oi.unit_price) AS revenue
FROM orders o
JOIN order_items oi ON oi.order_id = o.order_id
GROUP BY 1
ORDER BY 1;
```

### Example: Top Customers by Revenue
```sql
SELECT c.customer_id, c.full_name,
       SUM(oi.quantity * oi.unit_price) AS total_revenue
FROM customers c
JOIN orders o ON o.customer_id = c.customer_id
JOIN order_items oi ON oi.order_id = o.order_id
GROUP BY 1,2
ORDER BY total_revenue DESC
LIMIT 10;
```

### Example: Repeat Customers
```sql
SELECT c.customer_id, c.full_name,
       COUNT(DISTINCT o.order_id) AS order_count
FROM customers c
JOIN orders o ON o.customer_id = c.customer_id
GROUP BY 1,2
HAVING COUNT(DISTINCT o.order_id) >= 2
ORDER BY order_count DESC;
```

---

# Google Drive Steps (to share both PDF + Google Doc)
- Create a new Google Doc and paste this content
- File → Download → `PDF Document (.pdf)` for the PDF version
- File → Share → `Anyone with the link` → Viewer to generate public link
- Paste the Google Doc link in Cognizant form; attach the PDF as requested

# Postman Collection (attached in /postman)
Import the JSON file and set `{{baseUrl}}` and optional `{{apiKey}}`. Use sample bodies to create and fetch orders.

# Notes
- You can implement the API in any language; focus on SQL correctness
- Replace placeholder screenshots with your real Postman/Power BI/SQL outputs