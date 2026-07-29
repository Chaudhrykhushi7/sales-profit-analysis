-- Sub-question 1: Which Category/Sub-Category generate the highest profit, and which are losing money?
SELECT category, sub_category, SUM(profit) AS total_profit
FROM orders
GROUP BY category, sub_category
ORDER BY total_profit DESC;

-- Sub-question 2: Which Region generates the highest and lowest profit?
SELECT region, SUM(profit) AS total_profit
FROM orders
GROUP BY region
ORDER BY total_profit DESC;

-- Sub-question 3: Does higher discount actually result in lower profit?
SELECT
  CASE
    WHEN discount = 0 THEN 'No Discount'
    WHEN discount <= 0.2 THEN 'Low (0-20%)'
    WHEN discount <= 0.4 THEN 'Medium (20-40%)'
    ELSE 'High (40%+)'
  END AS discount_range,
  SUM(profit) AS total_profit,
  ROUND(AVG(profit)::numeric, 2) AS avg_profit_per_order
FROM orders
GROUP BY discount_range
ORDER BY total_profit DESC;