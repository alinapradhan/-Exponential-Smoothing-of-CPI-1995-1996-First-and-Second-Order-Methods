# Exponential Smoothing of CPI (1995–1996): First and Second Order Methods

## Overview
This practical  demonstrates exponential smoothing applied to a short monthly Consumer Price Index (CPI) series for 1995–1996. The included R script  implements:

- First-order exponential smoothing (single exponential smoothing) with a user-specified smoothing parameter lambda.
- Second-order exponential smoothing (double smoothing) and a simple forecast formula based on the two smoothed series.

Both methods are illustrated with plots and printed result tables.

## Files
- TSA_Practical_09.R
  - Implements first- and second-order exponential smoothing on the CPI vector with plotting and printed output.
- README.md
  - This file: documentation and usage instructions.

## Purpose
- Show how exponential smoothing smooths a time series and produces short-term forecasts.
- Compare single and double smoothing outputs and demonstrate the forecast formula forecast[t] = 2*y1[t] - y2[t] (Holt's basic double-smoothing forecast without separate trend parameterization).
- Visualize the smoothed series vs observed series and inspect the tabulated results.

## Script summary 
- Data:
  - cpi: numeric vector of monthly CPI values (24 months: Jan 1995 — Dec 1996).
  - month: Date sequence of months matching cpi.
- Parameters:
  - lambda: smoothing constant (default in script = 0.3).
- First-order smoothing:
  - y_tilde[1] initialized to first observation.
  - y_tilde[t] = lambda*cpi[t] + (1-lambda)*y_tilde[t-1]
  - Result table printed and plotted (observed vs smoothed).
- Second-order smoothing:
  - y1: first smooth (same formula).
  - y2: smoothing applied to y1.
  - forecast[t] computed as 2*y1[t] - y2[t].
  - Results tabulated and plotted (observed vs forecast).
- Outputs:
  - data.frame result1: Month, Observation, Smoothed (first-order).
  - data.frame result2: Month, Observation, y1, y2, forecast (second-order).
  - Two plots produced: first-order smoothing and second-order smoothing forecast.

## How to run

From RStudio or an R console:
- Open and source the script:
  source

From a shell:
- Run with Rscript:
  Rscript 

You can change the smoothing parameter lambda inside the script and re-run to see how smoothing responsiveness changes.

## Dependencies
- Base R only. No external CRAN packages are required for the provided script.

## Expected output
- Console: printed data.frame with smoothed values (first order) and a data.frame with y1, y2 and forecast (second order).
- Plots:
  - Plot 1: Observed CPI points/line (blue) and first-order smoothed series (red).
  - Plot 2: Observed CPI points/line (blue) and second-order forecast/smoothed series (red).
- Typical outputs are numeric tables of smoothed values and visual comparisons that show smoothing lag and forecast behavior.

## Interpretation & notes
- Lambda controls responsiveness: higher lambda -> more weight to recent observations -> less lag, more variability; lower lambda -> smoother series with more lag.
- First-order exponential smoothing is appropriate for level series without trend or seasonality.
- The second-order smoothing implemented here combines two exponential smoothers and uses forecast[t] = 2*y1[t] - y2[t] as a simple extrapolation. This approximates a trend-aware forecast but is not the full Holt linear trend method that uses separate trend smoothing parameters.
- The double smoothing approach will respond better when a slow linear trend exists but may still lag depending on lambda.

## Troubleshooting
- If plots do not display, ensure your R graphical device is open (RStudio plots pane, or call png()/pdf() to save).
- If you try different lambda values and results diverge unexpectedly, verify initialization (y_tilde[1] and y1[1], y2[1] are set to cpi[1] in the script).
- For longer series or series with trend/seasonality, consider Holt's linear method (holt) or Holt-Winters (for seasonality) from the forecast package.

## Suggested next steps
- Add an automatic lambda selection (optimize an error metric such as MSE on in-sample one-step-ahead forecasts).
- Compare the current implementation with forecast::holt() and forecast::HoltWinters() results.
- Save the plots to files (png/pdf) and export result tables as CSV for reporting.

## License & Contact
This practical material is provided for educational use. For questions, improvements, or to contribute, contact the repository owner or maintainer.

```
