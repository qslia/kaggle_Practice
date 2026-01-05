# Pairplot: Numeric Flight Features vs Satisfaction

## Purpose
- Visualize pairwise relationships among numeric flight features, colored by `satisfaction`.
- Assess class separation, linear/nonlinear trends, and univariate distributions.

## Code
```python
sns.pairplot(
    train_df[flight_features + ['satisfaction']],
    hue='satisfaction',
    diag_kind='kde',
    palette='Set2'
)
plt.suptitle("Numeric Flight Features vs Satisfaction", y=1.02)
plt.show()
```

## What Each Part Does
- `train_df[flight_features + ['satisfaction']]`: subsets the dataframe to only the numeric features you want and the target/class column.
- `hue='satisfaction'`: colors points and density curves by class for side‑by‑side comparison.
- `diag_kind='kde'`: shows kernel density estimates on the diagonal (one per class) instead of histograms.
- `palette='Set2'`: uses a readable, pastel color palette for classes.
- `plt.suptitle(..., y=1.02)`: adds a figure‑level title and nudges it upward to avoid overlap with the grid.
- `plt.show()`: renders the figure in the notebook.

Tip: For more control, capture the grid and set the title via the figure.
```python
g = sns.pairplot(train_df[flight_features + ['satisfaction']], hue='satisfaction', diag_kind='kde', palette='Set2')
g.fig.suptitle("Numeric Flight Features vs Satisfaction", y=1.02)
# Optional spacing if title overlaps
# g.fig.subplots_adjust(top=0.95)
plt.show()
```

## Requirements & Assumptions
- `flight_features` is a list of numeric column names.
- Column `satisfaction` exists and is categorical (or will be treated as such). If it is numeric (e.g., 0/1), it will still work; you can also cast to string for clearer legends:
  ```python
  train_df['satisfaction'] = train_df['satisfaction'].astype(str)
  ```
- Imports present: `import seaborn as sns`, `import matplotlib.pyplot as plt`.

## Interpretation
- Diagonal KDEs: view the distribution of each feature by class; separation indicates discriminative power.
- Off‑diagonal scatterplots: look for clustering, linear trends, or separability between classes.
- Heavy overlap usually implies that feature alone (or pairwise) has limited class separation.

## Practical Tips
- Performance: pairplots scale poorly with many rows/features.
  - Sample rows: `df_plot = train_df.sample(n=5000, random_state=42)`
  - Reduce redundancy: `sns.pairplot(..., corner=True)`
- Readability:
  - Transparency: `plot_kws={'alpha': 0.3, 's': 12, 'edgecolor': 'none'}`
  - Diagonal fill: `diag_kws={'fill': True}`
  - Size: `height=2.0, aspect=1.0`
- Scale mismatch: if features vary widely in scale, consider standardizing for clearer patterns (only for visualization; keep original for modeling if needed).

## Example With Enhancements
```python
df_plot = train_df.sample(n=5000, random_state=42) if len(train_df) > 5000 else train_df

g = sns.pairplot(
    df_plot[flight_features + ['satisfaction']],
    hue='satisfaction',
    diag_kind='kde',
    palette='Set2',
    corner=True,
    plot_kws={'alpha': 0.35, 's': 12, 'edgecolor': 'none'},
    diag_kws={'fill': True},
    height=2.2,
)

g.fig.suptitle("Numeric Flight Features vs Satisfaction", y=1.02)
plt.show()
```
