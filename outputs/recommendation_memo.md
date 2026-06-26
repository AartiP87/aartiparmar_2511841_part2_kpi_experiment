Task 1: Business Problem Statement

Problem Statement:
The company introduced a new onboarding and activation campaign to increase the number of users converting into paid subscribers.

1. The decision that needs to be made is:
* Should the new onboarding experience (Treatment) be launched to all users?

2. Stakeholders impacted
* Product Team
* Marketing Team
* Revenue Team
* Customer Success Team
* Company Leadership

3. Desired improvement
Increase in:
Paid conversion rate
User engagement
Revenue generation

4. Risks to monitor
* Higher refund requests
* More support tickets
* Lower revenue quality
* Negative impact on certain user segments

5. Evidence required
The company needs statistical evidence that:
* Paid conversion improves significantly.
* Guardrail metrics do not deteriorate excessively.
* The improvement is sustainable across important customer segments.

## Task 9 ##

## Subscription Campaign A/B Experiment — Full Analysis
**Date:** June 2026
**Prepared by:** Experiment Analysis Team
**Decision Required:** Launch / Do Not Launch / Partial Launch / Continue Testing

---

## Executive Summary

The new onboarding and activation campaign (Treatment) delivered a statistically significant improvement in paid conversion rate — more than doubling it relative to Control (+120.8% relative lift, p = 0.000513). Engagement scores also improved significantly. However, two critical guardrail metrics — support ticket rate (+10pp) and average revenue per converted user (ARPC, −53%) — show material deterioration in the Treatment group. A full unconditional launch is not recommended at this stage.

**Final Recommendation: Selective Launch — North Region Only**, while investigating onboarding friction and revenue quality before broader rollout.

---

## North Star Metric

**Paid Conversion Rate** — the proportion of users who become paying customers within 30 days of signup.

Selected because it is the clearest and most direct measure of business value. All funnel metrics (landing page visits, trial starts, onboarding completions) are intermediate steps; paid conversion is the ultimate downstream outcome that drives revenue, retention, and long-term growth.

---

## KPI Tree Summary

The KPI tree breaks Paid Conversion Rate into three primary drivers:

**1. Acquisition Quality**
- Landing Page Visit Rate
- Traffic Source Mix
- Plan Type Distribution
- Device Type Reach

**2. Activation & Onboarding**
- Trial Start Rate
- Onboarding Completion Rate
- Engagement Score
- Days to Convert

**3. Revenue Quality**
- Average Revenue Per Converted User (ARPC)
- Average Revenue Per User (ARPU)
- Refund Rate
- Revenue by Segment

**Guardrail Metrics monitored:** Refund Rate, Support Ticket Rate, Engagement Score Quality, ARPC

---

## Dataset Overview

| Item | Detail |
|---|---|
| Raw records | 1,408 |
| After deduplication | 1,400 |
| Control group | 690 users |
| Treatment group | 710 users |
| Duplicates removed | 8 (kept first occurrence) |
| Missing: device_type | 18 records (retained) |
| Missing: traffic_source | 24 records (retained) |
| Missing: engagement_score | 14 records (excluded from averages) |
| Revenue outliers | 3 high-value Control users (retained) |

---

## Experiment Result Summary

| Metric | Control | Treatment | Delta | Significant? |
|---|---|---|---|---|
| User Count | 690 | 710 | +20 | N/A |
| Landing Page Visit Rate | 63.62% | 72.39% | +8.77pp | — |
| Trial Start Rate | 25.07% | 29.01% | +3.94pp | — |
| Onboarding Completion Rate | 15.65% | 21.13% | +5.48pp | — |
| **Paid Conversion Rate** | **3.19%** | **7.04%** | **+3.85pp** | **YES (p = 0.000513)** |
| ARPU | $51.97 | $54.25 | +$2.28 | No (p = 0.910) |
| ARPC | $1,630 | $770 | −$860 | Material concern |
| Refund Rate | 0.00% | 0.42% | +0.42pp | No (p = 0.258) |
| Support Ticket Rate | 14.78% | 24.79% | +10.01pp | YES — Risk |
| Avg Engagement Score | 57.03 | 62.94 | +5.91 | YES (p < 0.001) |
| Avg Days to Convert | 8.9 days | 6.4 days | −2.5 days | — |

---

## Hypothesis Test Summary

| Item | Detail |
|---|---|
| **Test** | t-Test: Two-Sample Assuming Unequal Variances (Welch's t-Test) |
| **Tool** | Excel Data Analysis ToolPak |
| **H0** | μ_Control = μ_Treatment (no difference in conversion rate) |
| **H1** | μ_Treatment > μ_Control (Treatment improves conversion) |
| **Test Direction** | One-tailed (right-tailed) |
| **Alpha (α)** | 0.05 |
| **t Statistic** | −3.2910 (|t| = 3.291) |
| **Degrees of Freedom** | 1,259 |
| **p one-tail** | 0.000513 |
| **t Critical one-tail** | 1.6461 |
| **Decision** | Reject H0 — statistically significant |

The Treatment group converted at 7.04% vs 3.19% for Control — a +3.85pp improvement with only a 0.05% probability of occurring by chance. The result is robust and statistically significant.

---

## Guardrail Metric Analysis

### 1. Support Ticket Rate — HIGH RISK

| | Control | Treatment |
|---|---|---|
| Support Ticket Rate | 14.78% | 24.79% |
| Delta | | +10.01pp |
| Significance | | YES (p < 0.001) |

Treatment users raised support tickets at nearly **1.7× the rate** of Control. This is statistically significant and practically meaningful. At scale, this would substantially increase customer support costs, degrade customer experience, and may indicate unresolved onboarding friction or unmet product expectations introduced by the new campaign. This is the most operationally dangerous guardrail finding.

**Risk verdict: Do not scale until root cause is identified and resolved.**

---

### 2. Average Revenue Per Converted User (ARPC) — HIGH RISK

| | Control | Treatment |
|---|---|---|
| Converted Users | 22 | 50 |
| Total Revenue | ~$35,860 | ~$38,520 |
| ARPC | $1,630 | $770 |
| Delta | | −$860 (−53%) |

While Treatment generates modestly more total revenue ($38,520 vs $35,860), the per-user revenue is 53% lower. This means the campaign is converting more users but at a substantially lower value per conversion. Potential causes include: lower plan tier selections, shorter initial commitments, or the campaign reaching less purchase-ready customer segments.

At scale, if ARPC remains at $770 vs Control's $1,630, the long-term revenue trajectory could be significantly worse despite higher conversion counts. For example, at 10,000 users per group: Treatment generates ~$770 × 704 converters = $542,080 vs Control's ~$1,630 × 319 converters = $520,000 — only marginally better, and this gap narrows or reverses as acquisition costs rise.

**Risk verdict: Investigate plan tier mix and revenue composition before full rollout.**

---

### 3. Refund Rate — LOW RISK (Monitor)

| | Control | Treatment |
|---|---|---|
| Refund Rate | 0.00% | 0.42% |
| p-value | | 0.258 (not significant) |

Not statistically significant at current sample sizes, but Control had zero refunds while Treatment had some. This directional signal is worth monitoring at larger scale. Could indicate marginal customer fit issues in the Treatment group.

**Risk verdict: Monitor — not a blocker at this stage.**

---

### 4. Engagement Score — POSITIVE GUARDRAIL

| | Control | Treatment |
|---|---|---|
| Avg Engagement Score | 57.03 | 62.94 |
| Delta | | +5.91 (p < 0.001) |

Treatment users show significantly higher engagement scores. This is a strong positive signal suggesting the new campaign attracts or activates more engaged users — a protective factor against early churn and a positive leading indicator for retention.

**Risk verdict: No concern — this guardrail is favourable.**

---

## Segment-Level Insights

### By Region

| Region | Control Conv% | Treatment Conv% | Lift |
|---|---|---|---|
| North | 3.48% | 8.89% | +5.41pp (best) |
| South | 3.26% | 7.65% | +4.39pp |
| East | 2.55% | 6.47% | +3.92pp |
| West | 3.38% | 5.08% | +1.70pp (weakest) |

North Region shows the strongest absolute lift and is the recommended launch target.

### By Device Type

| Device | Control Conv% | Treatment Conv% | Lift |
|---|---|---|---|
| Desktop | 4.50% | 6.57% | +2.07pp |
| Mobile | 2.58% | 7.41% | +4.83pp |
| Tablet | 1.82% | 7.14% | +5.32pp |

Mobile and Tablet show strong treatment improvement. Treatment performs consistently across all device types.

### By Traffic Source

| Traffic Source | Control Conv% | Treatment Conv% | Lift |
|---|---|---|---|
| Referral | 2.47% | 10.99% | +8.52pp (best) |
| Paid Search | 1.29% | 6.25% | +4.96pp |
| Email | 2.74% | 7.14% | +4.40pp |
| Organic | 2.03% | 6.33% | +4.30pp |
| Social | 7.75% | 6.06% | −1.69pp (reversal) |

Referral traffic delivers the highest Treatment conversion rate at 10.99%. Notably, Social traffic showed a **reversal** — Control outperformed Treatment (7.75% vs 6.06%) — suggesting the new campaign may underperform for Social-sourced users. This warrants further investigation.

---

## Final Recommendation

### LAUNCH — North Region Only (Selective Launch)

**Rationale:**

1. **Statistical evidence is strong** — conversion rate improvement is real (p = 0.000513), not chance
2. **North Region is the safest launch target** — highest conversion lift (+5.41pp), and ARPU remains competitive ($81 Treatment vs $85 Control)
3. **Selective launch limits operational risk** — caps support ticket cost increase while generating revenue-positive outcomes
4. **Creates a larger, cleaner dataset** to investigate ARPC and support ticket concerns before full rollout
5. **Engagement score improvement** is a positive retention signal that supports launch confidence

**Conditions required before broader rollout:**

- Identify and resolve the root cause of the +10pp support ticket rate increase (specific onboarding steps causing confusion or unmet expectations)
- Analyse plan tier mix of Treatment converters vs Control to understand the ARPC gap
- Confirm whether Social traffic reversal is statistically meaningful or a sample size artefact
- Monitor 60-day and 90-day retention of North Region Treatment converters to validate LTV trajectory
- If ARPC gap narrows and support ticket rate is brought below 18%, proceed to full launch

---

## Risks and Limitations

1. **ARPC decline at scale** — If Treatment attracts structurally lower-value customers, total revenue impact could be neutral or negative despite higher conversion counts
2. **Support cost burden** — A +10pp support ticket rate is significant at scale and must be resolved before broad rollout
3. **Small conversion base** — Only 22 (Control) and 50 (Treatment) conversions; larger sample would increase confidence in ARPC and refund estimates
4. **High-value Control outliers** — Three users generated $3,888–$8,611 in revenue, inflating Control ARPC; even removing them, the ARPC gap remains significant
5. **Social traffic reversal** — Treatment underperforms Control for Social-sourced users; could affect results if Social is a primary acquisition channel
6. **Missing data** — 8 duplicate user IDs removed, 18 missing device types, 24 missing traffic sources may introduce mild segment-level bias
7. **Experiment duration unknown** — Cannot assess novelty effects, seasonality, or learning curves without knowing the experiment window and dates

---

## Next Steps

| Priority | Action | Owner | Timeline |
|---|---|---|---|
| 1 | Selective launch to North Region | Product / Engineering | Immediate |
| 2 | Qualitative research on support ticket drivers | Customer Success | 2 weeks |
| 3 | Analyse plan tier distribution by group | Data / Finance | 1 week |
| 4 | Set up 60-day monitoring dashboard (conversion, ARPC, ticket rate, retention) | Analytics | 1 week |
| 5 | Investigate Social traffic reversal | Growth / Marketing | 2 weeks |
| 6 | Re-run experiment with onboarding fixes; target n ≥ 2,000 per group | Product | 4–6 weeks |
| 7 | Full launch decision based on guardrail resolution | Leadership | 6–8 weeks |

---

## Appendix — Key Metrics Reference

| Metric | Control | Treatment |
|---|---|---|
| Users | 690 | 710 |
| Paid Conversions | 22 | 50 |
| Conversion Rate | 3.19% | 7.04% |
| Total Revenue 30d | ~$35,860 | ~$38,520 |
| ARPU | $51.97 | $54.25 |
| ARPC | $1,630 | $770 |
| Refund Rate | 0.00% | 0.42% |
| Support Ticket Rate | 14.78% | 24.79% |
| Avg Engagement Score | 57.03 | 62.94 |
| Avg Days to Convert | 8.9 | 6.4 |
| t Statistic | −3.2910 | |
| p-value (one-tail) | 0.000513 | |
| Statistical Decision | Reject H0 | |
