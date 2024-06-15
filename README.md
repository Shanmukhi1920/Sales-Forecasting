# Sales_Forecasting
## Overview
This project aims to forecast weekly sales in the Technology category using time series analysis techniques. The primary objective is to identify trends and seasonal patterns in the sales data to develop accurate forecasting models. Various ARIMA (Autoregressive Integrated Moving Average) models and Vector Autoregressive (VAR) models are evaluated to determine the best fit. Additionally, regression with ARIMA errors is applied to forecast related sales categories, such as Office and Furniture, based on the Technology sales data.

## Data Link
The dataset used in this project contains retail data of a global superstore for 4 years.. 
[Source](https://www.kaggle.com/datasets/rohitsahoo/sales-forecasting)

## Repository Contents
- `Project.Rmd`: The main R Markdown file containing the code, analysis, and documentation.
- `train.csv`: The dataset containing the sales data used for modeling.
  
## Methodology

### Data Preprocessing
1. **Data Cleaning**: Removed missing values and inconsistencies from the dataset.
2. **Log Transformation**: Applied a log transformation to stabilize the variance in the sales data.

### Exploratory Data Analysis
1. **Time Series Plots**: Visualized the sales data over time to identify potential trends and seasonal patterns.
2. **Autocorrelation Function (ACF) Plots**: Analyzed the autocorrelation between observations at different time lags to detect seasonality.
3. **Unit Root Tests**: Performed unit root tests (e.g., Augmented Dickey-Fuller, KPSS) to check for stationarity and applied differencing as needed.
4. **Seasonal Differencing**: Applied seasonal differencing to capture and remove seasonal patterns in the data.
   
### Feature Engineering
1. **Lag Features**: Calculated lagged values of Technology sales using ccf (Cross Correlation function) to use as predictors for forecasting Office and Furniture sales.

### Modeling and Evaluation
1. **ARIMA Models**: Built and evaluated multiple ARIMA models, including:
   - ARIMA(0,1,1)(0,1,2)[52]
   - ARIMA(1,1,1)(0,1,1)[52]
   - ARIMA(1,1,2)(0,1,1)[52]
   - ARIMA(2,1,2)(0,1,1)[52]
   - ARIMA(0,1,1)(1,1,1)[52]
2. **Auto ARIMA**: Utilized the `auto.arima` function to automatically select the best ARIMA model based on AIC (Akaike Information Criterion) and BIC (Bayesian Information Criterion).
3. **Model Evaluation**: Evaluated the performance of the models using various metrics, such as AIC, BIC, log-likelihood, sigma^2 (residual variance).

### Residual Analysis and Backtesting

1. **Ljung-Box Test**: Applied the Ljung-Box test to check for autocorrelation in the residuals.
2. **Backtesting**: Performed backtesting to evaluate the models' forecasting performance on historical data using the metrics: MAE (Mean Absolute Error), RMSE (Root Mean Squared Error), MAPE (Mean Absolute Percentage Error), and Symmetric MAPE.

### Regression with ARIMA Errors
Performed Prewhitening to remove autocorrelations within the series to forecast the sales.
1. **Office Sales Forecasting**: Forecasted Office sales using Technology sales regressed at lag 8.
2. **Furniture Sales Forecasting**: Forecasted Furniture sales using Technology sales regressed at lag 5.

### Vector Autoregressive (VAR) Models
Estimated VAR models to capture the interdependencies between multiple time series, such as Technology, Office, and Furniture sales and evaluated the performance of the VAR models using Portmanteau Test.

## Key Findings
- ARIMA(0,1,1)(1,1,1)[52] emerged as the best-performing model, balancing fit and complexity while providing accurate forecasts.
- The analysis highlighted the significance of seasonal patterns and trends in sales data. Regression with ARIMA errors showed that technology sales significantly impact office and furniture sales, particularly at specific lags.
- VAR model with 10 lags indicates that the residuals no longer exhibit significant autocorrelation, adequately capturing the dependencies in the data.

