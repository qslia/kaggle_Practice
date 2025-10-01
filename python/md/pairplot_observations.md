# Pairplot Observations: Numeric Flight Features vs Satisfaction

## Overview
- Plot compares `Flight Distance`, `Departure Delay in Minutes`, `Arrival Delay in Minutes`, and `Delay Change During Flight`, colored by `satisfaction`.

## Key Patterns
- Strong linear tie between `Departure Delay` and `Arrival Delay` (near y=x), indicating arrival delays largely mirror departure delays with limited in‑flight correction on average.
- `Delay Change During Flight` relates as expected:
  - Negative correlation with `Departure Delay` (more departure delay → more time recovered in flight, i.e., negative change).
  - Positive correlation with `Arrival Delay` (larger arrival delay → more positive change, i.e., time lost).
- Delay variables are heavily right‑skewed with long tails; most flights cluster near low delays with a few extreme outliers.
- `Flight Distance` shows multiple modes and wide spread; relationships to delays are weak/heterogeneous.

## Class Separation (satisfied vs neutral/dissatisfied)
- Considerable overlap across all plots; no single feature cleanly separates classes.
- Slight trend: higher delays (both departure and arrival) associate with more neutral/dissatisfied points, but separation is modest.
- `Delay Change During Flight` shows limited class separation on its own; distributions largely overlap around zero.

## Distribution Notes
- Diagonal KDEs confirm: delays are sparse near zero with heavy right tails; `Delay Change` is tightly centered near zero with thin tails in both directions.
- Outliers exist for delays (hundreds to >1000 minutes); these may need capping or investigation.

## Modeling Implications
- Expect limited power from any single delay feature; interactions or nonlinear models may help.
- Consider transformations for skewed delays (e.g., log1p or winsorization/clipping) and scaling before distance‑based or linear models.
- Multicollinearity warning: `Departure Delay` and `Arrival Delay` are highly correlated; regularization or dropping one may help linear models.
- `Delay Change During Flight` adds incremental signal about in‑flight recovery/slippage, but likely small alone.

## Next Checks
- Quantify correlations (Pearson/Spearman) and class‑wise means/medians.
- Evaluate feature importance via a baseline model (e.g., regularized logistic regression or tree‑based).
- Inspect route/carrier/time‑of‑day interactions where delay impact on satisfaction may be stronger.

