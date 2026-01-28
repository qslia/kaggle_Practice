`np.iinfo` returns machine limits for integer data types, providing attributes like `min` (minimum representable value) and `max` (maximum representable value) for a given integer type.
---
Let me explain with a concrete example:

```python
import numpy as np

# Get info for int8 (8-bit integer)
info = np.iinfo(np.int8)

print(f"Minimum value: {info.min}")  # -128
print(f"Maximum value: {info.max}")  # 127
```

**What it does:**
`np.iinfo(np.int8)` tells you the range of values that an `int8` data type can store:
- `int8` can hold integers from **-128 to 127**

**In your code (line 31):**
```python
if c_min > np.iinfo(np.int8).min and c_max < np.iinfo(np.int8).max:
```

This checks: "Can all values in this column fit within the int8 range (-128 to 127)?"
- If yes → convert the column to `int8` to save memory
- If no → try a larger integer type (like `int16`, `int32`, etc.)

**Purpose:** Memory optimization by using the smallest integer type that can safely hold the data.
---
This checks if the specified column contains any missing values (NaN), returning `True` if at least one missing value exists, `False` if all values are present.

- `.isnull()` - creates a boolean Series marking each value as True (missing) or False (present)
- `.any()` - returns True if any True exists in the Series
---
**Why use median:**
Median is robust to outliers—unlike mean, it won't be skewed by extreme values, making it a safer choice for imputation when data distribution is unknown.

**Why use train median for test:**
To prevent **data leakage**—if you calculate the test set's median separately, you're using information from the test set during preprocessing, which the model shouldn't have access to in a real-world scenario. 

**Correct approach:**
1. Calculate median from training data only
2. Apply that same median value to fill missing values in both train and test sets

This simulates real deployment where you only have historical (training) data to derive statistics, and future (test) data must be processed using those pre-computed values.
---
`pd.concat([train_df[col], test_df[col]])` combines the specified column from both train and test dataframes into a single Series by stacking them vertically (appending test values after train values).

- `[train_df[col], test_df[col]]` - list of two Series to combine
- `pd.concat()` - concatenates them into one Series
- `.unique()` - then extracts all distinct values from the combined Series

Result: an array of all unique values that appear in that column across both datasets.
---
