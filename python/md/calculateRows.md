Let me find the context around this line to explain it:


[1 tool called]

## Explanation of `n_rows = (len(features_to_plot) + n_cols - 1) // n_cols`

This formula computes the number of rows for a 2-column subplot grid. It uses integer division `//` to handle rounding.

### Breaking It Down:

```python
# From your code:
n_cols = 2
features_to_plot = [...]  # 15 items total
n_rows = (len(features_to_plot) + n_cols - 1) // n_cols
```

The calculation:
- `len(features_to_plot)`: total subplots (15)
- `n_cols`: columns per row (2)
- `n_rows`: rows needed

### How the Formula Works:

```
(15 + 2 - 1) // 2 = 16 // 2 = 8 rows
```

- Add `n_cols - 1` to round up via integer division
- `(15 + 1) // 2 = 8` ensures the grid fits all subplots

### Why This Formula?

- Without ceiling, dividing 15 by 2 yields 7 rows and leaves 1 item off grid.
- The `+ n_cols - 1` adjusts to ensure all subplots are included.

### General Formula:

Use:
```python
n_rows = (total_items + n_cols - 1) // n_cols
```
instead of:
```python
n_rows = total_items // n_cols  # This rounds DOWN
```

### In Your Case:
With 15 features and 2 columns:
- You get 8 rows and 2 columns
- Total grid: 16 subplots
- The 16th subplot remains empty

Result: all 15 plots fit on a 8×2 grid.