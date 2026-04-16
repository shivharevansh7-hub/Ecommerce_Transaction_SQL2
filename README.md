-- 5. Discount bucket analysis--
SELECT
    CASE
        WHEN discount_pct BETWEEN  0 AND  5 THEN '0-5%'
        WHEN discount_pct BETWEEN  5 AND 10 THEN '5-10%'
        WHEN discount_pct BETWEEN 10 AND 15 THEN '10-15% (Optimal)'
        WHEN discount_pct BETWEEN 15 AND 20 THEN '15-20%'
        WHEN discount_pct BETWEEN 20 AND 25 THEN '20-25%'
        ELSE '25-30%'
    END                          AS discount_range,
    COUNT(*)                     AS transactions,
    ROUND(AVG(units_sold), 2)    AS avg_units_sold,
    ROUND(AVG(profit_margin_pct),2) AS avg_margin_pct
FROM transactions
GROUP BY discount_range
ORDER BY discount_range;


 -- 4. Monthly trend--
SELECT month,
       COUNT(*)              AS txns,
       ROUND(SUM(revenue),2) AS revenue,
       ROUND(SUM(profit),2)  AS profit
FROM transactions
GROUP BY month
ORDER BY month;

-- Q2: Monthly Revenue and Profit Trends--
SELECT month,
    CASE 
        WHEN 1  THEN 'January'   WHEN 2  THEN 'February' WHEN 3  THEN 'March'
        WHEN 4  THEN 'April'     WHEN 5  THEN 'May'       WHEN 6  THEN 'June'
        WHEN 7  THEN 'July'      WHEN 8  THEN 'August'    WHEN 9  THEN 'September'
        WHEN 10 THEN 'October'   WHEN 11 THEN 'November'  WHEN 12 THEN 'December'
    END                                         AS month_name,
    COUNT(*)                                    AS transactions,
    SUM(units_sold)                             AS units_sold,
    ROUND(SUM(revenue), 2)                      AS revenue,
    ROUND(SUM(profit), 2)                       AS profit,
    ROUND(SUM(profit)/SUM(revenue)*100, 2)      AS profit_margin_pct,
    ROUND(AVG(discount_pct), 2)                 AS avg_discount_pct,
    ROUND(AVG(marketing_spend), 2)              AS avg_marketing_spend
FROM transactions
GROUP BY month
ORDER BY month;

