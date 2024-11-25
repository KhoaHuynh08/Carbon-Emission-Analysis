# Carbon-Emission-Analysis

## Data Structure
### Table product_emissions
```sql
SELECT * FROM product_emissions LIMIT 5;
```
| id           | company_id | country_id | industry_group_id | year | product_name                                                    | weight_kg | carbon_footprint_pcf | upstream_percent_total_pcf | operations_percent_total_pcf | downstream_percent_total_pcf | 
| -----------: | ---------: | ---------: | ----------------: | ---: | --------------------------------------------------------------: | --------: | -------------------: | -------------------------: | ---------------------------: | ---------------------------: | 
| 10056-1-2014 | 82         | 28         | 2                 | 2014 | Frosted Flakes(R) Cereal                                        | 0.7485    | 2                    | 57.50                      | 30.00                        | 12.50                        | 
| 10056-1-2015 | 82         | 28         | 15                | 2015 | "Frosted Flakes, 23 oz, produced in Lancaster, PA (one carton)" | 0.7485    | 2                    | 57.50                      | 30.00                        | 12.50                        | 
| 10222-1-2013 | 83         | 28         | 8                 | 2013 | Office Chair                                                    | 20.68     | 73                   | 80.63                      | 17.36                        | 2.01                         | 
| 10261-1-2017 | 14         | 16         | 25                | 2017 | Multifunction Printers                                          | 110       | 1488                 | 30.65                      | 5.51                         | 63.84                        | 
| 10261-2-2017 | 14         | 16         | 25                | 2017 | Multifunction Printers                                          | 110       | 1818                 | 25.08                      | 4.51                         | 70.41                        | 

### Product Produce the most to Carbon emission
```sql
SELECT 
	product_name, 
	ROUND(avg(carbon_footprint_pcf),2) AS Avg_pcf
FROM product_emissions 
GROUP BY product_name
ORDER BY avg(carbon_footprint_pcf) DESC
LIMIT 10;
```
| product_name                                                                                                                       | Avg_pcf    | 
| ---------------------------------------------------------------------------------------------------------------------------------: | ---------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | 3718044.00 | 
| Wind Turbine G132 5 Megawats                                                                                                       | 3276187.00 | 
| Wind Turbine G114 2 Megawats                                                                                                       | 1532608.00 | 
| Wind Turbine G90 2 Megawats                                                                                                        | 1251625.00 | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | 191687.00  | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | 167000.00  | 
| TCDE                                                                                                                               | 99075.00   | 
| Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | 91000.00   | 
| Mercedes-Benz S-Class (S 500)                                                                                                      | 85000.00   | 
| Mercedes-Benz SL (SL 350)                                                                                                          | 72000.00   |  
### Industry Groups of these product
```sql
SELECT 
	industry_group,
	product_name, 
	ROUND(avg(carbon_footprint_pcf),2) AS Avg_pcf
FROM product_emissions prd_em
JOIN industry_groups ind_gr 
	ON prd_em.industry_group_id = ind_gr.id 
GROUP BY product_name
ORDER BY avg(carbon_footprint_pcf) DESC
LIMIT 10;
```
| industry_group                     | product_name                                                                                                                       | Avg_pcf    | 
| ---------------------------------: | ---------------------------------------------------------------------------------------------------------------------------------: | ---------: | 
| Electrical Equipment and Machinery | Wind Turbine G128 5 Megawats                                                                                                       | 3718044.00 | 
| Electrical Equipment and Machinery | Wind Turbine G132 5 Megawats                                                                                                       | 3276187.00 | 
| Electrical Equipment and Machinery | Wind Turbine G114 2 Megawats                                                                                                       | 1532608.00 | 
| Electrical Equipment and Machinery | Wind Turbine G90 2 Megawats                                                                                                        | 1251625.00 | 
| Automobiles & Components           | Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | 191687.00  | 
| Materials                          | Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | 167000.00  | 
| Materials                          | TCDE                                                                                                                               | 99075.00   | 
| Automobiles & Components           | Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | 91000.00   | 
| Automobiles & Components           | Mercedes-Benz S-Class (S 500)                                                                                                      | 85000.00   | 
| Automobiles & Components           | Mercedes-Benz SL (SL 350)                                                                                                          | 72000.00   | 
