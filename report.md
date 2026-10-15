# AirPassengers Forecasting Report

## 1. Recommendation

**AutoARIMA is the recommended model** for forecasting monthly international air passenger numbers. Across eight rolling origins with a 12-month forecast horizon, it outperformed the SeasonalNaive benchmark on all three evaluation metrics: MASE (0.647 vs. 1.313), RMSSE (0.683 vs. 1.246), and CRPS (0.0339 vs. 0.0616).

The dataset contains 144 monthly observations from January 1949 to December 1960. Exploratory analysis and STL decomposition revealed a strong upward trend and clear annual seasonality. While SeasonalNaive captures the recurring yearly pattern, it does not adapt well to the long-term growth in passenger numbers.

AutoARIMA provides a more effective balance of trend and seasonal forecasting. Its lower error scores indicate better point forecasts and overall probabilistic performance across the evaluated rolling origins.

## 2. Prediction Intervals

Prediction intervals help communicate forecast uncertainty. An 80% prediction interval should contain approximately 80% of actual observations over repeated, comparable forecasts.

AutoARIMA produced a mean 80% prediction interval width of **44.08**, compared with **77.76** for SeasonalNaive. Its intervals were therefore considerably narrower. However, narrower intervals are only useful when they provide adequate coverage.

| Evaluation Metric       | SeasonalNaive | AutoARIMA |
| ----------------------- | ------------: | --------: |
| Mean 80% interval width |         77.76 |     44.08 |
| Empirical coverage      |        51.04% |    69.79% |
| Target coverage         |           80% |       80% |

AutoARIMA achieved better empirical coverage than SeasonalNaive, but its 69.79% coverage remained below the intended 80% level. SeasonalNaive performed worse, covering only 51.04% of actual observations.

**The intervals are not yet sufficiently calibrated.** AutoARIMA is the stronger candidate, but its uncertainty estimates may be too narrow for the intended coverage. Further calibration should be evaluated on separate rolling origins before the intervals are relied upon for decisions.

## 3. Residual Analysis

The series exhibits a strong upward trend and annual seasonality. These patterns help explain the difference between the two forecasting approaches.

The SeasonalNaive residual plot shows predominantly positive errors, indicating that actual passenger numbers were often higher than the forecasts. This suggests that repeating the previous year's values did not adequately capture the continued growth in air travel.

AutoARIMA residuals appear more balanced around zero, suggesting that it captures the main trend and seasonal patterns more effectively. This observation is consistent with its better cross-validation scores.

However, the residual autocorrelation function (ACF) indicates that some early lags remain outside the confidence bounds, with a possible additional effect at lag 24. This suggests that some temporal dependence may remain in the forecast errors. The model therefore captures the main patterns but may not explain all the structure in the series.

Residual plots and ACF results should be interpreted as diagnostic evidence rather than proof that all remaining correlations are statistically significant.

## 4. Proposed Improvement

The next step is to **calibrate AutoARIMA's prediction intervals using out-of-sample forecast errors**.

The calibration should follow the same rolling-origin discipline as the main evaluation. At each origin, the calibration must use only errors available from earlier forecasts, without accessing future observations. The adjusted intervals should then be evaluated on separate rolling origins.

The expected improvement is empirical coverage closer to the 80% target while avoiding unnecessarily wide intervals. Both coverage and interval width should be monitored to ensure that better coverage does not come at the cost of intervals that are too broad.

## Conclusion

AutoARIMA is the preferred model because it consistently outperformed SeasonalNaive across the evaluated error and probabilistic metrics. Nevertheless, its prediction intervals achieved only 69.79% coverage against the intended 80% target.

The recommended next step is to improve interval calibration and validate the results using rolling-origin evaluation. This would preserve the model's forecasting advantages while providing a more reliable representation of uncertainty.
