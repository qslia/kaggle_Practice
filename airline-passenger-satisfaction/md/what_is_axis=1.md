In **pandas**, the `axis` argument tells pandas whether to work **row-wise** or **column-wise**.

* **`axis=0`** → operate **down the rows** (i.e., across rows, affecting columns).

  * Often thought of as the "vertical axis".
  * Default in most operations.

* **`axis=1`** → operate **across the columns** (i.e., along each row).

  * Think of it as the "horizontal axis".

---

### Example 1: Dropping columns vs rows

```python
import pandas as pd

df = pd.DataFrame({
    "A": [1, 2, 3],
    "B": [4, 5, 6],
    "C": [7, 8, 9]
})

# Drop a column
print(df.drop("B", axis=1))
# Drops column B

# Drop a row
print(df.drop(0, axis=0))
# Drops the first row (index 0)
```

---

### Example 2: Summing

```python
df.sum(axis=0)  # sum each column (down the rows)
df.sum(axis=1)  # sum each row (across the columns)
```

---

📌 **Mnemonic**:

* `axis=0` → "go **down** (rows)", operate on **columns**.
* `axis=1` → "go **across** (columns)", operate on **rows**.

---

Do you want me to also make a **visual diagram** to help fix the difference between `axis=0` and `axis=1` in your memory?
