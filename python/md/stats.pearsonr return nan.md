Let me check the newly created markdown file about `stats.pearsonr` and then investigate why you're getting NaN values:


[2 tools called]

Let me search for any output or print statements that might show the NaN values:


[2 tools called]

Let me look for the actual output of the correlation calculation by searching for the cell that contains the stats.pearsonr call and its outputs:


[1 tool called]

Now let me check what's in that output cell and also look for any data quality issues:


[2 tools called]

Let me check what's being printed in those cells and also look for any data quality checks:


[2 tools called]

Let me check for any data quality analysis or missing value checks in the notebook:


[2 tools called]

Based on what I can see from the notebook outputs, here's why you're getting **NaN values** for both `r` and `p`:

## Why `r` and `p` are NaN

The **NaN (Not a Number)** values occur when `stats.pearsonr()` cannot calculate a valid correlation coefficient. This typically happens due to:

### 1. **Missing Values (Most Common Cause)**
- One or both columns (`'Departure Delay in Minutes'` or `'Arrival Delay in Minutes'`) contain **missing values** (NaN, None, or empty values)
- `stats.pearsonr()` cannot compute correlation when there are missing data points

### 2. **Constant Values**
- If one or both columns have **zero variance** (all values are the same)
- Example: All departure delays are 0, or all arrival delays are identical

### 3. **Insufficient Data**
- If there are too few valid data points after removing missing values

## How to Fix This

Here are the solutions you can try:

### **Solution 1: Check for Missing Values**
```python
# Check for missing values in both columns
print("Departure Delay missing values:", train_df['Departure Delay in Minutes'].isnull().sum())
print("Arrival Delay missing values:", train_df['Arrival Delay in Minutes'].isnull().sum())

# Check total missing values
print("Total missing:", train_df[['Departure Delay in Minutes', 'Arrival Delay in Minutes']].isnull().sum().sum())
```

### **Solution 2: Remove Missing Values**
```python
# Remove rows with missing values in either column
clean_data = train_df[['Departure Delay in Minutes', 'Arrival Delay in Minutes']].dropna()

# Then calculate correlation
r, p = stats.pearsonr(clean_data['Departure Delay in Minutes'], clean_data['Arrival Delay in Minutes'])
```

### **Solution 3: Use pandas corr() with dropna**
```python
# This automatically handles missing values
r_pearson = train_df['Departure Delay in Minutes'].corr(train_df['Arrival Delay in Minutes'], method='pearson')
```

## Why pandas `.corr()` Works But `stats.pearsonr()` Doesn't

- **pandas `.corr()`**: Automatically handles missing values by excluding them from the calculation
- **`stats.pearsonr()`**: Requires complete data and returns NaN when it encounters missing values

The fact that `r_pearson` shows `0.9654809013755736` (a valid correlation) but `r` and `p` are NaN confirms that there are missing values in your data that `stats.pearsonr()` cannot handle.