# PowerBI
### Dashboard Link : https://app.powerbi.com/groups/me/reports/495b33f1-cc02-4a03-8aba-27fae5438b46/8a2b74bc8c4d960976c4?experience=power-bi

## Problem Statement
Background: Our company is a car dealership that sells various car models. To effectively track and analyse our sales performance, we need a comprehensive Car Sales Dashboard in Power BI. 
Objective: The objective of this project is to design and develop a dynamic and interactive Car Sales Dashboard using Power BI. The dashboard will visualize critical KPIs related to our car sales, helping us understand our sales performance over time and make data-driven decisions.
Problem Statement 1: KPI’s Requirement
The dashboard should provide real-time insights into key performance indicators (KPIs) related to our sales data. This will enable us to make informed decisions, monitor our progress, and identify trends and opportunities for growth.
1.	Sales Overview:
•	Year-to-Date (YTD) Total Sales
•	Month-to-Date (MTD) Total Sales
•	Year-over-Year (YOY) Growth in Total Sales
•	Difference between YTD Sales and Previous Year-to-Date (PTYD) Sales
2.	Average Price Analysis:
•	YTD Average Price
•	MTD Average Price
•	YOY Growth in Average Price
•	Difference between YTD Average Price and PTYD Average Price
3.	Cars Sold Metrics:
•	YTD Cars Sold
•	MTD Cars Sold
•	YOY Growth in Cars Sold
•	Difference between YTD Cars Sold and PTYD Cars Sold
Problem Statement 2: Charts Requirement

1.	YTD Sales Weekly Trend: Display a line chart illustrating the weekly trend of YTD sales. The X-axis should represent weeks, and the Y-axis should show the total sales amount.
2.	YTD Total Sales by Body Style: Visualize the distribution of YTD total sales across different car body styles using a Pie chart.
3.	YTD Total Sales by Color: Present the contribution of various car colors to the YTD total sales through a pie chart.
4.	YTD Cars Sold by Dealer Region: Showcase the YTD sales data based on different dealer regions using a map chart to visualize the sales distribution geographically.
5.	Company-Wise Sales Trend in Grid Form: Provide a tabular grid that displays the sales trend for each company. The grid should showcase the company name along with their YTD sales figures.
6.	Details Grid Showing All Car Sales Information: Create a detailed grid that presents all relevant information for each car sale, including car model, body style, colour, sales amount, dealer region, date, etc


### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed all the data loaded from source.

### Below Dax used in UI to dervive required KPIs used in the dashbaord
car_data[Avg Price] = SUM(car_data[Price ($)])/COUNT(car_data[Car_id])
 - car_data[Avg Price Color] = if([Avg Price Diff]> 0, "Green", "Red")
 - car_data[Avg Price Diff] = [YTD Avg Price] - [PYTD Avg Price]
 - car_data[Cars Sold Color] = if([Cars Sold Diff]>0,"Green", "Red")
 - car_data[Cars Sold Diff] = [YTD Cars Sold]-[PYTD Cars SOld]
 - car_data[Max Point Area chart] = IF(MAXX(ALLSELECTED('Calendar'[week]), [Total Sales])=[Total Sales],MAXX(ALLSELECTED('Calendar'[week]), [Total Sales]),blank())
 - car_data[MTD Avg Price] = TOTALMTD([Avg Price],'Calendar'[Date])
 - car_data[MTD Avg Price KPI] = CONCATENATE("MTD Avg Price : ", FORMAT([MTD Avg Price]/1000,"$0.00K"))
 - car_data[MTD Cars Sold] = TOTALMTD(COUNT(car_data[Car_id]), 'Calendar'[Date])
 - car_data[MTD Cars Sold KPI] = CONCATENATE("MTD Cars Sold  : ", FORMAT([MTD Cars Sold]/1000,"$0.00K"))
 - car_data[MTD Sales KPI] = CONCATENATE("MTD Total Sales : ", FORMAT([MTD Total Sales]/1000000,"$0.00M"))
 - car_data[MTD Total Sales] = TOTALMTD(sum(car_data[Price ($)]), 'Calendar'[Date])
 - car_data[PYTD Avg Price] = CALCULATE([Avg Price],SAMEPERIODLASTYEAR('Calendar'[Date]))
 - car_data[PYTD Cars SOld] = CALCULATE(COUNT(car_data[Car_id]),SAMEPERIODLASTYEAR('Calendar'[Date]))
 - car_data[PYTD Total Sales] = CALCULATE(SUM(car_data[Price ($)]),SAMEPERIODLASTYEAR('Calendar'[Date]))
 - car_data[Sales Diff] = [YTD Total Sales]-[PYTD Total Sales]
 - car_data[Sales Diff color] = if([Sales Diff]>0,"Green", "Red")
 - car_data[Total Sales] = SUM(car_data[Price ($)])
 - car_data[YoY Avg Price Growth] = [Avg Price Diff]/[PYTD Avg Price]
 - car_data[YoY Cars Sold Growth] = [Cars Sold Diff]/[YTD Cars Sold]
 - car_data[YoY Sales Growth] = [Sales Diff]/[PYTD Total Sales]
 - car_data[YTD Avg Price] = totalytd([Avg Price],'Calendar'[Date])
 - car_data[YTD Cars Sold] = TOTALYTD(COUNT(car_data[Car_id]),'Calendar'[Date])
 - car_data[YTD Total Sales] = TOTALYTD(SUM(car_data[Price ($)]), 'Calendar'[Date])

           Using visual level filter from the filters pane, basic filtering was used & null values were unselected for consideration into average calculation.
           
           
