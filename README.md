1. Dashboard Objective
Provide executives with:
•	Revenue performance 
•	Growth trends 
•	Customer & product insights 
•	Early signals (decline, concentration risk, seasonality) 
________________________________________
2. Data Model 
Fact: fact_sales 
•	Dimensions: dim_customers, dim_products, dim_dates 
Ensure:
•	Single direction relationships (Dim → Fact) 
•	Date table marked properly 
________________________________________
Report Pages (Executive Flow)
Page 1: Executive Overview (Main Page)
 KPI Cards (Top Row)
•	Total Sales  (we discussed )
•	Total Orders (COUNT of SalesKey) – we discussed last session
•	Avg Order Value 
•	YoY Growth % 
DAX:
Total Sales = SUM(fact_sales[SalesAmount])
Total Orders = COUNT(fact_sales[SalesKey])
Avg Order Value = DIVIDE([Total Sales], [Total Orders])
Sales LY = CALCULATE([Total Sales], SAMEPERIODLASTYEAR(dim_dates[Date]))
YoY Growth % = DIVIDE([Total Sales] - [Sales LY], [Sales LY])
________________________________________
Sales Trend 
Line chart: 
o	Axis: dim_dates[MonthName] (sorted by Month) 
o	Legend: Year 
o	Value: Total Sales 
________________________________________
Sales by Category
•	Donut / Bar chart 
•	dim_products[Category] 
________________________________________
Sales by City
•	Map visual 
•	Size: Total Sales 
•	Location: City 
________________________________________
Executive Insight Box (Text)
Use dynamic measure like:
Top Category = 
TOPN(1, VALUES(dim_products[Category]), [Total Sales])
Display:
"Electronics contributes the highest revenue this period."
________________________________________
Page 2: Customer Insights
KPIs
•	Total Customers 
•	Revenue per Customer 
•	Repeat Purchase Rate (if extended) 
________________________________________
Top Customers
•	Table: 
o	CustomerName 
o	Total Sales 
________________________________________
Customer Distribution
•	Histogram-style (group by revenue buckets) 
________________________________________
Customer Geography
•	Map by City 
________________________________________
Page 3: Product Performance
Top Products
•	Bar chart (Top 10) 
•	ProductName vs Sales 
________________________________________
Category Performance Over Time
•	Stacked area chart 
________________________________________
Price vs Quantity
•	Scatter plot: 
o	X: UnitPrice 
o	Y: Quantity 
o	Size: SalesAmount 
This is powerful for execs (value vs volume view)
________________________________________
Page 4: Trends & Forecasting
Time Intelligence
•	YTD Sales 
•	MTD Sales 
•	QoQ Growth 
________________________________________
Forecast
•	Built-in Power BI forecast on sales trend 
________________________________________
Anomaly Detection
•	Enable anomaly detection in line chart 
________________________________________
4. Design Principles (Executive-Level)
 Layout
•	Use grid structure 
•	Keep top = KPIs, middle = trends, bottom = breakdowns 
Colors
•	1 primary (e.g., blue) 
•	1 accent (orange for highlights) 
•	Neutral background 
Typography
•	Large numbers for KPIs 
•	Minimal labels 
White Space
•	Don’t overcrowd (this is where most dashboards fail) 
________________________________________
 5. Interactivity
Slicers (Top Panel) – refer to the last week
•	Year 
•	Month 
•	Category 
________________________________________
Drill-through
•	From Overview → Customer Details 
•	From Category → Product Breakdown 
________________________________________
Tooltips Page
Create a tooltip page showing:
•	Mini trend 
•	Customer contribution 
________________________________________
6. Executive Insights Layer (What makes this “senior”)
Add calculated insights:
•	% contribution by top 10 customers 
•	Category concentration risk 
•	Growth vs decline segments 
Example:
Top 10 Customers Sales % =
DIVIDE(
    CALCULATE([Total Sales], TOPN(10, VALUES(dim_customers[CustomerKey]), [Total Sales])),
    [Total Sales]
)
________________________________________
7. What Will Make This Stand Out (Very Important)
Most dashboards stop at visuals. To elevate this:
Add narrative
Use a text box:
•	“Sales increased by 12% YoY driven by Electronics” 
Add alerts mindset
•	Highlight negative growth in red 
•	Add arrows/icons 
Focus on decisions
Every visual should answer:
“What action should leadership take?”

