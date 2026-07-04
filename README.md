# E-Commerce Landing Page A/B Test
## Conversion Analysis & Business Recommendation

**Tools:** Python · pandas · numpy · scipy · statsmodels · matplotlib  
**Techniques:** Two-proportion z-test · Power analysis · Cohen's h · Mann-Whitney U · Behavioural segmentation

---

## Result

The new landing page drove a statistically significant **+8.67 percentage point** conversion lift (5.40% → 14.07%), confirmed across all devices and regions.

| Metric | Value |
|--------|-------|
| Z-statistic | 10.35 |
| P-value | < 0.001 |
| Absolute lift | +8.67pp |
| 95% Confidence interval | [7.04pp – 10.30pp] |
| Relative lift | +160.5% |
| Cohen's h | 0.30 (medium effect) |
| Sample per group | 2,481 (14x the minimum required) |

**Decision: Ship the new page. Full rollout to all traffic.**

---

## Business Question

Did the new landing page design increase conversion rate enough to justify rollout, and is the result statistically trustworthy or just noise?

---

## Dataset

Synthetic UK retail website dataset — 5,000 users, 7 columns.

| Column | Description | Values |
|--------|-------------|--------|
| user_id | Unique user identifier | 10,000–20,000 |
| group | Experiment assignment | A (control) / B (treatment) |
| page_views | Pages viewed in session | 1–14 |
| time_spent | Seconds on site | 40–449 |
| conversion | Did the user convert? | Yes / No |
| device | Device type | Desktop / Mobile |
| location | UK region | England / Scotland / Wales / Northern Ireland |

---

## Repository Structure
