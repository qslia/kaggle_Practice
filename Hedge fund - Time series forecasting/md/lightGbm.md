LightGBM is a gradient boosting framework that uses tree-based learning algorithms, optimized for speed and efficiency with large datasets.
---
LightGBM was proposed by Microsoft Research in 2017, with the paper "LightGBM: A Highly Efficient Gradient Boosting Decision Tree" published at NIPS (Neural Information Processing Systems) 2017.
---
RMSE (Root Mean Square Error) is a metric that measures the average magnitude of prediction errors by taking the square root of the average squared differences between predicted and actual values.
---
`1 - RMSE` doesn't have a standard meaningful interpretation in machine learning because:

1. **RMSE has no upper bound** - it can be any positive value (0 to infinity), so `1 - RMSE` could be negative, making it unintuitive

2. **Scale-dependent** - RMSE is in the same units as your target variable. If your target ranges from 0-100, RMSE might be 15, making `1 - 15 = -14` meaningless

3. **Not normalized** - Unlike metrics bounded between 0 and 1 (like R², accuracy), RMSE doesn't naturally fit into `1 - metric` format

**What you might want instead:**
- **R² (R-squared)**: Already interpretable as "proportion of variance explained" (ranges 0 to 1, where higher is better)
- **1 - (RMSE / baseline_RMSE)**: Relative improvement over a baseline model
- **Normalized RMSE**: RMSE divided by the range or standard deviation of the target variable
---
I need to read the file to see what formula is in it.
The formula in the file is:

$$
\text{Score}
= \sqrt{
1 - \min\Big(
\max\Big(
\frac{\sum_{i\in I} w_i (y_i - \hat y_i)^2}
{\sum_{i\in I} w_i y_i^2},
0
\Big),
1
\Big)
}
$$

**What it is:**
A normalized, weighted error score for evaluating time series predictions, where:
- **Numerator**: Weighted sum of squared errors
- **Denominator**: Weighted sum of squared true values (normalizes by signal strength)
- **max(..., 0)**: Prevents negative ratios
- **min(..., 1)**: Caps ratio at 1
- **1 - clipped**: Flips error into score (lower error → higher score)
- **√**: Compresses differences near perfection, rewards real accuracy gains

**Score range**: 0 (worst) to 1 (perfect prediction)
---
No, it's **not RMSE** — it's more sophisticated.

**Key differences:**

1. **RMSE** (simple):
   $$\text{RMSE} = \sqrt{\frac{\sum (y_i - \hat{y}_i)^2}{n}}$$
   - Just averages squared errors
   - Scale-dependent (depends on target units)
   - Lower is better

2. **This formula** (normalized):
   $$\text{Score} = \sqrt{1 - \frac{\sum w_i (y_i - \hat{y}_i)^2}{\sum w_i y_i^2}}$$
   - **Weighted** errors (some predictions matter more)
   - **Normalized** by signal strength (scale-independent)
   - **Bounded** [0, 1] (always comparable)
   - Higher is better

**Relationship:**
It's closer to **1 - (weighted R²)** with a square root transformation, designed specifically to:
- Prevent overfitting near perfection
- Make the metric robust to different target scales
- Reward genuine predictive power over noise exploitation

So while it uses squared errors like RMSE, it's a much more refined competition metric.
---
This defines the hyperparameters for the LightGBM model:

- **`objective: 'regression'`** - Task type: predicting continuous numerical values
- **`metric: 'rmse'`** - Evaluation metric during training: Root Mean Squared Error
- **`boosting_type: 'gbdt'`** - Algorithm: Gradient Boosting Decision Trees
- **`learning_rate: 0.1`** - How much each tree contributes to the final prediction (smaller = slower but more accurate)
- **`num_leaves: 31`** - Maximum number of leaves per tree (controls model complexity)
- **`feature_fraction: 0.8`** - Randomly use 80% of features per tree (prevents overfitting)
- **`bagging_fraction: 0.8`** - Randomly use 80% of data samples per iteration (adds randomness)
- **`bagging_freq: 5`** - Apply bagging every 5 boosting iterations
- **`seed: 42`** - Random seed for reproducible results
- **`verbosity: -1`** - Suppress training output messages
- **`n_jobs: -1`** - Use all available CPU cores for parallel processing
---
