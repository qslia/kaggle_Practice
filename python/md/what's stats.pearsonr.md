Let me check the markdown file that was recently viewed, as it might contain relevant information about Pearson and Spearman correlations:


[1 tool called]

Now let me get more context around the `stats.pearsonr` function call in the notebook:


[1 tool called]

## `stats.pearsonr` Explanation

`stats.pearsonr` is a function from **SciPy's statistics module** that calculates the **Pearson correlation coefficient** along with its **p-value** for statistical significance testing.

### What it returns:
```python
r, p = stats.pearsonr(train_df['Departure Delay in Minutes'], train_df['Arrival Delay in Minutes'])
```

- **`r`**: The Pearson correlation coefficient (same as `r_pearson` calculated above)
- **`p`**: The p-value for testing the null hypothesis that the correlation is zero

### Key differences from pandas `.corr()`:

| Method | Returns | Purpose |
|--------|---------|---------|
| `train_df['col1'].corr(train_df['col2'], method='pearson')` | Just the correlation coefficient | Quick correlation calculation |
| `stats.pearsonr(col1, col2)` | Correlation coefficient + p-value | Statistical hypothesis testing |

### What the p-value tells you:
- **p < 0.05**: The correlation is statistically significant (reject null hypothesis)
- **p ≥ 0.05**: The correlation is not statistically significant (fail to reject null hypothesis)

### Why use `stats.pearsonr`?
1. **Statistical significance**: Determines if the observed correlation is likely due to chance
2. **Hypothesis testing**: Tests whether the true population correlation is zero
3. **Research validity**: Important for drawing meaningful conclusions from data

### In your airline data context:
- `r` will show how strongly departure delays correlate with arrival delays
- `p` will tell you if this correlation is statistically significant (not just random chance)
- You'd expect both a high `r` (strong correlation) and low `p` (statistically significant) since departure delays logically cause arrival delays

The comment "# With p-values (Pearson)" in your code indicates this is specifically for getting the statistical significance of the Pearson correlation.