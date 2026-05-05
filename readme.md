# A/B Testing Analysis: Control Group vs Test Group

## Project Overview

This project analyzes an A/B test conducted to evaluate whether a new strategy improves business performance compared to the existing control setup. The experiment compares two groups:

- **Control group**: current/baseline experience
- **Test group**: new/changed experience

The analysis focuses on the business funnel:
**Impressions → Clicks → Purchases → Earnings**

The goal is to determine whether the test variant creates a meaningful uplift in revenue and user behavior.

---

## Business Problem

The business needed to answer a simple but important question:

> **Does the test strategy improve monetization enough to justify rollout?**

In product and marketing experiments, it is not enough to see a visual difference between groups. The result must also be:
- statistically reliable,
- practically meaningful,
- and aligned with business goals.

---

## Objective

The objectives of this analysis were to:

1. Compare control vs test performance across key funnel metrics.
2. Measure conversion efficiency using derived metrics such as CTR and CVR.
3. Test whether the difference in earnings is statistically significant.
4. Estimate the likely uplift in earnings using confidence intervals.
5. Decide whether the test variant should be recommended for rollout.

---

## Dataset

Two CSV files were used:

- `control_group.csv`
- `test_group.csv`

The working dataframes were:

- `df_control`
- `df_test`

Each group contains **40 observations**, so the full dataset contains **80 rows** total.

### Columns used
- `Impression`
- `Click`
- `Purchase`
- `Earning`

---

## Why This Analysis Matters

A/B testing is useful because it helps answer whether a new idea improves business outcomes without relying on guesswork.

In this case:
- **Impressions** show reach
- **Clicks** show engagement
- **Purchases** show conversion intent
- **Earnings** show actual business value

For business decisions, **earnings** is the most important metric because it directly reflects monetization.

---

## Exploratory Summary

### Control Group
- Mean impressions: **101,711.45**
- Mean clicks: **5,100.63**
- Mean purchases: **550.90**
- Mean earnings: **1,908.58**

### Test Group
- Mean impressions: **120,512.43**
- Mean clicks: **3,967.55**
- Mean purchases: **582.05**
- Mean earnings: **2,514.93**

---

## Initial Business Interpretation

The test group shows a mixed pattern:

- **Higher impressions** than control
- **Lower clicks** than control
- **Higher purchases** than control
- **Much higher earnings** than control

This suggests that the test variant may be bringing in more reach and better monetization quality, even though top-of-funnel engagement dropped.

---

## Derived Metrics

To understand efficiency, the following metrics were derived:

### CTR
\[
CTR = \frac{Clicks}{Impressions}
\]

### CVR
\[
CVR = \frac{Purchases}{Clicks}
\]

### Revenue Efficiency
- Earnings per Click
- Earnings per Purchase

These derived metrics help explain *why* revenue changed, not just *whether* it changed.

---

## Distribution Analysis

Skewness values for both groups were close to zero for all key metrics.

### Interpretation
- Both control and test distributions were approximately symmetric.
- No strong skewness or extreme distortion was observed.
- This supports the use of parametric testing such as the t-test.

This is important because it suggests the result is not being driven by a few unusual outliers.

---

## Sample Size Planning

Before testing, a sample size calculation was performed using:

- **Alpha = 0.05**
- **Beta = 0.2**
- **Power = 80%**
- **Expected effect size = ₹200**
- **Variance-based formula** for continuous metric (`Earning`)

### Result
The required sample size came out to **69 observations per group**.

### Available data
- Control: **40**
- Test: **40**

### Interpretation
The available sample is smaller than the planned sample size, so the experiment is **underpowered from a planning perspective**.

However, the observed effect turned out to be strong enough to still produce a highly significant result.

---

## Hypothesis Testing

A one-sided two-sample t-test was used to test whether the test group outperformed the control group in earnings.

### Hypotheses
- **H0**: Test earnings are not higher than control earnings
- **H1**: Test earnings are higher than control earnings

### Variance Check
Levene’s test was used to check whether the two groups had equal variance. Based on the result, the t-test was run with either:
- `equal_var=True`, or
- `equal_var=False`

This is a standard and statistically sound approach.

---

## Earnings Result

### Observed Means
- **Control mean earnings:** 1,908.575
- **Test mean earnings:** 2,514.925

### Difference
- **Uplift:** about **₹606.35 per observation**

### t-test result
- **t-statistic:** `-9.2561`
- **p-value:** `1.720180077421263e-14`

### Conclusion
The p-value is far below 0.05, so the null hypothesis is rejected.

This means the test group earnings are **statistically significantly higher** than the control group.

---

## Confidence Interval

A bootstrap confidence interval was calculated for the difference in earnings:

### 95% Confidence Interval (Test - Control)
**[₹478.07, ₹728.28]**

### Interpretation
- The entire interval is above zero.
- This confirms that the test group consistently outperforms the control group.
- The business can expect an uplift of roughly **₹478 to ₹728 per observation**.

This is very useful because it gives a practical range of expected impact, not just a yes/no answer.

---

## Business Interpretation

The test variant appears to be a **strong business win**.

### What improved
- Revenue / earnings increased substantially
- Purchases increased
- The uplift is statistically significant
- The confidence interval is fully positive

### What weakened
- Clicks decreased
- This suggests the test may be attracting fewer clicks, but the users who do engage are more valuable

### What this means
The test strategy seems to improve **quality over quantity**:
- fewer clicks,
- but stronger monetization and better final business value.

---

## Recommendation

### Recommended action
**Roll out the test variant cautiously, with monitoring.**

### Why
- Earnings improvement is statistically significant
- The uplift is large and practically meaningful
- Confidence interval supports a positive impact
- The result aligns with a business objective of increasing monetization

### Caveat
Since the sample size is smaller than the ideal planned sample size, it is still good practice to:
- collect more data,
- verify the trend again,
- and monitor guardrail metrics like CTR and user engagement.

---

## Limitations

This analysis has a few limitations:

1. **Small sample size**  
   The required sample size was 69 per group, but only 40 per group were available.

2. **Single metric focus**  
   Earnings was treated as the main business metric. Other metrics should still be monitored.

3. **Directional behavior in funnel**  
   Clicks dropped even though revenue increased, so the trade-off should be monitored after rollout.

---

## Key Takeaways

- The test group generated **significantly higher earnings** than the control group.
- The uplift is not just statistically significant, but also **business meaningful**.
- The confidence interval suggests the expected gain is stable and positive.
- Despite the smaller-than-ideal sample size, the result is strong enough to support a positive business decision.

---

## Final Conclusion

> The test variant outperformed the control group in earnings with a statistically significant and practically meaningful uplift. Although the experiment used fewer observations than the ideal required sample size, the observed effect is strong, the confidence interval is fully positive, and the result supports a positive rollout decision with continued monitoring.

---

## How to Run

### 1. Install dependencies
```bash
pip install pandas scipy numpy plotly statsmodels
```

### 2. Load data
```python
import pandas as pd

df_control = pd.read_csv("control_group.csv")
df_test = pd.read_csv("test_group.csv")
```

### 3. Run the notebook
Open `AB testing.ipynb` and execute the cells in order.

---

## Suggested Visualizations for Dashboard

For a polished dashboard, include:

- KPI cards for control vs test
- Funnel comparison chart
- Bar chart for raw metrics
- CTR and CVR comparison
- Box plot / histogram for distribution
- Earnings uplift chart with confidence interval

---

## Skills Demonstrated

- A/B testing
- Hypothesis testing
- Sample size planning
- Variance checking with Levene’s test
- Confidence intervals
- Business-focused interpretation
- Revenue analysis
- Python for data analysis
