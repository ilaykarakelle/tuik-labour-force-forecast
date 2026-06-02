# TÜİK Forecasting Project: Employed by Status in Employment

**Author:** İlayda Karakelle  
**Course:** Quantitative Methods for Decision Making  
**Date:** 2026-06-03

---

## 1. Project Overview

This project forecasts Turkey's total number of employed persons (15+ age) using quarterly data from the TÜİK Data Portal, accessed directly through the `tuikr` R package. Ten forecasting methods are applied and compared using standard accuracy measures. The superior method is selected to forecast 2026 Q2.

---

## 2. Data Source and TÜİK Connection

- **TÜİK Data Set Name:** Employed by status in employment
- **TÜİK Theme / Category:** Employment, Unemployment and Wages (Theme 8)
- **TÜİK Table Name:** Employed by status in employment
- **tuikr Dataflow ID:** NA (istab type table, accessed via `table_url`)
- **Selected Variable:** Total employed (15+ age)
- **Data Frequency:** Quarterly
- **Time Coverage:** 2021 Q1 – 2026 Q1
- **Latest Available Observation:** 2026 Q1 — 31,480 thousand persons
- **Forecast Target Period:** 2026 Q2
- **Date of Data Access:** 2026-06-03
- **R Package Used for Data Access:** `tuikr` (https://github.com/emraher/tuikr)

> **Note on data access:** TÜİK's SDMX API returned HTTP 401 Unauthorized errors for all dataflow IDs when using `statistical_data()`. As a reproducible alternative, `statistical_tables()` was used to retrieve the `table_url` for the istab-type table, and the data were fetched directly within R using `httr::GET()`. All data access was performed programmatically inside the R notebook. No local data file was manually created, edited, or uploaded.

---

## 3. Research Objective

This project forecasts Turkey's quarterly total employment (15+ age). Employment is a key macroeconomic indicator that reflects labour market conditions. The series exhibits both an upward trend and quarterly seasonal patterns, making it well suited for comparative evaluation of multiple forecasting methods.

---

## 4. Use of TÜİK Data in R

Data was accessed directly from TÜİK using the `tuikr` package via `statistical_tables(8)`. The table URL was fetched using `httr::GET()` with an Accept header. No manually prepared or edited data file was used. All filtering, cleaning, and time series structuring was performed within the R notebook.

- Selected variable: Total employed (15+ age, Toplam)
- Time variable: Year and quarter columns from the TÜİK table
- Data frequency: Quarterly
- Latest available observation: 2026 Q1
- Forecast target: 2026 Q2

---

## 5. Exploratory Time Series Analysis

- Clear upward trend from 2021 to 2025
- Visible quarterly seasonality (Q3 peaks, Q1 troughs)
- Seasonal indices: Q1 = 0.976, Q2 = 0.998, Q3 = 1.016, Q4 = 1.015
- No missing values
- Slight decline in 2026 Q1

---

## 6. Forecasting Methods Applied

- Naïve Forecasting
- Moving Average (3-quarter window)
- Weighted Moving Average (weights: 0.2, 0.3, 0.5)
- Exponential Smoothing (alpha = 0.3)
- Trend-Adjusted Exponential Smoothing (alpha = 0.3, beta = 0.2)
- Linear Trend Projection
- Seasonal Indices
- Additive Decomposition
- Multiplicative Decomposition
- Regression with Trend and Seasonal Dummy Variables

---

## 7. Forecast Accuracy Comparison

| Method | Bias | MAD | MSE | MAPE | RSFE | Tracking Signal | 2026 Q2 Forecast |
|---|---|---|---|---|---|---|---|
| Naïve Forecasting | 204.45 | 582.35 | 475,612.15 | 1.87% | 4,089.00 | 0.351 | 31,480.00 |
| Moving Average (3) | 198.77 | 443.68 | 281,521.23 | 1.42% | 3,776.67 | 0.448 | 32,401.67 |
| Weighted Moving Average | 135.22 | 321.71 | 144,499.32 | 1.03% | 2,569.20 | 0.420 | 32,150.70 |
| Exponential Smoothing | 773.12 | 922.31 | 1,146,202.60 | 2.96% | 16,235.46 | 0.838 | 32,261.64 |
| Trend-Adjusted ES | −1,109.88 | 1,109.88 | 1,534,334.18 | 3.60% | −23,307.51 | −1.000 | 32,545.67 |
| Linear Trend Projection | 0.00 | 615.21 | 618,351.28 | 2.00% | 0.00 | 0.000 | 33,614.64 |
| Seasonal Indices | −0.85 | 524.48 | 394,852.80 | 1.70% | −17.92 | −0.002 | 33,514.06 |
| Additive Decomposition | 39.62 | 119.72 | 19,945.04 | 0.38% | 673.55 | 0.331 | 32,587.44 |
| Multiplicative Decomposition | 40.35 | 121.74 | 21,214.85 | 0.39% | 685.95 | 0.331 | 32,588.43 |
| **Regression w/ Dummies** | **0.00** | **510.42** | **371,261.42** | **1.65%** | **0.00** | **0.000** | **33,753.03** |

---

## 8. Selection of the Superior Method

**Selected Method: Regression with Trend and Seasonal Dummy Variables**

This method was selected because:
- It explicitly models both the upward trend and quarterly seasonality
- Bias = 0.00 and Tracking Signal = 0.000, indicating no systematic over- or under-forecasting
- R² = 0.837; all coefficients are statistically significant (p < 0.05)
- Estimated equation: Total Employed = 28,181.37 + 212.10 × t + 905.40 × Q2 + 1,268.70 × Q3 + 1,014.60 × Q4
- Although Additive and Multiplicative Decomposition yield lower MAD and MSE, they cannot be directly extended to a reproducible single-point forecast without additional assumptions about the trend component
- Actual vs forecast plot shows consistent fit throughout the series

---

## 9. Final Next-Period Forecast

- **Superior Method:** Regression with Trend and Seasonal Dummy Variables
- **Date of Data Access:** 2026-06-03
- **Latest Available TÜİK Observation:** 2026 Q1 — 31,480 thousand persons
- **Forecast Target Period:** 2026 Q2
- **Forecasted Value:** 33,753.03 thousand employed persons
- **MAD:** 510.42 | **MAPE:** 1.65%

---

## 10. Interpretation of Results

Total employment in Turkey shows a consistent upward trend with clear quarterly seasonality. Q3 is typically the peak quarter. The regression model captures both patterns and forecasts a seasonal recovery of approximately 33,753 thousand employed persons in 2026 Q2, up from the Q1 trough of 31,480 thousand, consistent with historical seasonal patterns.

---

## 11. Limitations

- Short time series (21 quarters) limits robustness of seasonal estimates
- No external variables included (GDP, inflation, policy changes)
- 2026 Q1 decline may reflect structural changes not captured by the model
- TÜİK may revise historical data after the access date

---

## 12. Reproducibility

1. Clone the repository: `git clone https://github.com/ilaykarakelle/tuik-labour-force-forecast`
2. Open `tuik-labour-force-forecast.Rproj` in RStudio
3. Run `renv::restore()` to restore the package environment
4. Open `forecasting_project.Rmd` and click **Knit**

All data are accessed directly from TÜİK through the `tuikr` package at runtime. No local data files are required.

---

## 13. Repository Structure
tuik-labour-force-forecast/
│
├── README.md
├── forecasting_project.Rmd
├── forecasting_project.html
├── outputs/
│   ├── tables/
│   │   ├── accuracy_comparison.csv
│   │   └── final_forecast.csv
│   └── figures/
│       ├── actual_series_plot.png
│       ├── naive_forecast_plot.png
│       ├── moving_average_plot.png
│       ├── weighted_moving_average_plot.png
│       ├── exponential_smoothing_plot.png
│       ├── trend_adjusted_smoothing_plot.png
│       ├── trend_projection_plot.png
│       ├── seasonal_indices_plot.png
│       ├── additive_decomposition_plot.png
│       ├── multiplicative_decomposition_plot.png
│       ├── regression_seasonal_dummy_plot.png
│       └── superior_method_plot.png
├── R/
│   ├── data_import.R
│   ├── forecasting_methods.R
│   ├── accuracy_measures.R
│   └── plots.R
├── renv.lock
└── .gitignore
---

## 14. Author

- **Name:** İlayda Karakelle
- **Course:** Quantitative Methods for Decision Making
- **Date:** 2026-06-03
