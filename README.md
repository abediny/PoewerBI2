# 1. Dashboard Objective
Provide executives with: <br/>
•	Revenue performance <br/>
•	Growth trends <br/>
•	Customer & product insights <br/>
•	Early signals (decline, concentration risk, seasonality) <br/>
________________________________________
# 2. Data Model 
Fact: fact_sales <br/>
•	Dimensions: dim_customers, dim_products, dim_dates <br/>
Ensure:<br/>
•	Single direction relationships (Dim → Fact) <br/>
•	Date table marked properly <br/>
________________________________________
## Report Pages (Executive Flow)
Page 1: Executive Overview (Main Page) <br/>
 KPI Cards (Top Row) <br/>
•	Total Sales  (we discussed ) <br/>
•	Total Orders (COUNT of SalesKey) – we discussed last session <br/>
•	Avg Order Value  <br/>
•	YoY Growth % <br/> 
DAX: <br/>
Total Sales = SUM(fact_sales[SalesAmount])  <br/>
Total Orders = COUNT(fact_sales[SalesKey]) <br/>
Avg Order Value = DIVIDE([Total Sales], [Total Orders]) <br/>
Sales LY = CALCULATE([Total Sales], SAMEPERIODLASTYEAR(dim_dates[Date])) <br/>
YoY Growth % = DIVIDE([Total Sales] - [Sales LY], [Sales LY])
________________________________________
Sales Trend <br/>
Line chart: <br/>
o	Axis: dim_dates[MonthName] (sorted by Month) <br/>
o	Legend: Year <br/>
o	Value: Total Sales <br/>
________________________________________
Sales by Category<br/>
•	Donut / Bar chart <br/>
•	dim_products[Category] <br/>
________________________________________
Sales by City<br/>
•	Map visual <br/>
•	Size: Total Sales <br/>
•	Location: City <br/>
________________________________________
Executive Insight Box (Text)<br/>
Use dynamic measure like: <br/>
Top Category = TOPN(1, VALUES(dim_products[Category]), [Total Sales]) <br/>
Display:<br/>
"Electronics contributes the highest revenue this period." <br/>
________________________________________
## Page 2: Customer Insights
KPIs <br/>
•	Total Customers  <br/>
•	Revenue per Customer  <br/>
•	Repeat Purchase Rate (if extended)  <br/>
________________________________________
Top Customers <br/>
•	Table: <br/>
o	CustomerName <br/>
o	Total Sales <br/>
________________________________________
Customer Distribution <br/>
•	Histogram-style (group by revenue buckets)  <br/>
________________________________________
Customer Geography <br/>
•	Map by City  <br/>
________________________________________
## Page 3: Product Performance
Top Products <br/>
•	Bar chart (Top 10)  <br/>
•	ProductName vs Sales  <br/>
________________________________________
Category Performance Over Time <br/>
•	Stacked area chart  <br/>
________________________________________
Price vs Quantity<br/>
•	Scatter plot:  <br/>
o	X: UnitPrice  <br/>
o	Y: Quantity <br/>
o	Size: SalesAmount  <br/>
This is powerful for execs (value vs volume view) <br/>
________________________________________
## Page 4: Trends & Forecasting
Time Intelligence <br/>
•	YTD Sales <br/>
•	MTD Sales <br/>
•	QoQ Growth <br/>
________________________________________
Forecast<br/>
•	Built-in Power BI forecast on sales trend <br/>
________________________________________
Anomaly Detection <br/>
•	Enable anomaly detection in line chart <br/>
________________________________________
# 4. Design Principles (Executive-Level) Layout
•	Use grid structure <br/>
•	Keep top = KPIs, middle = trends, bottom = breakdowns <br/>
Colors<br/>
•	1 primary (e.g., blue) <br/>
•	1 accent (orange for highlights) <br/>
•	Neutral background <br/>
Typography<br/>
•	Large numbers for KPIs <br/>
•	Minimal labels <br/>
White Space<br/>
•	Don’t overcrowd (this is where most dashboards fail) <br/>
________________________________________
# 5. Interactivity
Slicers (Top Panel) – refer to the last week<br/>
•	Year <br/>
•	Month <br/>
•	Category <br/>
________________________________________
Drill-through <br/>
•	From Overview → Customer Details <br/>
•	From Category → Product Breakdown <br/>
________________________________________
Tooltips Page<br/>
Create a tooltip page showing:<br/>
•	Mini trend <br/>
•	Customer contribution <br/>
________________________________________
# 6. Executive Insights Layer (What makes this “senior”)
Add calculated insights:<br/>
•	% contribution by top 10 customers <br/>
•	Category concentration risk <br/>
•	Growth vs decline segments <br/>
Example:<br/>
Top 10 Customers Sales % =
DIVIDE(
    CALCULATE([Total Sales], TOPN(10, VALUES(dim_customers[CustomerKey]), [Total Sales])),
    [Total Sales]
)
________________________________________
# 7. What Will Make This Stand Out (Very Important)
Most dashboards stop at visuals. To elevate this:<br/>
Add narrative<br/>
Use a text box:<br/>
•	“Sales increased by 12% YoY driven by Electronics” <br/>
Add alerts mindset<br/>
•	Highlight negative growth in red <br/>
•	Add arrows/icons <br/>
Focus on decisions<br/>
Every visual should answer:<br/>
“What action should leadership take?”<br/>

