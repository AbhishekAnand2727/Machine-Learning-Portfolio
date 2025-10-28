# Store Sales - Time Series Forecasting

This project focuses on forecasting store sales based on historical data using various time series techniques and machine learning models. The goal was to build a **robust model** capable of accurately predicting future sales.

***

### Aim and Approach

The primary objective of this project was to develop an **end-to-end time series forecasting pipeline**. I achieved this by:
* Loading and merging **multiple data sources** (stores, oil prices, holidays, transactions).
* Performing extensive **Exploratory Data Analysis (EDA)** to understand seasonality and trends.
* Engineering **time-series specific features** (lags, rolling averages).
* Building, training, and evaluating several regression models to predict store sales.

##  Datasets Used and Details 

### Since the dataset train.csv was over 100MB, I couldn't upload it on github here is a link to the kaggle dataset 
Link: https://www.kaggle.com/competitions/store-sales-time-series-forecasting

The project was built upon the successful integration of **five distinct datasets**, each contributing unique features essential for accurate time series forecasting.

| Dataset File Name | Description | Key Features Contributed | Role in Feature Engineering |
| :--- | :--- | :--- | :--- |
| **train.csv / test.csv** | The core historical and test sales data. | `date`, `store_nbr`, `family`, `sales` (Target), `onpromotion` | **Primary Data Source**. Provided the dependent variable and the crucial `onpromotion` feature. |
| **stores.csv** | Static metadata about the 54 individual store locations. | `city`, `state`, **`type` (Store Type)**, `cluster` | Merged to create **categorical features** for store-specific modeling. |
| **holidays\_events.csv** | Details on holidays, events, and their scope (National, Regional, Local). | **`type` (Holiday Type)**, `locale`, `transferred` | Used to engineer the **`holiday_type`** feature, accounting for seasonal and event-driven sales volatility. |
| **oil.csv** | Daily closing price of **Ecuadorian crude oil**. | `dcoilwtico` | Merged as a **macro-economic numerical predictor**, with missing values imputed via **Forward-Fill (ffill)**. |
| **transactions.csv** | The total number of transactions processed at each store daily. | **`transactions`** | Merged as a direct **numerical predictor** of sales volume, providing insight into customer traffic. |

***

### Data Joining Strategy

* **Primary Join Keys:** Datasets were primarily joined to the sales data (`train.csv`/`test.csv`) using the **`date`** column and the **`store_nbr`** column.
* **Feature Enrichment:** The merge process transformed the base sales record into a rich observation containing economic indicators, store context, and event information necessary for the machine learning models.

### Project Workflow

#### 1. Data Merging and Initial Cleaning
I first loaded all raw CSV files and merged them onto the main sales data (`train.csv` and `test.csv`). Missing values were handled by:
* **Oil Prices:** Applying **forward-filling (ffill)** to handle missing oil price entries on non-trading days.
* **Holidays:** Filling `NaN` holiday entries with a **'WorkDay'** placeholder, and zeroing out missing transaction counts.

#### 2. Exploratory Data Analysis (EDA)
I performed EDA to visualize key drivers of sales, confirming strong seasonality and external influence:
* **Overall Trend:** I analyzed total monthly sales to identify clear **yearly seasonality** and visually checked correlation with oil price fluctuations.
* **Seasonality:** Sales were analyzed by **Day of Week** (Mon-Sun) and **Month** (Jan-Dec) to quantify expected dips and peaks.
* **Store Characteristics:** Sales distribution was evaluated against **Store Type** to identify which store categories are the primary revenue drivers.

#### 3. Feature Engineering
I engineered robust, time-aware features for the models:
* **Time Features:** I extracted calendar components like `day_of_week`, `month`, `year`, and created a binary `is_weekend` feature.
* **Lag Features (CRITICAL):** I created `sales_lag_1` and `sales_lag_7` by shifting past sales data, grouped by `store_nbr`, proving the strong predictive power of recent history.
* **Rolling Averages:** I calculated `sales_roll_mean_7` and `sales_roll_mean_30` to capture short-term and long-term sales trends.

#### 4. Data Preprocessing and Splitting
* **Time Series Split:** I split the data strictly by date to ensure the validation set represented future data (**no shuffling**).
* **Feature Transformation:** I used `sklearn.compose.ColumnTransformer` to ensure data was machine-ready:
    * **Standard Scaling** was applied to all numerical features.
    * **One-Hot Encoding** was applied to all categorical features (e.g., `store_nbr`, `city`, `month`, `holiday_type`).

#### 5. Model Building and Evaluation
I trained three distinct regression models to establish a baseline and find the highest-performing algorithm.

***

## 📈 Results and Conclusion

### Performance Summary

| Model | RMSE | MAE | R-squared ($R^2$) |
| :---------------------- | :--------: | :--------: | :---------------: |
| **XGBoost Regressor** | **332.39** | **97.88** | **0.9399** |
| Random Forest Regressor | 342.49 | 126.91 | 0.9362 |
| Linear Regression | 807.29 | 317.28 | 0.6453 |

### Conclusion

The results clearly show that the **XGBoost Regressor** is the superior model for this time series forecasting problem, achieving state-of-the-art performance.

The **XGBoost Regressor** and **Random Forest** models effectively leveraged the engineered time-series features to achieve an R-squared value near **0.94**, meaning they explained approximately 94% of the variance in sales. The very low **RMSE of 332.39** confirms the high accuracy of the final prediction. The final predictions for the test set were generated using the highly accurate XGBoost model.

This was a great learning experience in time series forecasting. I mastered data integration by merging five disparate sources, crucial for feature richness. The greatest learning came from engineering time-aware features (lags and rolling averages) and implementing a robust ColumnTransformer pipeline for mixed-type data, confirming the superior performance of XGBoost in handling non-linear time dependencies over simpler models.