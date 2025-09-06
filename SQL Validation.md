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
SELECT ROUND(AVG(`Profit_margin%`),2) AS `Avg_Profit_Margin%` FROM supply_chain_data;
```
| Avg_Profit_Margin% |
| -------------------- |
| 86.07          |

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
  ROUND(SUM(Revenue) *100 / (SELECT SUM(Revenue) FROM supply_chain_data),2) AS `Total_Revenue%`
FROM supply_chain_data GROUP BY Customer_demographics;
```
| Customer_demographics | Total_Revenue% |
| -------------------- | ---------------|
| Female | 39.85 | 
| Male | 60.15 | 

## Average Defect Rate % by Product Type
```sql
SELECT
  Product_type,
  ROUND(AVG(Defect_rates) * 100 / (SUM(AVG(Defect_rates)) OVER()) ,2) AS `Avg_defect_rates%`
FROM supply_chain_data GROUP BY Product_type;
```
| Product_type | Avg_defect_rates% |
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
  ROUND(AVG(Profit_margin),2) AS `Avg_profit_margin%`
FROM supply_chain_data GROUP BY Supplier_name ORDER BY `Avg_profit_margin%` DESC;
```
| Supplier_name | Avg_profit_margin% |
| -------------------- | ---------------|
| Supplier 3| 91.08| 
| Supplier 2| 87.24| 
| Supplier 5| 85.27| 
| Supplier 1| 84.16| 
| Supplier 4| 84.11| 

## Top 20 SKU by Order Quantities
```sql
SELECT
  SKU,
  SUM(Order_quantities) AS Order_quantities
FROM supply_chain_data GROUP BY SKU ORDER BY Order_quantities DESC
LIMIT 20;
```
| SKU | Order_quantities | SKU | Order_quantities |
| ------------- | ------------| ------------ | ------------|
| SKU0 | 96 | SKU43 | 85| 
| SKU90 | 96 | SKU88 | 85| 
| SKU33 | 95 | SKU9 | 83| 
| SKU19 | 94 | SKU56 | 83| 
| SKU38 | 88 | SKU50 | 82| 
| SKU2 | 88 | SKU84 | 80| 
| SKU12 | 85 | SKU10 | 80| 
| SKU91 | 85 | SKU14 | 78| 
| SKU35 | 85 | SKU16 | 78| 
| SKU17 | 85 | SKU72 | 77| 

## Top 20 SKU by Stock Levels
```sql
SELECT
  SKU,
  SUM(Stock_levels) AS Stock_levels
FROM supply_chain_data GROUP BY SKU ORDER BY Stock_levels DESC
LIMIT 20;
```
| SKU | Stock_levels | SKU | Stock_levels |
| ------------- | ------------| ------------ | ------------|
| SKU12 | 100 | SKU7 | 93| 
| SKU51 | 100 | SKU46 | 92 | 
| SKU59 | 100 | SKU89 | 90 | 
| SKU91 | 98 | SKU40 | 90 | 
| SKU55 | 97 | SKU92 | 90 | 
| SKU49 | 97 | SKU5 | 90 | 
| SKU77 | 96 | SKU32 | 89 |
| SKU53 | 96 | SKU62 | 86 | 
| SKU69 | 95 | SKU23 | 84 |
| SKU45 | 93 | SKU25 | 82 | 

## Top 20 SKU by Lead Time and Manifacturing Lead Time
```sql
SELECT
  SKU,
  SUM(Mfg_lead_time) AS Mfg_lead_time,
  SUM(Lead_time) AS Lead_time
FROM supply_chain_data GROUP BY SKU ORDER BY Mfg_lead_time DESC
LIMIT 20;
```
| SKU | Mfg_lead_time | Lead_time | SKU | Mfg_lead_time | Lead_time |
| ---------- | ------------| ------------ | ------------| ------------ | ------------|
| SKU1 | 30 | 23 | SKU66 | 28 | 24 |
| SKU30 | 30 | 27 | SKU49 | 28 | 28 |
| SKU0 | 29 | 29 | SKU22 | 28 | 22 | 
| SKU23|  29 | 11 | SKU52 | 27 | 10 | 
| SKU92 | 29 | 4 | SKU2 | 27 | 12 | 
| SKU54 | 29 | 26 | SKU82 | 26 | 6 |
| SKU91 | 28 | 5 | SKU95 | 26 | 18 |
| SKU96 | 28 | 28 | SKU45 | 25 | 25 | 
| SKU51 | 28 | 18 | SKU57 | 25|  21 |
| SKU56 | 28 | 24 | SKU60 | 24 | 29 | 
 
## Average Profit Margin % by Product Type
```sql
SELECT
  Product_type,
  ROUND(AVG(`Profit_margin%`) * 100 / (SUM(AVG(`Profit_margin%`)) OVER()) ,2) AS `Avg_profit_margin%`
FROM supply_chain_data GROUP BY Product_type;
```
| Product_type | Avg_profit_margin% |
| -------------------- | ---------------|
| cosmetics | 33.76| 
| haircare| 32.98| 
| skincare| 33.26|

## Total Costs % by Transportation Modes
```sql
SELECT
  Transportation_modes,
  ROUND((SUM(Costs)+SUM(Mfg_costs)+SUM(Shipping_costs)) * 100 / (SUM((SUM(Costs)+SUM(Mfg_costs)+SUM(Shipping_costs))) OVER()) ,2) AS `Total_costs%`
FROM supply_chain_data GROUP BY Transportation_modes;
```
| Transportation_modes | Total_costs% |
| -------------------- | ---------------|
| Air | 27.25 | 
| Rail | 28.71 | 
| Road | 30.52 | 
| Sea | 13.52 | 

## Average Defect Rate % by Transportation Modes
```sql
SELECT
  Transportation_modes,
  ROUND(AVG(Defect_rates) * 100 / (SUM(AVG(Defect_rates)) OVER()) ,2) AS `AVG_defect_rates%`
FROM supply_chain_data GROUP BY Transportation_modes;
```
| Transportation_modes | AVG_defect_rates% |
| -------------------- | ---------------|
| Air | 20.09 | 
| Rail | 25.54 | 
| Road | 28.87 | 
| Sea | 25.50 | 

## Stock Level by Supplier Name
```sql
SELECT
  Supplier_name,
  ROUND(SUM(Costs),2) AS Total_costs,
  ROUND(SUM(Shipping_costs),2) AS Total_shipping_costs,
  ROUND(SUM(Mfg_costs),2) AS Total_mfg_costs
FROM supply_chain_data GROUP BY Supplier_name ORDER BY Total_costs DESC;
```
| Supplier_name | Total_costs | Total_shipping_costs | Total_mfg_costs
| --------------- | ---------------| ---------------| ---------------|
| Supplier 1 | 15520.98 | 148.83 | | 
| Supplier 2 | 11330.60 | 126.26 | | 
| Supplier 5 | 9648.41 | 104.22 | | 
| Supplier 4 | 9392.59 | 103.67 | | 
| Supplier 3 | 7032.00 | 71.83 | |

## Stock Level by Supplier Name
```sql
SELECT
  Supplier_name,
  SUM(Stock_levels) AS Stock_levels
FROM supply_chain_data GROUP BY Supplier_name ORDER BY Stock_levels ASC;
```
| Supplier_name | Stock_levels |
| -------------------- | ---------------|
| Supplier 3| 654| 
| Supplier 5| 898| 
| Supplier 2| 1022| 
| Supplier 4| 1061| 
| Supplier 1| 1142| 
