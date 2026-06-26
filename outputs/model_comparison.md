# Model Comparison Report

## Overview

Three OLS regression models were estimated on a cleaned dataset of 306 store-month observations. The dependent variable in all models is `monthly_sales`.

---

## Model Summary Table

| Item | M1: Footfall | M2: Marketing Spend | M3: Multiple Regression |
|---|---|---|---|
| **Model Name** | Simple — Footfall | Simple — Marketing Spend | Multiple OLS w/ Dummies |
| **Dep. Variable** | monthly_sales | monthly_sales | monthly_sales |
| **Ind. Variables** | footfall | marketing_spend | footfall, marketing_spend, inventory_pct, holiday_flag, store_type dummies, region dummies |
| **N Observations** | 306 | 306 | 306 |
| **R-squared** | 0.7348 | 0.1574 | **0.8268** |
| **Adj. R-squared** | 0.7340 | 0.1547 | **0.8203** |
| **Significant Vars** | footfall *** | marketing_spend *** | footfall ***, marketing_spend ***, inventory_pct ***, holiday_flag *, store_Airport ***, store_Mall ***, store_High Street *, region_South **, region_West *** |
| **Non-significant** | — | — | avg_discount_pct, region_North |
| **Business Usefulness** | HIGH | MODERATE | HIGHEST |
| **Primary Limitation** | Ignores all other drivers | Very low R²; not causal | More complex to communicate; some multicollinearity possible |

---

## Model-by-Model Analysis

### M1: Simple Regression — Footfall

**Equation:** `monthly_sales = 447,699 + 35.64 × footfall`

**R² = 0.7348** — Footfall alone explains nearly 74% of the variation in monthly sales. This is a remarkably strong single-variable model. The coefficient of 35.64 implies that every additional monthly visitor adds approximately $35.64 to sales.

**Business Usefulness:** Very high. Footfall is directly actionable — store managers can use this to set footfall targets linked to sales goals. The model is easy to explain to non-technical stakeholders.

**Limitation:** It ignores store type, marketing investment, region effects, and seasonal factors (holidays). Using only footfall may lead to misattribution of sales changes.

---

### M2: Simple Regression — Marketing Spend

**Equation:** `monthly_sales = 567,464 + 2.05 × marketing_spend`

**R² = 0.1574** — Marketing spend alone explains only 15.7% of variance. While the coefficient is statistically significant (p < 0.001), the low R² suggests marketing is not the primary driver of sales. The coefficient of 2.05 implies $2.05 in sales per $1 of marketing spend (a marginal ROI).

**Business Usefulness:** Moderate. Useful to confirm that marketing has some positive relationship with sales, but the model should not be relied upon for planning. The relationship may be confounded (e.g., high-traffic stores also get more marketing budget).

**Limitation:** Likely suffers from omitted variable bias. Stores with more marketing spend may also have other advantages (location, store type) that actually drive sales.

---

### M3: Multiple Regression — Full Model

**Equation:**
```
monthly_sales = 127,238
              + 33.50 × footfall
              + 1.18  × marketing_spend
              + 2,742 × inventory_availability_pct
              + 14,176 × holiday_flag
              + 36,317 × store_Airport
              + 26,347 × store_Mall
              + 14,750 × store_High Street
              + 21,906 × region_South
              + 22,473 × region_West
              [+ non-significant terms]
```

**R² = 0.8268** — The multiple model explains 82.7% of variation in monthly sales. This is a substantial improvement over both simple models.

**Business Usefulness:** Highest. This model reveals the independent contribution of each driver:
- **Footfall** remains the dominant driver even after controlling for other variables
- **Inventory availability** matters significantly — stores with better stock drive more revenue
- **Store type** has a strong structural effect — Airport stores generate $36K more per month than comparable Residential stores, all else equal
- **Region** matters — West and South outperform East
- **Holiday periods** provide a ~$14K lift
- **Discounting** (avg_discount_pct) is NOT a significant predictor — suggesting discounts do not reliably generate enough volume to boost total sales

**Limitation:** The model is more complex and has 12 predictors. Some multicollinearity may exist between footfall and store_type. The model also does not account for temporal trends, store age, or competitor quality.

---

## Recommendation

**Use Model M3 (Multiple Regression) for business decisions.** It provides the best fit and the most nuanced understanding of what drives monthly sales. Model M1 (Footfall) is a useful, communicable tool for operational target-setting. Model M2 (Marketing) should not be used in isolation.

**Priority actions based on M3:**
1. Invest in footfall-generating activities (top driver)
2. Improve inventory availability — each percentage point adds ~$2,742/month
3. Prioritise Airport and Mall expansion over Residential formats
4. Plan for holiday-period uplifts (~$14K boost)
5. Re-evaluate discounting strategy — it does not significantly drive total monthly revenue
