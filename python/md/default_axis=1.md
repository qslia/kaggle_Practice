Good question — let’s break it down clearly 👇

When you write:

```python
test_df.drop(columns=['id'], errors='ignore', inplace=True)
```

then **`axis=1` is implied by default**, because you used the keyword `columns=...`.

### Explanation:

* `DataFrame.drop()` has two main ways to specify what to remove:

  1. By **labels and axis**, e.g.

     ```python
     df.drop('colname', axis=1)
     ```
  2. By **columns or index** keywords, e.g.

     ```python
     df.drop(columns=['colname'])
     df.drop(index=[0, 1, 2])
     ```

If you use `columns=...`, pandas automatically sets `axis=1` internally.
So these two lines are **equivalent**:

```python
df.drop(columns=['id'])
df.drop(['id'], axis=1)
```

✅ **Answer:**
Yes — in

```python
test_df.drop(columns=['id'], errors='ignore', inplace=True)
```

`axis=1` is the default behavior because of the `columns=` argument.
