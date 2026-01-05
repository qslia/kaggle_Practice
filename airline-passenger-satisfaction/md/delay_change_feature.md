# Delay Change During Flight

## What It Is
- Feature name: `Delay Change During Flight`.
- Definition: `Arrival Delay in Minutes - Departure Delay in Minutes`.
- Meaning:
  - Positive → the flight ended up more delayed than it left (lost time en‑route).
  - Zero → no net change during the flight.
  - Negative → the flight made up time and arrived less delayed than it departed.

## Why It’s Useful
- Captures in‑flight recovery or slippage beyond gate delays.
- Separates ground processes (boarding, taxi, ATC at origin) from en‑route performance.
- Often predictive for satisfaction and operational outcomes relative to raw delays.

## How To Create
```python
# Basic creation (vectorized)
train_df['Delay Change During Flight'] = (
    train_df['Arrival Delay in Minutes'] - train_df['Departure Delay in Minutes']
)

test_df['Delay Change During Flight'] = (
    test_df['Arrival Delay in Minutes'] - test_df['Departure Delay in Minutes']
)
```

## Robust Creation (types + missing)
```python
cols = ['Arrival Delay in Minutes', 'Departure Delay in Minutes']
for df in (train_df, test_df):
    # Ensure numeric; non-numeric coerces to NaN
    df[cols] = df[cols].apply(pd.to_numeric, errors='coerce')

    # Option 1: propagate NaN if either is missing (default arithmetic behavior)
    df['Delay Change During Flight'] = df['Arrival Delay in Minutes'] - df['Departure Delay in Minutes']

    # Option 2: impute missing before diff (choose imputation thoughtfully)
    # df['Delay Change During Flight'] = (
    #     df['Arrival Delay in Minutes'].fillna(0) - df['Departure Delay in Minutes'].fillna(0)
    # )
```

## Quick Sanity Checks
```python
# Examples
# Dep 30, Arr 10 → -20 (made up 20 minutes)
# Dep 0,  Arr 25 → 25  (lost 25 minutes)

# Basic distribution and spot-checks
train_df['Delay Change During Flight'].describe()
train_df[['Departure Delay in Minutes', 'Arrival Delay in Minutes', 'Delay Change During Flight']].head()
```

## Edge Cases
- Missing values: default arithmetic yields `NaN` if either delay is `NaN`. Decide whether to impute before or after.
- Negative delays: some datasets use negative to indicate early departure/arrival; differences remain meaningful but interpret accordingly.
- Outliers: extremely large positive/negative differences may reflect data errors; consider capping or robust scaling when modeling.

## Modeling Notes
- Apply the exact same transformation to both train and test to avoid discrepancies.
- Data leakage warning: if your prediction target must be known at departure time (e.g., predicting arrival delay from pre-departure info), do NOT construct features using actual arrival delay.
- For scale-sensitive models (e.g., linear models, distance-based methods), consider standardizing this feature.

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
train_df[['Delay Change During Flight']] = scaler.fit_transform(
    train_df[['Delay Change During Flight']]
)

test_df[['Delay Change During Flight']] = scaler.transform(
    test_df[['Delay Change During Flight']]
)
```

## Interpretation Tips
- Positive cluster → en‑route slippage or congestion; investigate routes, times, carriers.
- Negative cluster → effective time recovery; may correlate with longer cruise segments or favorable winds.
- Zero cluster → delays mostly explained by ground operations rather than flight phase.

