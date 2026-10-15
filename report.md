# AirPassengers Forecasting Report

## 1. Recommendation

**AutoARIMA is the recommended model** for forecasting monthly AirPassengers data. Across eight rolling origins with a 12-month forecast horizon, it outperformed the SeasonalNaive baseline in MASE (0.647 vs. 1.313), RMSSE (0.683 vs. 1.246), and CRPS (0.0339 vs. 0.0616).

## 2. Prediction Intervals

AutoARIMA produced narrower 80% prediction intervals, with a mean width of 44.08 compared with 77.76 for SeasonalNaive. However, its empirical coverage was only 69.79%, below the intended 80% target. SeasonalNaive coverage was even lower at 51.04%.

Therefore, AutoARIMA offers narrower intervals and better coverage than the baseline, but its uncertainty estimates still need improvement.

## 3. Residual Analysis

The series shows a strong upward trend and annual seasonality. SeasonalNaive residuals were mostly positive, suggesting under-forecasting as passenger counts increased. AutoARIMA residuals appeared more balanced around zero, indicating that it captured the main patterns more effectively.

However, its residual ACF suggests some remaining temporal correlations, so the model may not have captured every pattern.

## 4. Proposed Improvement

Calibrate AutoARIMA's prediction intervals using out-of-sample forecast errors, ensuring that each training fold uses only information available at that point in time. Then evaluate coverage on separate rolling origins to check whether it approaches the 80% target without unnecessarily widening the intervals.

## Conclusion

AutoARIMA is the stronger forecasting candidate, but its prediction intervals need better calibration before they can be relied upon for decision-making.
