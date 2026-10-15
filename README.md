# International AirPassengers Forecasting

**Submitted by:** Lama Alqahtani
**Academy:** @SDAIAAcademy

## Project Overview

This project explores and forecasts the monthly AirPassengers time series from 1949 to 1960 as part of the SDAIA Time Series course capstone.

The analysis covers time series decomposition, seasonal baseline forecasting, model comparison using AutoGluon, rolling-origin cross-validation, prediction interval evaluation, and residual analysis.

## Key Findings

AutoARIMA outperformed the SeasonalNaive baseline across all three rolling-origin evaluation metrics:

| Metric | SeasonalNaive |  AutoARIMA |
| ------ | ------------: | ---------: |
| MASE   |        1.3133 | **0.6472** |
| RMSSE  |        1.2456 | **0.6833** |
| CRPS   |        0.0616 | **0.0339** |

AutoARIMA also produced narrower 80% prediction intervals, with a mean width of 44.08 compared with 77.76 for SeasonalNaive. However, its empirical coverage was 69.8%, below the target of 80%, indicating that prediction interval calibration could be improved.

## Project Files

* `project.ipynb` — Notebook containing the analysis, forecasting models, evaluation, and visualizations.
* `report.md` — Final report with the recommendation, prediction interval assessment, residual findings, and proposed next step.
* `brief.md` — Original project instructions.
* `rubric.md` — Project grading criteria.

## Recommendation

AutoARIMA is the preferred model based on the rolling-origin evaluation results. Further work should focus on improving prediction interval calibration before relying on the forecast intervals for decision-making.
