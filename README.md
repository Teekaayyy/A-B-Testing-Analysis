# Project 08: A/B Testing Analysis
### Did the Change Actually Work? A Complete Statistical Testing Framework

---

## Business Brief

A company redesigned a landing page and wants to know if the new version converts better. Most people compare two conversion rates, see a difference, and declare a winner. That is not A/B testing. That is guessing with extra steps.

This project runs a complete, rigorous A/B test covering sanity checks, sample size validation, hypothesis testing, practical significance, and a sequential analysis chart.

---

## Dataset

| Property | Detail |
|----------|--------|
| **Name** | A/B Testing Dataset |
| **Direct Link** | https://www.kaggle.com/datasets/zhangluyuan/ab-testing |
| **Records** | 294,478 user sessions |
| **Groups** | Control (old page) vs Treatment (new page) |
| **Target** | Converted: 0 or 1 |

---

## What Makes This Different

- Runs sanity checks to detect contaminated groups before any testing
- Validates sample size against required statistical power
- Uses the correct test (z-test for proportions, not t-test)
- Tests both statistical AND practical significance
- Includes a sequential p-value chart showing when the result stabilised
- Ends with a clear go or no-go recommendation with full justification

---

## Project Structure

```
ab-testing-analysis/
├── project_08_ab_testing.ipynb
└── README.md
```

---

## Kaggle Setup

1. Search **"ab-testing"** by *zhangluyuan* on Kaggle and attach it
2. Upload `project_08_ab_testing.ipynb`
3. Run the path finder cell first
4. Update `DATA_PATH` in Cell 3 if needed
5. Run all cells

---

## Notebook Walkthrough

### Section 1: Setup
Libraries including scipy and statsmodels. Test parameters defined upfront: alpha=0.05, power=0.80, minimum detectable effect=1 percentage point.

### Section 2: Load Data
Auto-detects CSV files. Loads and prints column names and sample rows.

### Section 3: Sanity Checks
Four checks before any test is run:
- Group imbalance: are control and treatment roughly 50/50?
- Cross-contamination: did any users appear in both groups?
- Landing page mismatch: did users see the wrong page for their group?
- Duplicate user IDs: was anyone counted more than once?
Rows failing these checks are removed with counts printed.

### Section 4: Baseline Conversion Metrics
Calculates conversion rates for both groups. Computes absolute difference and relative lift. Compares against minimum detectable effect to assess practical significance.

### Section 5: Sample Size Validation
Uses NormalIndPower to calculate required sample size per group for the chosen alpha, power, and MDE. Compares required vs actual sample size. Prints a pass or warning.

### Section 6: Hypothesis Testing
Formal hypothesis statement (H0 and H1). Two-proportion z-test using proportions_ztest. 95% confidence intervals for both groups. Plain-English decision and recommendation.

### Section 7: Test Results Visualisations
Three charts:
- Bar chart with 95% confidence interval error bars
- P-value gauge showing observed p vs alpha threshold
- Bootstrapped conversion rate distributions (2,000 bootstrap samples)

### Section 8: Sequential P-Value Chart
Calculates cumulative p-value as each user is added (sampled for performance). Line chart showing how the p-value evolved over time with alpha threshold line. Marks the exact sample size where significance was first reached. This answers: was the result stable or did it only barely cross the line at the end?

### Section 9: Power Analysis
Power curve showing what effect sizes are detectable at 80% power with the actual sample size. Highlights the adequate power region. Contextualises whether a non-significant result means no effect exists or the test was underpowered.

### Section 10: Executive Summary Dashboard
Dark-theme KPI cards: control conversion, treatment conversion, absolute difference, p-value, test decision, recommendation.

### Section 11: Findings and Conclusions
Framework table mapping each analysis step to its purpose. Four common A/B testing mistakes with explanations of how this analysis avoids each one.

---

## Key Concepts Covered

| Concept | Where Used |
|---------|-----------|
| Two-proportion z-test | Section 6 |
| Statistical vs practical significance | Sections 4 and 6 |
| Sample size and statistical power | Section 5 |
| Bootstrap confidence intervals | Section 7 |
| Sequential testing | Section 8 |
| Power curve analysis | Section 9 |

---

## Tools Used

| Tool | Purpose |
|------|---------|
| Python (Pandas, NumPy) | Data manipulation |
| Scipy | Stats tests |
| Statsmodels | proportions_ztest, proportion_confint, NormalIndPower |
| Plotly | Interactive dashboard |
| Matplotlib | Sequential chart, power curve, results panel |

---

*Built by Jessica Dan-Odhomo - [LinkedIn](https://www.linkedin.com/in/jessica-dan-odhomo) - [GitHub](https://github.com/Teekaayyy)*
