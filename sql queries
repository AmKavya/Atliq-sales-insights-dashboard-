-- 1. Data Exploration & Quality Checks
SELECT * FROM sales.market;
SELECT * FROM sales.transactions;
SELECT COUNT(*) FROM sales.customers;
SELECT DISTINCT product_code FROM sales.transactions WHERE market_code = 'Mark001';

-- 2. Transaction Analysis by Market
SELECT market_code, COUNT(*) as cnt FROM sales.transactions GROUP BY market_code;

-- 3. Count customers and check unique values
SELECT COUNT(*) FROM sales.customers;
SELECT COUNT(DISTINCT customer_name) FROM sales.customers;

-- 4. Date Table summary
SELECT year, COUNT(*) AS total_dates FROM sales.date GROUP BY year;

-- 5. Transactions per month per year
SELECT year, month_name, COUNT(*) AS transactions_count
FROM sales.date AS dt JOIN sales.transactions tr ON tr.order_date = dt.date
GROUP BY dt.year, dt.month_name;

-- 6. Revenue aggregation and quantity sum
SELECT d.year, m.market_name, SUM(tr.sales_amount) AS total_revenue, SUM(tr.sales_qty) AS total_qty
FROM sales.transactions tr
JOIN sales.markets m ON tr.market_code = m.market_code
JOIN sales.date d ON tr.order_date = d.date
GROUP BY d.year, m.market_name
ORDER BY d.year, total_revenue DESC;

-- 7. Currency consistency check
SELECT DISTINCT(currency), COUNT(*) FROM sales.transactions GROUP BY currency;

-- 8. Identifying problematic values
SELECT * FROM sales.transactions WHERE sales_amount <=0;
SELECT * FROM sales.transactions WHERE product_code IS NULL OR product_code = '';

-- 9. Top Customers / Top Products by revenue
SELECT customer_code, SUM(sales_amount) AS total_revenue
FROM sales.transactions
GROUP BY customer_code
ORDER BY total_revenue DESC
LIMIT 5;

SELECT product_code, SUM(sales_amount) AS prod_revenue
FROM sales.transactions
GROUP BY product_code
ORDER BY prod_revenue DESC
LIMIT 5;
