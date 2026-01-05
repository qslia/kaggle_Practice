# Correlation: What It Is and How To Use It

## Definition
- Correlation measures the strength and direction of association between two variables.
- Range: from -1 to +1.
  - +1: perfect positive association (as X increases, Y increases linearly).
  - 0: no linear association (could still be nonlinear).
  - -1: perfect negative association (as X increases, Y decreases linearly).

## Common Types
- Pearson r (linear): measures linear association between two numeric variables; sensitive to outliers and assumes roughly linear relationship.
- Spearman ρ (rank/monotonic): computes correlation on ranks; captures monotonic (not necessarily linear) trends; more robust to outliers and skew.
- Kendall τ (rank concordance): compares pairwise orderings; robust and interpretable for small samples.
- Point-biserial: Pearson correlation where one variable is binary (0/1), often used for label vs numeric feature.

## Quick Interpretation Guide
- |r| ≈ 0.1 small, 0.3 moderate, 0.5+ strong (rules of thumb; domain matters).
- Sign tells direction; magnitude tells strength.
- High correlation does not imply causation (confounders, reverse causality, common drivers).

## Python Examples
```python
import pandas as pd
import numpy as np
from scipy import stats

# Pearson and Spearman between two Series
r_pearson = train_df['Departure Delay in Minutes'].corr(train_df['Arrival Delay in Minutes'], method='pearson')
r_spearman = train_df['Departure Delay in Minutes'].corr(train_df['Arrival Delay in Minutes'], method='spearman')

# With p-values (Pearson)
r, p = stats.pearsonr(train_df['Departure Delay in Minutes'], train_df['Arrival Delay in Minutes'])

# Correlation matrix (Pearson by default)
features = ['Flight Distance', 'Departure Delay in Minutes', 'Arrival Delay in Minutes', 'Delay Change During Flight']
corr_mat = train_df[features].corr()

# Spearman matrix (more robust for skewed delays)
spearman_mat = train_df[features].corr(method='spearman')
```

## Visualizing a Correlation Matrix
```python
import seaborn as sns
import matplotlib.pyplot as plt

plt.figure(figsize=(6,4))
sns.heatmap(corr_mat, annot=True, fmt='.2f', cmap='vlag', center=0)
plt.title('Pearson Correlation (Flight Features)')
plt.show()
```

## Caveats and Pitfalls
- Nonlinearity: Pearson misses curved relationships; check scatterplots or use Spearman.
- Outliers: can inflate/flip Pearson; use robust methods or winsorize with care.
- Range restriction: limited variance can hide true relationships.
- Mixed types: do not correlate arbitrary codes (e.g., 1=Economy, 2=Business) with numeric features; use proper encodings.
- Autocorrelation/time: correlated errors inflate significance in time series; use appropriate models.
- Multiple testing: many correlations increase false positives; adjust (e.g., Benjamini–Hochberg).

## In Your Pairplot
- Expect high positive Pearson between `Departure Delay` and `Arrival Delay` (near y=x).
- `Delay Change During Flight` tends to correlate negatively with `Departure Delay` and positively with `Arrival Delay`.
- `Flight Distance` shows weak/heterogeneous correlation with delays.

## Going Further
- Partial correlation: correlation of X and Y controlling for Z (e.g., control for route or carrier).
- Confidence intervals: bootstrap r for uncertainty.
- For classification targets, use point-biserial or compare class-wise distributions and model-based feature importance.

