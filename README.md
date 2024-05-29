# Testing analysis
 import pandas as pd
import numpy as np
from scipy import stats

# Sample data for A/B testing
data = {
    'group': np.random.choice(['A', 'B'], size=1000),
    'conversion': np.random.randint(0, 2, size=1000)
}

df = pd.DataFrame(data)

# Separate the data into groups
group_a = df[df['group'] == 'A']
group_b = df[df['group'] == 'B']

# Calculate conversion rates
conversion_rate_a = group_a['conversion'].mean()
conversion_rate_b = group_b['conversion'].mean()

print(f"Conversion rate for group A: {conversion_rate_a:.2f}")
print(f"Conversion rate for group B: {conversion_rate_b:.2f}")

# Perform a t-test to compare the conversion rates
t_stat, p_value = stats.ttest_ind(group_a['conversion'], group_b['conversion'])

print(f"T-statistic: {t_stat:.2f}")
print(f"P-value: {p_value:.2f}")

# Determine if the result is statistically significant
alpha = 0.05
if p_value < alpha:
    print("The result is statistically significant.")
else:
    print("The result is not statistically significant.")
