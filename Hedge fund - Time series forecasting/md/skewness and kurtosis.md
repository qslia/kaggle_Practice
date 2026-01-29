**Skewness** is a measure of the asymmetry of a probability distribution around its mean.

**Kurtosis** is a measure of the "tailedness" of a probability distribution, indicating the frequency of extreme values (outliers) relative to the center.
---
### Skewness Value
- **0**: Symmetric distribution (like a Normal Distribution).
- **Positive (> 0)**: Right-skewed (long tail on the right, most data concentrated on the left).
- **Negative (< 0)**: Left-skewed (long tail on the left, most data concentrated on the right).

### Kurtosis Value
- **3 (or 0 if using Fisher’s definition)**: Normal "mesokurtic" distribution.
- **Positive (> 3 / > 0)**: "Leptokurtic" (sharp peak, heavy tails) — more extreme outliers than a normal distribution.
- **Negative (< 3 / < 0)**: "Platykurtic" (flat top, thin tails) — fewer extreme outliers than a normal distribution.

*Note: Pandas uses "excess kurtosis" by default, so a normal distribution will have a kurtosis value of 0.*