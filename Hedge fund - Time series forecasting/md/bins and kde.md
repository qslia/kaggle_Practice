**bins**: Number of intervals to divide the data range into for the histogram (100 means the data is split into 100 equal-width bars).

**kde**: Kernel Density Estimate - when `True`, overlays a smooth curve showing the probability density distribution of the data.
---
A boxplot is a statistical visualization that displays data distribution through quartiles, showing the median, interquartile range (box), and outliers (points beyond whiskers).
---
Probability density describes how probability is distributed across different values of a continuous variable—it's the height of the curve at any point, where higher values indicate that data points are more concentrated in that region.

**Key points:**

1. **Not a probability itself**: The density value at a point isn't a probability (can even be > 1), but the *area under the curve* between two points gives the probability of values falling in that range

2. **Interpretation**: 
   - Higher density = more data clustered around that value
   - Lower density = fewer observations in that region

3. **Total area = 1**: The entire area under the probability density curve always equals 1 (representing 100% of the data)

**Example**: If a KDE plot shows a peak at x=5 with density=0.8, it means values near 5 are common in your dataset, but to find P(4 < x < 6), you'd integrate (calculate area) under the curve from 4 to 6.
---
`plt.legend()` displays a legend box on the plot showing labels for each plotted element (in this case, 'Train' and 'Test' from the previous kdeplot calls).