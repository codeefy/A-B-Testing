# 📊 Facebook Ads A/B Testing: Revenue Optimization Case Study

---

## 📱 Business Context

This project simulates a real-world **Facebook Ads (Meta Ads) A/B testing scenario**, where a company is testing a new campaign strategy to improve revenue.

In digital marketing platforms like Facebook/Instagram, businesses continuously experiment with:

- Ad creatives  
- Audience targeting  
- Landing pages  
- Campaign strategies  

### The Core Question:

> “Does the new campaign strategy generate higher revenue per user compared to the current one?”

---

## 🎯 Problem Statement

The company wants to optimize its advertising performance.

Two strategies are being compared:

- **Control Group** → Existing campaign (baseline strategy)  
- **Test Group** → New campaign (optimized strategy)

The decision to roll out the new campaign depends on:

- Revenue improvement  
- Conversion efficiency  
- Statistical reliability  

---

## 🧪 Experiment Design

| Component | Description |
|----------|------------|
| Type | A/B Test |
| Groups | Control vs Test |
| Sample Size | 40 observations per group |
| Total Data | 80 observations |

### Metrics Tracked:
- Impressions → Reach  
- Clicks → Engagement  
- Purchases → Conversion  
- Earnings → Revenue (Primary Metric)  

---

## 🎯 Objective

1. Compare performance between control and test groups  
2. Evaluate conversion funnel efficiency  
3. Test statistical significance of earnings  
4. Estimate revenue uplift  
5. Make a business recommendation  

---

## 📊 Exploratory Analysis

### Control Group
- Earnings ≈ **₹1908**

### Test Group
- Earnings ≈ **₹2515**

👉 Initial observation:
- Revenue increased significantly in test group

---

## 🔍 Funnel Insight

| Stage | Observation |
|------|------------|
| Impressions | Increased |
| Clicks | Decreased |
| Purchases | Increased |
| Earnings | Strong increase |

### Interpretation:
The test strategy brings:
> **Fewer but higher-quality users**

---

## 📐 Sample Size Consideration

- Required sample size ≈ **69 per group**
- Available data = **40 per group**

### Insight:
> The experiment is slightly underpowered, so results must be interpreted carefully.

---

## 🧪 Hypothesis Testing

### Hypothesis:

- **H0**: Test does NOT improve earnings  
- **H1**: Test improves earnings  

### Method:
- Levene’s Test → Variance check  
- Two-sample t-test → Mean comparison  
- One-tailed test → Business-driven direction  

---

## 📊 Results

- Mean Difference ≈ **+₹606**
- t-statistic ≈ **-9.26**
- p-value ≈ **1.72e-14**

### Conclusion:

> The result is **statistically significant** (p < 0.05)

---

## 📈 Confidence Interval

**95% CI (Test − Control):**  
👉 **[₹478, ₹728]**

### Interpretation:

- Entire interval is positive  
- Strong and consistent uplift  
- Reliable business impact  

---

## 💰 Business Impact

> The new strategy increases earnings by approximately **₹478–₹728 per user**

At scale, this translates to:
- Significant revenue growth  
- Improved ROI on ad spend  

---

## ⚖️ Trade-Off Analysis

| Metric | Impact |
|--------|-------|
| CTR | Decreased ❌ |
| Conversion Rate | Increased ✅ |
| Revenue | Increased significantly ✅ |

### Insight:

> The strategy improves **quality over quantity**

---

## 🧠 Key Insight

> Not all clicks are valuable — the test group generates fewer clicks but higher revenue.

---

## 🚀 Recommendation

### ✅ Decision:
**Proceed with rollout of test strategy**

### ⚠️ With caution:
- Monitor CTR drop  
- Validate with larger sample  
- Track long-term performance  

---

## 📉 Limitations

1. Sample size < required threshold  
2. Short experiment duration  
3. Limited behavioral metrics  

---

## 🧠 What Would I Do Next?

- Collect more data (reach ≥ 69 per group)  
- Run experiment longer  
- Segment users (device, region, etc.)  
- Track retention & lifetime value  

---

## 🎯 Final Conclusion

> The test campaign delivers a statistically significant and practically meaningful increase in revenue. Despite a slightly smaller sample size, the strong effect size and confidence interval indicate that the strategy is promising and suitable for rollout with continued monitoring.

---

## 🛠️ Tools & Skills Used

- Python (Pandas, NumPy, SciPy)  
- A/B Testing  
- Hypothesis Testing  
- Confidence Intervals  
- Data Visualization (Plotly)  
- Business Analytics  

---

## 💡 Key Takeaway

> “Data-driven decisions are not just about significance—they are about impact.”

---