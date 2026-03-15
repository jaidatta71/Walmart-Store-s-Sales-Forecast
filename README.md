# Walmart-Stores-Sales-Forecast
Kaggle's Walmart challenge: Modelling weekly sales. In this notebook, we use data from Walmart to forecast their store's weekly sales.


### Overview
The purpose of the project is to forecast sales for Walmart's product categories in their store based on the sales history of each category. Historical sales data for 45 Walmart stores located in different regions is provided. Each store contains a number of departments.  The goal is to build a predictive model that can accurately predict department-wide weekly sales for each store.

Walmart runs several promotional markdown events throughout the year. These markdowns precede prominent holidays, the four largest of which are the Super Bowl, Labor Day, Thanksgiving, and Christmas. The weeks including these holidays are weighted five times higher in the evaluation than non-holiday weeks. Model the effects of markdowns on these holiday weeks in the absence of complete/ideal historical data.

This project applies regression model techniques. Evaluation is based on RMSE values for the test set.

[](https://www.kaggle.com/competitions/walmart-recruiting-store-sales-forecasting/overview)

### Project Structure
project-name/ Walmart Store's Sales Forecast

├── dataset files

├── notebooks for exploration

├── src(Source code)

├── results Output graphs and evaluation results

└── README.md   

### Dataset
Dataset source:  [](https://www.kaggle.com/competitions/walmart-recruiting-store-sales-forecasting/data)

Dataset consists of 5 files stores.csv, features.csv, train.csv, test.csv
Features include:
  1. Temperature - average temperature in the region
  2. Fuel_Price - cost of fuel in the region
  3. MarkDown1-5 - anonymized data related to promotional markdowns that Walmart is running. MarkDown data is only available after Nov 2011, and is not available for all stores all the time. Any missing value is marked with an NA.
  4. CPI - the consumer price index
  5. Unemployment - the unemployment rate
  6. IsHoliday - whether the week is a special holiday week

Target variable: Weekly_Sales (sales for the given department in the given store)
Target Submission File:
For each row in the test set (store + department + date triplet), predict the weekly sales of that department. The Id column is formed by concatenating the Store, Dept, and Date with underscores (e.g. Store_Dept_2012-11-02).   


### Data Clean up approach:
Droped records if all the values are Null, Only ststus = Clean, Non Salved Cars, Keep data from year: 2000 only, Keep only Non Zero Priced cars
Delete Duplicate VINs and keep only one record & Dropped Duplicate VINs
Simplify Model list in a new column "model_short". Keep top N models per MANUFACTURER; Rest group it under "others".
Data infusion for NULL records like a. Add values to missing data for SIZE & TYPE. If type = truck, van, bus Update size = "full-size" etc..
### Feature engineering:
Create new features that are easy for more meaningful for car business: like No.of years(age), Miles driven per year, Odometer Reading (price per mile)
Treat outliers with LOG transformation.

### Identification of Features making the impact

### Pipe line construction after addressing Low cardinality & High Cardinality columns
Low cardinality: OHE
Hifg Cardinality: TargetEncoding
Numeric: Median
Model Prediction by LGBMRegressor Model
With # of estimators=1000 with 5 fold cross validation

### Evaluation Metrics:
Test RMSE: 0.07 Test MAE: 0.03 Test R²: 0.995
