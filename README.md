# 🚕 Sweet Lift Taxi — Predicting Taxi Orders

## 📋 Project Overview

This project aims to help **Sweet Lift Taxi** company predict the number of taxi orders for the next hour at airports. By anticipating demand, the company can optimize driver allocation during peak hours, ensuring better service and efficiency.
The goal is to build a robust model to predict hourly taxi orders.
The success criteria is to achieve a competitive **RMSE not exceeding 48** on the test set.

## 🗂️ Data Preparation

The dataset consists of historical taxi order data, including `datetime` and `num_orders`. Key preparation steps involved:
- Loading and initial inspection of the data.
- Converting `datetime` to the appropriate format and setting it as the index.
- Verifying chronological order and resampling the data to an hourly frequency.

## 📈 Data Analysis

Exploratory Data Analysis revealed significant patterns:
- **Overall Trend**: A gradual increase in taxi demand from March to August.
- **Seasonality**: Clear daily and weekly seasonal patterns, with demand peaking just after midnight and in the late afternoon/early evening.
- **Residuals**: Mostly stable noise, with a few notable spikes.

## 🧠 Model Training and Evaluation

Several time-series and regression models were developed and evaluated based on RMSE. The data was split into training (90%) and test (10%) sets, ensuring no data leakage.

### Models Explored:

1.  **ARIMA (non-seasonal)**:
    -   **RMSE**: 62.77
    -   *Note*: Seasonal ARIMA could not be tested due to environment limitations.
2.  **Autoregressive (AR) Model**:
    -   **RMSE**: 69.92
3.  **Moving Average (MA) Model**:
    -   **RMSE**: 84.68
4.  **Linear Regression**:
    -   **RMSE**: 52.28
    -   *Features engineered*: month, day, dayofweek, is_weekend, is_week_day, hour, peak hour indicators, cyclical hour/dayofweek, lagged features, and rolling mean.
5.  **Random Forest Regressor**:
    -   **RMSE**: **44.69**
    -   *Parameters tuned*: `n_estimators`, `max_depth`, `min_samples_split` using `GridSearchCV`.

### 🏆 Best Performing Model

The **Random Forest Regressor** achieved the lowest RMSE of **44.69**, successfully surpassing the project's goal of RMSE < 48. This model demonstrated superior capability in capturing the complex, non-linear relationships and temporal patterns within the data.

## 🚀 Conclusion

The Random Forest model is the recommended solution for predicting taxi orders, providing robust and accurate forecasts that meet the business objective. Its strong performance highlights the effectiveness of ensemble methods in time-series forecasting when relevant features are engineered.

## 💻 Technologies Used

-   Python
-   Pandas
-   NumPy
-   Matplotlib
-   Seaborn
-   `statsmodels` (for `seasonal_decompose`, `AutoReg`, `ARIMA`)
-   `pmdarima` (`auto_arima`)
-   Scikit-learn (`train_test_split`, `LinearRegression`, `RandomForestRegressor`, `GridSearchCV`, `mean_squared_error`)
