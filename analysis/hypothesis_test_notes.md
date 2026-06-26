# Hypothesis Test Notes — Paid Conversion Rate
## t-Test: Two-Sample Assuming Unequal Variances (Welch's t-Test)

**Tool:** Excel Data Analysis ToolPak  
**Variable tested:** `converted_to_paid` (binary: 0 = not converted, 1 = converted)

---

## Hypotheses

| | |
|---|---|
| **Null Hypothesis (H0)** | The mean paid conversion rate of the Control group equals that of the Treatment group. (μ_Control = μ_Treatment) |
| **Alternate Hypothesis (H1)** | The mean paid conversion rate of the Treatment group is greater than that of the Control group. (μ_Treatment > μ_Control) |
| **Test Direction** | One-tailed (right-tailed) — testing for improvement in Treatment only |
| **Significance Level (α)** | 0.05 |
| **Metric Tested** | Paid Conversion Rate |
| **Reason for Metric** | Paid conversion is the North Star metric — it directly measures whether the new campaign drives users to become paying customers |

---

## Test Inputs

| Input | Control | Treatment |
|---|---|---|
| Mean | 0.031884058 (3.19%) | 0.070422535 (7.04%) |
| Variance | 0.030912265 | 0.065555533 |
| Observations (n) | 690 | 710 |
| Hypothesized Mean Difference | 0 | |

---

## Test Output

| Statistic | Value |
|---|---|
| Degrees of Freedom (df) | 1,259 |
| t Statistic | −3.290977801 |
| P(T≤t) one-tail | **0.000513031** |
| t Critical one-tail | 1.646064825 |
| P(T≤t) two-tail | 0.001026062 |
| t Critical two-tail | 1.961850017 |

---

## Decision Rule

Since this is a **one-tailed test** (testing whether Treatment > Control):

- If **p one-tail < α (0.05)** → Reject H0
- **0.000513 < 0.05 → Reject H0**

> **Note on negative t-statistic:** The t-stat is −3.291 because Excel placed Control (lower mean) in the first column and Treatment (higher mean) in the second. The absolute value |t| = 3.291 exceeds the one-tail critical value of 1.646, confirming the result is significant in the correct direction — Treatment outperforms Control.

---

## P-Value Evidence

| Test | P-Value | Alpha (α) | Decision |
|---|---|---|---|
| One-tail | 0.000513 | 0.05 | **Reject H0 — Significant** |
| Two-tail | 0.001026 | 0.05 | **Reject H0 — Significant** |

The probability of observing this difference by chance is **0.051%** — far below the 5% threshold.

---

## Interpretation Logic

The Treatment group converted at **7.04%** versus **3.19%** for Control — a **+3.85 percentage point** lift, representing a **+120.8% relative improvement** in paid conversion rate.

With p = 0.000513 (one-tail), this result is statistically significant at the 95% confidence level. The improvement is highly unlikely to be due to random variation.

The t-statistic of −3.291 (absolute value 3.291) is well beyond the critical threshold of 1.646 for a one-tailed test at α = 0.05, providing strong evidence to reject the null hypothesis.

---

## Business Interpretation

The new campaign (Treatment) demonstrably improves paid conversion. However, statistical significance alone does not justify a full launch. The following guardrail concerns must also be addressed:

| Guardrail Metric | Control | Treatment | Risk |
|---|---|---|---|
| Support Ticket Rate | 14.78% | 24.79% | HIGH — significant increase |
| Avg Revenue per Converted User (ARPC) | $1,630 | $770 | HIGH — 53% decline |
| Refund Rate | 0.00% | 0.42% | LOW — not yet significant |
| Engagement Score | 57.03 | 62.94 | POSITIVE — Treatment higher |

---

## Summary Decision

| | |
|---|---|
| **Statistical Decision** | Reject H0 — Treatment conversion rate is significantly higher than Control (p = 0.000513) |
| **Business Recommendation** | Selective launch (North Region only) pending investigation of support ticket rate increase and ARPC decline before full rollout |
