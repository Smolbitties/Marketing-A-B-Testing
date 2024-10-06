# A/B Testing: Ads vs. Public Service Announcements (PSAs)

## Project Overview

This project performs an A/B testing analysis to statistically compare the conversion rates between two groups: 'ad' and 'psa' using Python. It helps to determine if there is a statistically significant difference between the conversion rates of these two groups.

## Data Description

The data contains the following columns:
- `user_id`: Unique identifier for each user.
- `test_group`: Denotes whether the user was in the 'ad' or 'psa' group.
- `converted`: 1 if the user converted (i.e., took the desired action), 0 otherwise.

## Methods

### Conversion Rate Calculation
We calculate the conversion rate for both groups as the number of users who converted divided by the total number of users in each group.

```python
conversions_ad = df[df['test group'] == 'ad']['converted'].sum()
total_ad = df[df['test group'] == 'ad'].shape[0]

conversions_psa = df[df['test group'] == 'psa']['converted'].sum()
total_psa = df[df['test group'] == 'psa'].shape[0]
```
A/B Testing
A two-sample z-test for proportions is applied to compare the conversion rates between the 'ad' and 'psa' groups.
```
from statsmodels.stats.proportion import proportions_ztest
counts = np.array([conversions_ad, conversions_psa])
nobs = np.array([total_ad, total_psa])

z_stat, p_value = proportions_ztest(counts, nobs)
print(f"Z-statistic: {z_stat}, P-value: {p_value}")
```
Interpretation
Based on the p-value, we determine if there is a significant difference in conversion rates.
The z-statistic and p-value calculated from the A/B test will help to decide whether to reject the null hypothesis. If the p-value is less than 0.05, there is a statistically significant difference between the ad and psa groups, otherwise, there is no significant difference.
