# Soil moisture regression — reviewing my first pipeline

## 1. The question

Can satellite-derived variables (`VV`, `VH`, `smap_am`) predict observed `soil_moisture`? I tried a linear model, a feedforward neural net and bagged trees. These features and target are named directly in the original notebook.

## 2. Original pipeline

`read CSV → missing-value inspection → IQR outlier removal → correlation/feature plots → scale everything → train/test split → model fitting → R² and MSE`

The notebook's cell outputs show 30,747 initial rows and 26,989 rows after removal, with 4,574 flagged *cells* across columns (not 4,574 unique removed rows). There are 21,591 training rows and 5,398 test rows after the filtering.

## 3. Historical metrics (not freshly rerun)

| Model | Test MSE | Test R² |
|---|---:|---:|
| Linear regression | 0.01523 | 0.00150 |
| Feedforward neural network | 0.01510 | 0.00959 |
| Bagged decision trees | 0.01515 | 0.00646 |

Those R² values are very low. A previous statement about "20% better performance" cannot be confirmed using these metrics and should not appear in my resume.

## 4. What I would change now

The original notebook scaled features before train/test splitting. That allows test statistics into training transformations. I also removed rows as outliers *including the target* before splitting, which can distort the test distribution. The revised notebook in `reviewed/` demonstrates splitting first, training-only preprocessing, a mean-prediction baseline, and a reproducibility status marker.

## 5. Missing data and verification

Original filename: `t_s1_am_6am.csv` — **not recovered**. The revised notebook can execute on a labeled synthetic fixture to validate mechanics, but must not invent real soil prediction metrics. Put the CSV under `data/` after checking that redistribution is permitted; the `.gitignore` excludes it by default.

## 6. Interview framing

"I explored satellite-based soil moisture regression using three model families. When I audited the old notebook, the test R² values were near zero and I spotted preprocessing leakage. I rebuilt the evaluation path to split first and compare against a simple baseline. That taught me to distinguish a runnable pipeline from a useful predictive model."

MSE is the mean of squared residuals. R² is 1 minus the ratio of residual sum of squares to the sum of squared deviations from the test-target mean. Values near zero explain almost none of the test-target variation.
