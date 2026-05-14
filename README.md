# HSI Sentiment Analysis

This project analyzes sentiment in `HSI.xlsx` by using `up_votes` and `down_votes` as proxies for market mood, then comparing that sentiment against price movement in the Hang Seng Index.

A key part of the script is its use of a rolling time window. This lets the analysis focus on local market behavior over a short span of rows, rather than treating the data as isolated daily observations.

## What the script does

- Reads `HSI.xlsx` into a pandas DataFrame.
- Parses the `date` column and cleans the column names for easier handling.
- Converts the relevant numeric fields into usable numeric types.
- Preserves copies of the original sentiment columns for comparison.
- Uses a rolling median-based Median Absolute Deviation approach to decide how missing sentiment values should be handled.
- If local volatility is high, missing sentiment defaults to a neutral `50 / 50` split.
- If local volatility is low, missing sentiment is filled by linear interpolation.
- Computes `net_votes` as the difference between `up_votes` and `down_votes`.
- Calculates the market return over each time window using the relevant closing values.
- Plots sentiment against window-based market return in a scatter plot.

## Output

If the script runs successfully, it produces:

- `HSI_output.csv`
- A plot comparing `net_votes` with the window-based market return

## Assumptions

- The rows in the Excel file are already sorted in time order.
- The analysis works on row position, not on exact calendar spacing.
- Missing vote values are handled using the MAD-based imputation rule.
- This is an exploratory analysis workflow, not a production forecasting model.
