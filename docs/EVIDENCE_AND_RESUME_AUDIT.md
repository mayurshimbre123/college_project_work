# Evidence audit for college project resume bullets

**Review method:** Examined actual notebook source cells and existing saved cell outputs, compared to earlier CV descriptions. Historical outputs are **not** independent fresh reproductions. Use the original notebooks for precise context.

| CV/portfolio claim | What the recovered notebook supports | Corrected representation |
|---|---|---|
| "Soil moisture prediction improved performance by 20%" | Linear: MSE **0.01523**, R² **0.00150**. Neural net: MSE **0.01510**, R² **0.00959**. Bagged tree: MSE **0.01515**, R² **0.00646**. No supporting 20%-improvement experiment. | "Compared linear regression, a feedforward neural network and bagged trees on satellite features; used EDA and error metrics, and identified weak held-out predictive signal." |
| "Tweet sentiment analysis using Logistic Regression and Naive Bayes" | Recovered notebook implements hand-built logistic regression and records **0.9950** test accuracy on NLTK `twitter_samples`; this file does not implement Naive Bayes. | "Implemented logistic regression with word-label frequency features and gradient descent for NLTK tweet sentiment; notebook records 99.5% held-out accuracy (not independently reproduced)." |
| "Synthetic GRU text generation, perplexity 7.23" | `GRULM()` contains embedding + two GRU layers; printed perplexity **7.2319922** after `model.init_from_file('model.pkl.gz')`. The separately shown training run used only one step. | "Implemented a Trax GRU language-model learning workflow; evaluated a supplied saved checkpoint at 7.23 perplexity in the original notebook." |
| "English Premier League data analysis" | GitHub hosts original EPL notebooks, `results.csv`, `stats (1).csv`; structured football results and team statistics are present. | "Explored EPL match and team statistics using Python data analysis and visualization; original notebooks and datasets archived." |

## Methodological corrections worth discussing in interviews

1. **Soil:** The original notebook uses `StandardScaler().fit_transform(X)` **before** `train_test_split`, which leaks test-distribution statistics. Split first; fit imputation/scaling only on training data using a `Pipeline`.
2. **Soil:** Original IQR filtering includes the target column and occurs before splitting. Prefer fit any outlier rule on training predictors only; keep test distribution untouched and report discarded examples. Compare against `DummyRegressor`.
3. **Soil:** R² near zero means the reported models explain almost none of the held-out target variance. Even if one MSE is numerically lower, don't frame this as strong predictive success.
4. **Sentiment:** The NLTK tweet sample's labels and vocabulary may make in-dataset classification easy; test on a new domain/time period before extrapolating 99.5% to real deployment.
5. **GRU:** Report the saved checkpoint's provenance separately from the one-step training demonstration. Don't claim the 7.23 result was achieved by the single training step.
6. **All:** Preserve original outputs, but clearly distinguish `recorded historical output`, `locally rerun`, `synthetic demonstration`, and `not reproduced`.

## Missing input artifacts and access boundaries

- `t_s1_am_6am.csv` needed for soil rerun — missing from inspected Library and original GitHub root.
- Shakespeare `data/` directory and `model.pkl.gz` for GRU — missing from inspected Library and original GitHub root.
- NLTK `twitter_samples` corpus — NLTK can download separately in a permitted environment; not rerun during this audit.
- Original EPL CSVs **are** on the existing GitHub repository; direct links are in the EPL report. No claim of fresh metric reproduction is made.
- IBM Skills Network virtual machine filesystem cannot be inspected through the current ChatGPT/GitHub connection. If original datasets live there, they need to be brought into an accessible folder for rerun.
