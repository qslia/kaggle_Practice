This line calculates the percentage of missing values for each column in the training dataset.

- `train_df.isnull().sum()` - counts missing values per column
- `/ len(train_df)` - divides by total number of rows to get proportion
- `* 100` - converts proportion to percentage

Result: a Series where each column name maps to its missing data percentage (e.g., 15.2 means 15.2% of values are missing).
---
This line filters and sorts missing value proportions in descending order.

Breaking it down:
- `missing_props[missing_props > 0]` - filters to keep only columns that have missing values (proportion greater than 0)
- `.sort_values(ascending=False)` - sorts the remaining columns by their missing value proportion from highest to lowest

So if `missing_props` originally contained all columns with their missing percentages (including 0% for complete columns), this line creates a new Series containing only the columns with missing data, ranked from most missing to least missing.
