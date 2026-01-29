`.over` is a window function in Polars that allows you to perform calculations within specific groups while maintaining the original row count of the DataFrame.
---
import polars as pl

df = pl.DataFrame({
    "category": ["A", "A", "B", "B"],
    "sales": [10, 20, 100, 200]
})

result = df.with_columns(
    pl.col("sales").mean().over("category").alias("avg_by_cat")
)

print(result)
---
It is more similar to pandas **`groupby().transform()`** than a standard `groupby`.

**The key difference:**
A standard pandas `groupby` reduces the number of rows to the number of groups, whereas `.over()` (like `transform`) performs a grouped calculation but maps the results back to the original rows, keeping the DataFrame size unchanged.
