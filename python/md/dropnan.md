Yes. `train_df.dropna()` removes all rows with missing values (NaN).

## `dropna()` Default Behavior

```python
train_df = train_df.dropna()
```

This method:
- Drops any row with at least one missing value.
- Returns a DataFrame with all complete rows.
- Modifies rows only (no changes to columns).

### Default Parameters:
```python
train_df.dropna(
    axis=0,      # Drop rows (default)
    how='any',    # Drop if ANY value in row is NaN (default)
    inplace=False # Return new DataFrame (default)
)
```

## Common Variations:

### 1. Drop rows with ANY missing value (default)
```python
train_df.dropna()  # Drops row if it has any NaN
```

### 2. Drop rows where ALL values are missing
```python
train_df.dropna(how='all')  # Only drops rows entirely NaN
```

### 3. Drop rows with missing values in specific columns
```python
train_df.dropna(subset=['Departure Delay', 'Arrival Delay'])
```

### 4. Drop columns instead of rows
```python
train_df.dropna(axis=1)  # Drop columns with missing values
```

## In Your Context:
Removing NaN rows lets `stats.pearsonr()` return valid values instead of NaN, so `r` and `p` will compute correctly. The downside is reduced sample size. Consider imputation (e.g., median/mean) if preserving rows matters.