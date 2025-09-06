Data validation using SQL aims to ensure that the values displayed on the dashboard are accurate and correct. I use SQL Database Management to validation my own dashboard.

## Total Revenue
```sql
SELECT ROUND(SUM(Revenue),2) AS Total_Revenue FROM supply_chain_data;
```
| Total_Revenue |
| -------------------- |
| 577604.82           |

## Total Product Sold
```sql
SELECT SUM(Products_sold) AS Total_Product_Sold FROM supply_chain_data;
```
| Total_Product_Sold |
| -------------------- |
| 46099             |

## Total Costs
```sql
SELECT ROUND(SUM(Costs)+SUM(Shipping_costs)+SUM(Mfg_costs),2) AS Total_Costs FROM supply_chain_data;
```
| Total_Costs |
| -------------------- |
| 52924.5782154             |

## Average Profit Margin (%)
```sql
SELECT ROUND(AVG(Profit_margin%),2) AS Avg_Profit_Margin% FROM supply_chain_data;
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

## Total Revenue % by Customer Demographics
```sql
SELECT
  Customer_demographics,
  ROUND(SUM(Revenue) *100 / (SELECT SUM(Revenue) FROM supply_chain_data),2) AS Total_Revenue
FROM supply_chain_data GROUP BY Customer_demographics;
```
| Customer_demographics | Total_Revenue |
| -------------------- | ---------------|
| Female | 39.85 | 
| Male | 60.15 | 

## Average Defect Rate % by Product Type
```sql
SELECT
  Product_type,
  ROUND(AVG(Defect_rates) * 100 / (SUM(AVG(Defect_rates)) OVER()) ,2) AS Avg_defect_rates
FROM supply_chain_data GROUP BY Product_type;
```
| Product_type | Avg_defect_rates |
| -------------------- | ---------------|
| cosmetics | 28.49| 
| haircare| 36.86| 
| skincare| 34.65| 

## Total Revenue by Product Type
```sql
SELECT
  Product_type,
  ROUND(SUM(Revenue),2) AS Total_Revenue
FROM supply_chain_data GROUP BY Product_type ORDER BY Total_Revenue DESC;
```
| Product_type | Total_Revenue |
| -------------------- | ---------------|
| cosmetics | 161521.27 | 
| haircare | 174455.39 | 
| skincare | 241628.16 | 

## Top 5 SKU by Total Revenue
```sql
SELECT
  SKU,
  ROUND(SUM(Revenue),2) AS Total_Revenue
FROM supply_chain_data GROUP BY SKU ORDER BY Total_Revenue DESC
LIMIT 5;
```
| SKU | Total_Revenue |
| -------------------- | ---------------|
| SKU51| 9866.47| 
| SKU38| 9692.32| 
| SKU31| 9655.14| 
| SKU90| 9592.63| 
| SKU2| 9577.75| 

## Total Revenue by Shipping Carriers
```sql
SELECT
  Shipping_carriers,
  ROUND(SUM(Revenue),2) AS Total_Revenue
FROM supply_chain_data GROUP BY Shipping_carriers;
```
| Shipping_carriers | Total_Revenue |
| -------------------- | ---------------|
| Carrier A| 142629.99| 
| Carrier B| 250094.65| 
| Carrier C| 184880.18|

## Average Profit Margin % by Supplier Name
```sql
SELECT
  Supplier_name,
  ROUND(AVG(Profit_margin),2) AS Avg_profit_margin
FROM supply_chain_data GROUP BY Supplier_name ORDER BY Avg_profit_margin DESC;
```
| Supplier_name | Avg_profit_margin |
| -------------------- | ---------------|
| Supplier 3| 91.08| 
| Supplier 2| 87.24| 
| Supplier 5| 85.27| 
| Supplier 1| 84.16| 
| Supplier 4| 84.11| 
