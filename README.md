TÜİK Forecasting Project: Employed Persons by Employment Status
Author: İlayda Karakelle

Course: Quantitative Methods for Decision Making

Date: 2026-06-03

1. Project Overview
This project forecasts the total number of employed persons (aged 15 and over) in Turkey using quarterly data from the TÜİK (Turkish Statistical Institute) Data Portal. Ten different forecasting methods were applied and compared. The method that yielded the best results was used to forecast the second quarter of 2026.

2. Data Source and TÜİK Connection
TÜİK Dataset Name: Employed Persons by Employment Status

TÜİK Theme / Category: Employment, Unemployment, and Wages (Theme 8)

TÜİK Table Name: Employed Persons by Employment Status

tuikr Data Stream ID: N/A (Accessed via table_url)

Selected Variable: Total employed persons (15+ years)

Data Frequency: Quarterly

Time Span: 2021 Q1 – 2026 Q1

Last Observation: 2026 Q1 — 31,480 thousand people

Forecast Target Period: 2026 Q2

Date of Access: 2026-06-03

R Package Used: tuikr (https://github.com/emraher/tuikr)

Note on Data Access: TÜİK's SDMX API returned an HTTP 401 Unauthorized error when using statistical_data(). As a reproducible alternative, statistical_tables() was used to retrieve the data for the istab type table, and the data was processed directly within R. All data access was performed programmatically within an R notebook. No local data file was manually created, edited, or uploaded.

3. Research Objective
This project forecasts Turkey's quarterly total employment (aged 15+). Employment is a key macroeconomic indicator reflecting labor market conditions. The quarterly period provides sufficient observations for seasonal analysis.

4. Using TÜİK Data in R
Data was accessed directly from TÜİK via the tuikr package using statistical_tables(8). The table URL was retrieved using httr::GET() with an Accept header. No manually prepared or edited data files were used. All filtering, cleaning, and time-series configuration were performed within the R notebook.

5. Exploratory Time Series Analysis
A clear upward trend from 2021 to 2025.

Visible quarterly seasonality (peaks in Q3, troughs in Q1).

No missing values.

A slight decline in the first quarter of 2026.

6. Forecasting Methods Applied
Naive Forecast

Moving Average (3-quarter window)

Weighted Moving Average (weights: 0.2, 0.3, 0.5)

Exponential Smoothing (alpha = 0.3)

Trend-Adjusted Exponential Smoothing (alpha = 0.3, beta = 0.2)

Linear Trend Projection

Seasonal Indices

Additive Decomposition

Multiplicative Decomposition

Regression with Trend and Seasonal Dummy Variables

7. Forecast Accuracy Comparison
Method	Bias	MAD	MSE	MAPE	Tracking Signal	2026 Q2 Forecast
Naive Forecast	204.45	582.35	475,612.15	1.87%	4,089.00	31,480.00
Moving Average (3)	198.77	443.68	281,521.23	1.42%	3,776.67	32,401.67
Weighted MA	135.22	321.71	144,499.32	1.03%	2,569.20	32,150.70
Exponential Smoothing	773.12	922.31	1,146,202.60	2.96%	16,235.46	32,261.64
Trend-Adjusted ES	-1,109.88	1,109.88	1,534,334.18	3.60%	-23,307.51	32,545.67
Linear Trend Proj.	0.00	615.21	618,351.28	2.00%	0.00	33,614.64
Seasonal Indices	-0.85	524.48	394,852.80	1.70%	-17.92	33,514.06
Additive Decomp.	39.62	119.72	19,945.04	0.38%	673.55	32,587.44
Multiplicative Decomp.	40.35	121.74	21,214.85	0.39%	685.95	32,588.43
Regression w/ Dummies	0.00	510.42	371,261.42	1.65%	0.00	33,753.03
8. Selection of the Superior Method
Selected Method: Regression with Trend and Seasonal Dummy Variables.

Rationale: This model explicitly captures both the upward trend and quarterly seasonality.

Performance: Bias = 0.00 and Tracking Signal = 0.000, indicating no systematic over- or under-estimation.

Statistical Significance: R 
2
 =0.837; all coefficients are statistically significant (p < 0.05).

Forecasting Equation: Total Employment=28,181.37+212.10×t+905.40×Q2+1,268.70×Q3+1,014.60×Q4

9. Final Forecast for the Future Period
Superior Method: Regression with Seasonal Dummy Variables

TÜİK Last Observation (2026 Q1): 31,480 thousand people

Forecast (2026 Q2): 33,753.03 thousand employed persons

Accuracy: MAD: 510.42 | MAPE: 1.65%

10. Interpretation of Results
Total employment in Turkey shows a stable upward trend with clear quarterly seasonality. The third quarter is typically the peak employment period. The regression model captures both patterns and predicts a seasonal recovery to approximately 33,753 thousand employed persons in Q2 2026, consistent with historical seasonal patterns.

11. Limitations
Short time series (21 quarters) limits the robustness of seasonal forecasts.

No external variables (GDP, inflation, policy changes) were included.

The decline in Q1 2026 may reflect structural changes not captured by the model.

TÜİK may revise historical data after the access date.

12. Reproducibility
Clone the repository: git clone [https://github.com/ilaykarakelle/tuik-labour-force-forecast](https://github.com/ilaykarakelle/tuik-labour-force-forecast)

Open tuik-labour-force-forecast.Rproj in RStudio.

Run renv::restore() to restore the package environment.

Open forecasting_project.Rmd and click Knit. All data is accessed directly from TÜİK via the tuikr package at runtime.

13. Repository Structure
(Structure follows the provided directory tree in the original text)

14. Author
Name: İlayda Karakelle

Course: Quantitative Methods for Decision Making

Date: 2026-06-03git