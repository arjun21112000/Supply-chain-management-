Introduction 
Welcome to the AI Variant Data Analyst Internship Project: Supply Chain Management Project! This project was completed during an internship at AI Variant as part of the Data Analyst course at ExcelR. The project involves the analysis of Supply Chain data and the creation of interactive dashboards using tools like Excel, Tableau, and SQL. The datasets used are Product_data, Store, Inventory, customers,  sales and Point_of_sales  each containing between 200 to 100000+ records 
## Dashboard Creation

### Excel Dashboard
The Excel dashboard serves as a quick-access platform for visualising crucial financial insights from the supply chain data. It is designed with a clean and organised layout that prioritises clarity and comprehension. 
The dashboard utilises various data visualisation components such as pie chart ,stacked area-clustered column chart,, line graphs, and PivotTables to represent key performance indicators (KPIs) such as month wise sales trend, orders by region , sales and profit by region .it offers year and region filters as well.

![EXCEL DASHBOARD ](https://github.com/arjun21112000/Supply-chain-management-/assets/159052306/cd2b36ec-5d1d-4e9d-817c-17c92b0f4be4)




### Tableau Dashboard
The Tableau dashboard provides an interactive platform for in-depth analysis of supply chain data, facilitating a deeper understanding of Customer behaviours and patterns. Its design follows a clean and modern approach, with visuals strategically positioned for a cohesive data exploration experience. The dashboard integrates a variety of data visualisation components, including pie chart, bar charts, and line graph, to depict KPIs such as Top 10 store sales wise, region wise and brand wise sales . 

![TABLEAU DASHBOARD ](https://github.com/arjun21112000/Supply-chain-management-/assets/159052306/b5b3703c-fd15-4782-9714-73d5fb2b6199)



Users can interact with filters to dynamically adjust visualisations, and hovering over data points reveals detailed tooltips that enhance user comprehension. Dashboard actions and filters, such as filter actions , enable users to explore correlations and details by interacting with one visualisation to affect others.



## SQL Queries and Data Analysis

### Purpose of SQL Queries

SQL queries played a crucial role in deriving valuable insights from the supply chain datasets, enabling the extraction and transformation for actionable insight.

## Query 1: REGION WISE SALES

**SQL Query:**

```
     SELECT 
    		ROUND(SUM(PS.SALES_AMOUNT)/1000000,2) AS TOTAL_SALE_IN_MILLIONS,
    		SE.STORE_REGION
     from
    		supply_chain.Point_of_sales as PS
     INNER JOIN 
		supply_chain.Sales as S ON
    		PS.ORDER_NUMBER = S.ORDER_NUMBER
     INNER JOIN 
		supply_chain.Store as SE ON 
   		 S.STORE_KEY = SE.STORE_KEY
     GROUP BY 
		SE.STORE_REGION;
```

**SQL Query Output:**

![REGION WISE SALE](https://github.com/arjun21112000/Supply-chain-management-/assets/159052306/0f92cbed-e4ba-4df1-805d-62c6059510b9)


## Query 2: TOTAL PROFIT
**SQL Query:**
```
     SELECT
    		ROUND(SUM(TOTAL_SALE - Monthly_Rent_Cost)/1000000,1)AS Total_profit
     FROM (

     	SELECT
        		SUM(F.SALES_AMOUNT - F.COST_AMOUNT) AS TOTAL_SALE,
        		SE.Monthly_Rent_Cost

   	 FROM
       		 	supply_chain.Point_of_sales AS F

   	 INNER JOIN
       		 	supply_chain.Sales as S ON F.ORDER_NUMBER = S.ORDER_NUMBER

    	INNER JOIN
        		supply_chain.Store AS SE ON S.STORE_KEY = SE.STORE_KEY

    	GROUP BY
        		SE.Monthly_Rent_Cost
     ) AS Sub;
```


**SQL Query Output:**

![Total_profit](https://github.com/arjun21112000/Supply-chain-management-/assets/159052306/d10f9364-1737-4fc2-af05-e8b0fb835f73)


## Query 3: BRAND WISE SALES 
**SQL Query:**

```sql
     select 
		PD.product_group as Brand,
    		ROUND(SUM(PS.SALES_AMOUNT)/1000000,2) AS TOTAL_SALE_IN_MILLIONS

     from 
		supply_chain.Product_data as PD

     inner join 
		supply_chain.Point_of_sales as PS on
    		PD.product_key = PS.product_key

     group by Brand
		order by TOTAL_SALE_IN_MILLIONS desc
		limit 10;
```

**SQL Query Output:**

![Brand wise sales](https://github.com/arjun21112000/Supply-chain-management-/assets/159052306/8a433ffc-fc58-4f2f-bae4-c9ee6e2b3107)

## Query 4: TOP 10 STORES SALES WISE.
**SQL Query:**
```
	SELECT 
   			 ROUND(SUM(PS.SALES_AMOUNT)/1000000,2) AS TOTAL_SALE_IN_MILLIONS,
			SE.STORE_NAME AS TOP_10_STORES

	from
    			supply_chain.Point_of_sales as PS

	INNER JOIN 
			supply_chain.Sales as S ON
    			PS.ORDER_NUMBER = S.ORDER_NUMBER

	INNER JOIN 
			supply_chain.Store as SE ON 
   			 S.STORE_KEY = SE.STORE_KEY

	GROUP BY 
			TOP_10_STORES

	ORDER BY 
			TOTAL_SALE_IN_MILLIONS DESC
	LIMIT 10;
```

**SQL Query Output:**

![Top 10 store wise sale](https://github.com/arjun21112000/Supply-chain-management-/assets/159052306/07f4aca0-97f9-49c5-9bee-f3019335741c)



## Query 5: MONTH WISE SALES FOR PARTICULAR YEAR 
**SQL Query:**

```sql
	select 
			ROUND(SUM(PS.SALES_AMOUNT)/1000000,2) AS TOTAL_SALES,
			MONTH(S.DATE )AS MONTHS

	FROM 
			supply_chain.Point_of_sales as PS

	INNER JOIN 
			supply_chain.Sales as S ON
    			PS.Order_Number = S.Order_Number

	WHERE 
			S.DATE >= "2022-01-01" AND S.DATE <= "2022-12-31" 

	GROUP BY
			MONTHS

	ORDER BY
			 MONTHS asc;
```

**SQL Query Output:**

![Month wise sales ](https://github.com/arjun21112000/Supply-chain-management-/assets/159052306/aa75462d-a477-4a95-a230-b908b41e5cf6)


## SQL Code and Explanation
Each query's SQL code is designed to retrieve, aggregate, and calculate specific metrics. Explanation accompanying the code provides clarity on the logic applied and the importance of the query within the project's context.

## Insights from SQL Analysis
The SQL analysis reveals trends such as brand wise sales explain which brand have high demand , top performing stores explains stores which are performing well which helps us optimise inventory as well, month wise and region wise sales will help in keeping track of patterns and insight into behaviour of customers over a period of time .

## Usage Instructions
### Cloning the Repository:
Clone the project repository using the command `git clone https://github.com/DeveshGaonkar/Bank_Analytics` in your preferred terminal. This creates a local copy of the project files on your machine.

### Setting Up Data Sources:
To work with the dashboards and SQL queries, ensure Product_data.csv, Store.csv, Inventory.csv, customers.csv,  sales.csv and Point_of_sales.csv are available in the designated folders. Open the respective dashboard tools and link these datasets to your project.

### Accessing and Interacting with Dashboards:
1. Open the Excel dashboard by double-clicking `Excel (supply_chain) 2023.xlsx`.
3. In Tableau, open `Tableau(supply_chain).twbx`.
4. Navigate through tabs and interact with charts by selecting dropdowns, buttons, and filters.

### Running SQL Queries:
Install a SQL environment MySQL. Copy each SQL query from the documentation and execute it in the SQL environment. Observe the query output for insights.

### Troubleshooting and FAQs:
If dashboards don't load properly, ensure the required software is installed. For SQL query issues, check SQL syntax and ensure data sources are accurately linked. For more FAQs, refer to the documentation.

## Conclusion
### Project Summary
The project involved analysing Supply Chain using Excel and Tableau dashboards, as well as SQL queries. Key insights were derived to understand future demand, payment behaviours, and geographic trends.

### Achievements and Insights
The project successfully created interactive dashboards showcasing critical KPIs, revealing trends like Region wise sales and profit, Brand wise sales, and sales growth. Insights contributed to informed decision-making.

### Lessons Learned
Challenges included dataset cleaning and tool-specific nuances. The project highlighted the importance of clear visualisation design and thorough data understanding for meaningful analysis.

### Future Enhancements
Future work could involve advanced SQL analysis or integration with live data sources to maintain real-time insights.

## Contact Information
- **Name:** Arjun Lalchandra Yadav
- **Email Address:** arjun21112000@gmail.com
- **LinkedIn Profile:**  https://www.linkedin.com/in/arjun-yadav21/
- **GitHub Repository:** Supply-chain-management-

## Additional Resources 
[Link to the Tableau.](https://public.tableau.com/views/Tableausupply_chain/Dashboard1?:language=en-US&:display_count=n&:origin=viz_share_link)  
[Link to the Excel.](https://1drv.ms/x/c/51ce8b46227cfb78/EQ406IvHCHRFrvfAfpA41zIBs2-1rHQE-_yeRvwO-pZceg?e=5Kt8HE)  
[Documentation or tutorials on using Tableau.](https://help.tableau.com/current/guides/get-started-tutorial/en-us/get-started-tutorial-home.htm)  
[Documentation or tutorials on using MySQL.](https://www.javatpoint.com/mysql-tutorial)  
[Documentation or tutorials on using Excel.](https://www.javatpoint.com/excel-tutorial) 
