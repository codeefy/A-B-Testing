# Facebook Ad Bidding  A/B Test Analysis



🗂️ **Case Study Problem**

**Background**

**Facebook, one of the world's largest digital advertising platforms, continuously experiments with new features to improve outcomes for both advertisers and the platform. In this case, Facebook's product team introduced a new bidding mechanism called Average Bidding as an alternative to the long-standing Maximum Bidding system.**

**Under Maximum Bidding, advertisers define a hard ceiling — the most they are ever willing to pay per ad impression. Facebook's algorithm bids up to (but never beyond) that ceiling when deciding whether to show the ad**

**Under Average Bidding, advertisers instead define a target average spend per impression. Facebook's algorithm dynamically bids higher or lower on individual auctions, but aims to keep the average spend near the stated target over time. This flexibility allows Facebook to target more valuable, high-intent users — even if it occasionally costs more per impression — while compensating by bidding less on lower-value impressions.**


## 📌 Table of Contents

- [Business Context](#-business-context)
- [The Experiment](#-the-experiment)
- [Project Structure](#-project-structure)
- [Tech Stack](#-tech-stack)
- [Methodology](#-methodology)
- [Key Results & Insights](#-key-results--insights)
- [Funnel Analysis](#-funnel-analysis)
- [Derived KPIs](#-derived-kpis)
- [Statistical Validation](#-statistical-validation)
- [Confidence Interval](#-confidence-interval)
- [Business Recommendation](#-business-recommendation)
- [How to Run](#-how-to-run)

---

## 🏢 Business Context

Digital advertising platforms like Facebook offer advertisers multiple bidding strategies to control how their budget is spent. Two of the most common are:

| Strategy | Description |
|---|---|
| **Maximum Bidding** *(Control)* | Advertiser sets the **maximum** they're willing to pay per impression. Facebook never exceeds this ceiling. |
| **Average Bidding** *(Test)* | Advertiser sets the **average** they're willing to pay. Facebook optimizes bids up and down around this average. |

**The Business Question:**
*Does switching from Maximum Bidding to Average Bidding generate more revenue for advertisers  and is the difference statistically significant?*

This question directly impacts:
- **Advertisers** : which strategy gives them better ROI on ad spend
- **Facebook / Meta** : which bidding model drives more platform revenue
- **Product & Growth teams** : whether to deprecate, promote, or A/B expose this feature further


## 🧪 The Experiment

| Parameter | Detail |
|---|---|
| **Test Type** | Two-sample A/B Test |
| **Control Group** | Maximum Bidding (existing feature) |
| **Test Group** | Average Bidding (new feature) |
| **Duration** | 40 days |
| **Sample Size** | 40 observations per group (80 total) |
| **Primary Metric** | Earning (Revenue) |
| **Secondary Metrics** | Impressions, Clicks, Purchases |
| **Significance Level (α)** | 0.05 |
| **Statistical Power (1-β)** | 0.80 |

---



The dataset contains two CSV files - one per group-each with **40 daily observations** and **4 features**:

| Column | Description |
|---|---|
| `Impression` | Number of times the ad was shown to users |
| `Click` | Number of times users clicked on the ad |
| `Purchase` | Number of purchases made after clicking |
| `Earning` | Revenue generated from those purchases |

**Data Quality:** ✅ No missing values in either group. Both datasets are clean and ready for analysis.

---

## 📁 Project Structure

```
facebook-ab-test/
│
├── data/
│   ├── control_group.csv       # Maximum Bidding group (40 days)
│   └── test_group.csv          # Average Bidding group (40 days)
│
├── AB_testing.ipynb            # Main analysis notebook
├── README.md                   # Project documentation
└── requirements.txt            # Python dependencies
```

---

## 🛠 Tech Stack

| Tool | Purpose |
|---|---|
| **Python 3.13** | Core programming language |
| **Pandas** | Data loading, cleaning, transformation |
| **NumPy** | Numerical computations, bootstrap sampling |
| **SciPy** | Statistical tests (t-test, Levene's test) |
| **Matplotlib** | Distribution histograms |
| **Plotly** | Interactive funnel chart visualization |

---

## 🔬 Methodology

The analysis follows a structured, end-to-end data science workflow:

```
1. Data Loading & Inspection
        ↓
2. Exploratory Data Analysis (EDA)
        ↓
3. Comparative Metric Analysis
        ↓
4. Funnel Analysis
        ↓
5. Derived KPI Computation
        ↓
6. Hypothesis Testing
   ├── Levene's Test (variance equality check)
   └── Two-Sample t-Test (mean comparison)
        ↓
7. Bootstrap Confidence Interval
        ↓
8. Sample Size Validation
        ↓
9. Business Conclusion & Recommendation
```

### Hypothesis

**H₀ (Null):** There is no significant difference in earnings between Maximum Bidding and Average Bidding.

**H₁ (Alternative):** Average Bidding generates significantly higher earnings than Maximum Bidding.

---

## 📈 Key Results & Insights

### Overall Performance Comparison

| Metric | Control (Max Bid) | Test (Avg Bid) | Change |
|---|---|---|---|
| **Impressions** | 101,711 | 120,512 | 🟢 +18.5% |
| **Clicks** | 5,100 | 3,967 | 🔴 −22.2% |
| **Purchases** | 550.9 | 582.1 | 🟢 +5.65% |
| **Earnings** | 1,908.58 | 2,514.93 | 🟢 **+31.77%** |

### 💡 Key Insight

Average Bidding reaches **18% more users** and generates **31.8% more revenue**, despite attracting **22% fewer clicks**. This means fewer but more relevant, high-intent users are clicking-leading to better conversions and higher-value purchases.

---

## 🔻 Funnel Analysis
![Funnel Analysis Chart](Asset/funnel%20Comparison.png)

The funnel tracks user progression through the ad journey: **Impression → Click → Purchase → Earning**

| Funnel Stage | Control | Test | Interpretation |
|---|---|---|---|
| **Impression → Click (CTR)** | 5.01% | 3.29% | Test attracts broader but less click-happy audience |
| **Click → Purchase (CVR)** | 10.80% | **14.67%** | 🟢 Test users who click are more likely to buy -better targeting |
| **Purchase → Earning** | 346.45% | **432.08%** | 🟢 Test generates higher revenue per  purchase-higher-value orders |

### What This Tells Us

- **Lower CTR is not a red flag.** The test group trades volume for quality-fewer clicks, but far more conversions and revenue per click.
- **Average Bidding appears to attract higher purchase-intent users**, possibly because the flexible bidding algorithm optimizes for audiences more likely to convert rather than simply maximizing reach.
- **Revenue per purchase is 24.7% higher** in the test group, suggesting Average Bidding may surface higher-value customers or product segments.

---

## 📊 Derived KPIs
![Funnel Analysis Chart](Asset/metric%20Comparision.png)


These efficiency metrics reveal how well each strategy monetizes user engagement:

| KPI | Control (Max Bid) | Test (Avg Bid) | Lift |
|---|---|---|---|
| **Earning per Click** | $0.37 | **$0.63** | +70.3% |
| **Earning per Impression** | $0.0188 | **$0.0209** | +11.2% |
| **Purchase per Click** | 0.1080 | **0.1467** | +35.8% |
| **Earning per Purchase** | $3.46 | **$4.32** | +24.9% |

**Earning per Click is the standout metric** — the test strategy generates **70% more revenue per click**. This is the clearest indicator that Average Bidding delivers superior monetization efficiency.

---

## ✅ Statistical Validation

### Step 1 - Levene's Test (Variance Equality)

Before running the t-test, variance homogeneity between groups was verified using **Levene's Test**.

- The result determined which variant of the t-test to apply (equal variance vs. Welch's t-test).

### Step 2 — Two-Sample t-Test

| Stat | Value |
|---|---|
| **Mean Earning (Control)** | 1,908.58 |
| **Mean Earning (Test)** | 2,514.93 |
| **t-statistic** | −9.2561 |
| **p-value** | 1.72 × 10⁻¹⁴ |
| **Cohen's d** | −2.0697 |
| **Result** | ✅ **Reject H₀** |

### Interpretation

**The p-value of **1.72 × 10⁻¹⁴** is astronomically smaller than α = 0.05.**
**The probability this result is due to chance is essentially **zero**.
**Cohen's d of **−2.07** indicates a **large effect size** — this is not a marginal gain, it is a substantial, meaningful difference.**

---

## Confidence Interval

A **Bootstrap Confidence Interval** (5,000 iterations) was computed to estimate the true range of the earnings uplift:

```
95% Confidence Interval (Test − Control Earnings): [478.07, 728.28]
```

**Interpretation:** We are **95% confident** that switching to Average Bidding increases daily earnings by **between $478 and $728 per campaign**, compared to Maximum Bidding.

### Sample Size Validation

Using the power analysis formula with α = 0.05 and β = 0.20:

```
Required sample size per group: 69
Actual sample size per group:   40
```

⚠️ The experiment ran with fewer observations than the theoretically recommended 69. However, given the **extremely low p-value (10⁻¹⁴)** and **large effect size (Cohen's d = 2.07)**, the test results are highly robust and the conclusion holds with confidence.

---

## 🎯 Business Recommendation

### ✅ Recommendation: **Roll out Average Bidding to all advertisers**

The evidence from this 40-day experiment is conclusive:

| Factor | Evidence |
|---|---|
| **Revenue uplift** | +31.8% increase in average daily earnings |
| **Statistical confidence** | p-value = 1.72 × 10⁻¹⁴ (near-zero chance of randomness) |
| **Effect size** | Cohen's d = 2.07 (large effect) |
| **Revenue range** | $478–$728 daily earnings increase per campaign (95% CI) |
| **Efficiency** | +70% earning per click, +35% purchase rate per click |

### Strategic Implications

1. **For Advertisers:** Average Bidding delivers meaningfully better ROI. Advertisers should migrate from Maximum Bidding or use Average Bidding as the default strategy for revenue-focused campaigns.

2. **For Facebook / Meta Product Team:** This feature drives measurable platform revenue improvement. Consider making Average Bidding the **default bidding option**, with Maximum Bidding available as an advanced setting.

3. **For Marketing Teams:** The lower CTR under Average Bidding should not be misread as underperformance. Teams should update their KPI dashboards to **prioritize Earning per Click and Purchase CVR** over raw click volume.

4. **Next Steps:**
   - Replicate the test with a larger sample (n ≥ 69 per group) to close the sample size gap
   - Segment results by campaign type, industry vertical, and ad format to understand where Average Bidding performs best
   - Monitor long-term effects over 90–180 days to check for saturation or novelty effects

---

## ▶️ How to Run

### 1. Clone the repository

```bash
git clone https://github.com/your-username/facebook-ab-test.git
cd facebook-ab-test
```

### 2. Install dependencies

```bash
pip install pandas numpy scipy matplotlib plotly
```

Or use the requirements file:

```bash
pip install -r requirements.txt
```

### 3. Launch the notebook

```bash
jupyter notebook AB_testing.ipynb
```

### Requirements

```
pandas
numpy
scipy
matplotlib
plotly
jupyter
```


