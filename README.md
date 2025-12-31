# time-series-forecasting-sales

Data Cleaning & Preprocessing
•	Changed the format of InvoiceDate to standard Date time
•	Removed the Invoices starting with C as they are cancelled orders and i am forecasting for the demand only
•	Cleaned invalid data like prices in negative and quantity less than 0
•	Removed SKU’s having StockCode other than 5 numerics
•	Combined the Dataset of both years 2019-10 and 2010-11
•	Sorted the Dataset based on Invoice Date

Data Aggregation to understand Daily Demand
•	Created a new dataframe having total quantity of a particular SKU on a single date
•	Filled 0 having no demand of the SKUs to maintain time continuity
•	Filtered weak SKU’s -> Remove SKUs having total demand < 50 in two years

Feature Engineering
•	Added Lag features for past 1,7 and 14 days to understand the previous pattern of demand
•	Added Rolling mean and Std to get the volatility and the short term trend
•	Removed Nans from the dataset 

Train/Test Split
•	Splitted Data Based on a particular date . i have spillted in 80-20 but based on the date (01-07-2011)
•	Defined the Features and target
•	Choose Tree based models (i.e XGBoost) as works well with lag features and its fast

Evaluation
•	On average , the forecast is off by approx. 35 units per sku per day as model RMSE is approx  35
![Uploading image.png…]()
