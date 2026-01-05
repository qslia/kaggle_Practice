# Removing Extra Subplots with `fig.delaxes`

## Snippet
```python
for j in range(i + 1, len(axes)):
    fig.delaxes(axes[j])
```

## What It Does
- Iterates over axes after index `i` (i.e., `i+1` to the end).
- Calls `fig.delaxes(axes[j])` to remove each of those subplot axes from the figure.
- Result: the deleted subplots will not be drawn and no longer consume layout space.

## When To Use
- You created a grid of subplots but only need the first `k` of them.
- You are building a triangular layout (e.g., only lower triangle) and want to remove redundant upper‑triangle plots.
- You want a clean figure before `tight_layout()` or `constrained_layout` so empty axes don’t affect spacing.

## Why `delaxes` vs. Alternatives
- `fig.delaxes(ax)` or `ax.remove()` both detach the axes from the figure; the slot is freed for layout.
- `ax.set_visible(False)` only hides drawing but still occupies space in the layout—usually not desired.

## Minimal Example
```python
import matplotlib.pyplot as plt

# Suppose we prepare 1x4 subplots but only have 2 plots to show
fig, axs = plt.subplots(1, 4, figsize=(10, 3))

# Plot on the first two axes
axs[0].plot([1, 2, 3])
axs[1].scatter([1, 2, 3], [3, 2, 1])

# Remove the remaining axes to avoid empty panels
for j in range(2, len(axs)):
    fig.delaxes(axs[j])

fig.suptitle('Only first two subplots kept')
plt.tight_layout()
plt.show()
```

## Notes
- Ensure `axes[j]` belongs to `fig`; otherwise `delaxes` raises an error.
- If `axes` is 2D (e.g., from `plt.subplots(nrows, ncols)`), flatten it first: `axes = axes.ravel()`.
- Deleting axes changes `fig.axes`; avoid reusing deleted axes objects after removal.

