**Forward fill (ffill)**: A method that propagates the last valid observation forward to fill missing values in sequential data.

**What the paragraph says**:

The author wants to use forward fill (ideal for time series because it carries forward the most recent known value), but **can't use it yet** because:
- The data isn't properly sorted by time (`ts_index`)
- The data isn't grouped by identifier columns (`code`/`sub_code`)

Without proper sorting/grouping, forward fill would incorrectly propagate values across different time series or out of chronological order.

**Solution**: Use median imputation as a safe, simple alternative that doesn't depend on data ordering.
---
**Forward fill example:**

Suppose you have a time series with missing values:

```python
import pandas as pd

data = pd.Series([10, None, None, 25, None, 30])
print("Original data:")
print(data)
# 0    10.0
# 1     NaN
# 2     NaN
# 3    25.0
# 4     NaN
# 5    30.0

print("\nAfter forward fill:")
print(data.ffill())
# 0    10.0
# 1    10.0  <- filled with previous value (10)
# 2    10.0  <- filled with previous value (10)
# 3    25.0
# 4    25.0  <- filled with previous value (25)
# 5    30.0
```

**What happened:**
- Index 1 and 2: Missing values filled with the last known value (10)
- Index 4: Missing value filled with the last known value (25)

**Why it's good for time series:** It assumes that values remain stable until a new observation is available, which is realistic for many time-dependent measurements (stock prices, sensor readings, etc.).