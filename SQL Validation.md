Data validation using SQL aims to ensure that the values displayed on the dashboard are accurate and correct. I use SQL Database Management to validation my own dashboard.

## Total Revenue
```sql
SELECT SUM(Revenue) AS Total_Revenue FROM supply_chain_data;
```
| Total_Revenue |
| -------------------- |
| 577604.818740             |

## Total Product Sold
```sql
SELECT SUM(Products_sold) AS Total_Product_Sold FROM supply_chain_data;
```
| Total_Product_Sold |
| -------------------- |
| 46099             |

## Total Costs
```sql
SELECT SUM(Costs)+SUM(Shipping_costs)+SUM(Mfg_costs) AS Total_Costs FROM supply_chain_data;
```
| Total_Costs |
| -------------------- |
| 52924.5782154             |

## Average Profit Margin (%)
```sql
SELECT AVG(Profit_margin%) AS Avg_Profit_Margin% FROM supply_chain_data;
```
| Avg_Profit_Margin% |
| -------------------- |
| 4.35956            |

## Stock Level
```sql
SELECT SUM(Stock_levels) AS Stock_Levels FROM supply_chain_data;
```
| Stock_Levels |
| -------------------- |
| 4777             |

## Order Quantity
```sql
SELECT SUM(Order_quantities) AS Order_Quantities FROM supply_chain_data;
```
| Order_Quantities |
| -------------------- |
| 4922            |

## Average Quantity Per Order
```sql
SELECT AVG(transaction_qty) AS Avg_Qty_Per_Order FROM coffee_sales;
```
| Avg_Qty_Per_Order |
| -------------------- |
| 1.4487           |

## Daily Trend for Total Orders
```sql
SELECT
  day AS Day,
  SUM(transaction_qty) AS Total_Orders
FROM coffee_sales GROUP BY day;
```
| Day | Total_Orders |
| -------------------- | -------------------- |
| Sunday	| 29627  |
| Monday	| 30715 |
| Tuesday	| 29882 |
| Wednesday	| 30051 |
| Thursday	| 30659 |
| Friday	| 30639 |
| Saturday	| 29083 |

## Hourly Trend for Total Orders
```sql
SELECT
  hour AS Hour,
  SUM(transaction_qty) AS Total_Orders
FROM coffee_sales GROUP BY hour;
```
| Hour | Total_Orders |
| -------------------- | -------------------- |
| 6	| 6726 |
| 7	| 19044 |
| 8	| 24675 |
| 9	| 24715 |
| 10	| 26089 |
| 11	| 13835 |
| 12	| 12553 |
| 13	| 12272 |
| 14	| 12748 |
| 15	| 12753 |
| 16	| 12689 |
| 17	| 12554 |

## Sales by Store Location
```sql
SELECT
  store_location AS Store_Location,
  SUM(total_bill) AS Total_Revenue
FROM coffee_sales GROUP BY store_location;
```
| Store_Location | Total_Revenue |
| -------------------- | -------------------- |
| Astoria	| 213373.71 |
| Hell's Kitchen	| 211472.72 |
| Lower Manhattan	| 209060.05 |

## Sales by Product Category
```sql
SELECT
  product_category AS Product_Category,
  SUM(total_bill) AS Total_Revenue
FROM coffee_sales GROUP BY product_category;
```
| Product_Category | Total_Revenue |
| -------------------- | -------------------- |
| Bakery	| 82315.64 |
| Chocolate	| 76823.64 |
| Coffee	| 269952.45 |
| Syrup	| 8408.8 |
| Tea	| 196405.95 |

## Total Orders by Size
```sql
SELECT
  size AS Size_Product,
  SUM(transaction_qty) AS Total_Orders
FROM coffee_sales GROUP BY size;
```
| Size_Product | Total_Orders |
| -------------------- | -------------------- |
| Large	| 82951 |
| Regular	| 91887 |
| Small	| 35818 |

## Top 5 Best Seller by Total Orders
```sql
SELECT
  product_detail AS Product_Detail,
  SUM(transaction_qty) AS Total_Orders
FROM coffee_sales GROUP BY product_detail
ORDER BY Total_Orders DESC
LIMIT 5;
```
| Product_Detail | Total_Orders |
| -------------------- | -------------------- |
| Ethiopia| 13053 |
| Brazilian| 13012 |
| Columbian Medium Roast| 12920 |
| Our Old Time Diner Blend| 12891 |
| Jamaican Coffee River| 12431 |

## Bottom 5 Best Seller by Total Orders
```sql
SELECT
  product_detail AS Product_Detail,
  SUM(transaction_qty) AS Total_Orders
FROM coffee_sales GROUP BY product_detail
ORDER BY Total_Orders ASC
LIMIT 5;
```
| Product_Detail | Total_Orders |
| -------------------- | -------------------- |
| Chili Mayan	| 148 |
| Oatmeal Scone	| 1820 |
| Ginger Biscotti	| 1836 |
| Almond Croissant	| 1911 |
| Chocolate Chip Biscotti	| 1924 |
