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

---

## Analysis

### 1. Sanity Checks

Before running any statistics, the experiment was validated for structural integrity.

| Check | Result | Status |
|-------|--------|--------|
| Group split | 50.38% A / 49.62% B | ✅ Pass |
| Duplicate users | 0 | ✅ Pass |
| Device balance | Within 3pp across groups | ✅ Pass |
| Location balance | All regions 24–26% in both groups | ✅ Pass |

### 2. Power Analysis

The experiment needed 175 users per group to detect the observed effect at 80% power. With 2,481 per group, it was adequately powered — the result is unambiguous.

| Metric | Value |
|--------|-------|
| Alpha | 0.05 |
| Target power | 80% |
| Cohen's h | 0.30 (medium) |
| Minimum sample needed | 175 per group |
| Actual sample | 2,481 per group |

### 3. Statistical Test

A two-proportion z-test was applied — the correct test for binary conversion outcomes between two independent groups. Two-sided to account for the possibility the new page could also underperform.

![Conversion Rate Results](images/ab_test_results.png)

### 4. Segmentation

The lift holds across every sub-group tested. No segment underperforms.

![Segmentation Analysis](images/ab_test_segmentation.png)

| Segment | Control | Treatment | Lift | Significant |
|---------|---------|-----------|------|-------------|
| Desktop | 5.87% | 13.91% | +8.04pp | ✅ p < 0.001 |
| Mobile | 4.94% | 14.24% | +9.30pp | ✅ p < 0.001 |
| England | 6.93% | 14.69% | +7.76pp | ✅ p < 0.001 |
| Northern Ireland | 5.05% | 11.46% | +6.42pp | ✅ p < 0.001 |
| Scotland | 4.93% | 15.06% | +10.13pp | ✅ p < 0.001 |
| Wales | 4.77% | 15.12% | +10.35pp | ✅ p < 0.001 |

### 5. Behavioural Deep-Dive

Four analyses were run beyond conversion rate to understand *why* the new page won.

---

#### Analysis 1 — Do converters behave differently from non-converters?

![Behavioural Profile](images/ab_test_behavioural_profile.png)

| Cohort | n | Avg time spent | Avg page views |
|--------|---|---------------|----------------|
| A — Did not convert | 2,383 | 241.5s | 7.61 |
| A — Converted | 136 | 245.4s | 7.17 |
| B — Did not convert | 2,132 | 243.4s | 7.51 |
| B — Converted | 349 | 242.4s | 7.37 |

No significant difference in time spent or page views between converters and non-converters in either group (all p > 0.20). Conversion is independent of engagement depth.

---

#### Analysis 2 — Did the new page make users faster to convert?

![Engagement Efficiency](images/ab_test_efficiency.png)

Converters on both pages spent identical time on site (242s vs 245s, p = 0.80) and viewed the same number of pages (7.37 vs 7.17, p = 0.62), confirmed by Mann-Whitney U. The new page converted more people — not a different type of person.

---

#### Analysis 3 — Does conversion probability change with engagement level?

![Engagement Threshold](images/ab_test_engagement_threshold.png)

| Time bin | Control rate | Treatment rate | Lift |
|----------|-------------|----------------|------|
| 0–50s | 1.59% | 11.27% | +9.68pp |
| 101–150s | 6.19% | 14.98% | +8.79pp |
| 201–250s | 4.41% | 15.11% | +10.70pp |
| 351–400s | 5.75% | 11.62% | +5.87pp |
| 401–450s | 5.97% | 14.13% | +8.16pp |

The control page converts at a flat 4–6% regardless of time spent. The treatment page starts at 11% even for users who spent under 50 seconds and stays elevated throughout.

---

#### Analysis 4 — Did the new page damage experience for non-converters?

![Engagement Quality](images/ab_test_engagement_quality.png)

Non-converters on the new page spent 243s vs 242s on the old page (p = 0.59). No degradation in engagement quality — the win is clean with no hidden cost to non-converting users.

---

## Key Finding

The new page changed **who converts**, not **how anyone behaves**. All four behavioural analyses point to the same conclusion: a specific page element — most likely the CTA, offer framing, or trust signals — is triggering purchase decisions independently of engagement depth.

**The implication for product:** run a follow-up element-level test to isolate and amplify the exact driver.

---

## Business Recommendation

| Dimension | Finding | Verdict |
|-----------|---------|---------|
| Statistical significance | p < 0.001, z = 10.35 | ✅ Significant |
| Effect size | Cohen's h = 0.30 | ✅ Meaningful |
| Confidence interval | [7.04pp – 10.30pp], all positive | ✅ Precise |
| Experiment validity | All 4 sanity checks passed | ✅ Trustworthy |
| Statistical power | 2,481 per group vs 175 needed | ✅ Robust |
| Device consistency | +8.04pp desktop, +9.30pp mobile | ✅ Universal |
| Location consistency | All 4 regions significant | ✅ Universal |
| Non-converter impact | No degradation (p = 0.59) | ✅ No hidden cost |

**Ship the new page. Monitor conversion rate and revenue weekly for 4 weeks post-rollout. Run a follow-up element-level test on the CTA and offer block.**

---

## Caveats

- **Synthetic dataset:** The 160% relative lift is unrealistic for production e-commerce (typical wins are 2–15% relative). The methodology is valid; the magnitude should not be taken at face value.
- **No revenue data:** Conversion rate improvement is confirmed but average order value is unknown. Post-rollout revenue monitoring is essential.
- **Unknown experiment duration:** If the test ran for less than two full business cycles, novelty effect cannot be ruled out.

---

## How to Run

```bash
git clone https://github.com/biancakhambatta/ecommerce-ab-test-analysis
cd ecommerce-ab-test-analysis
pip install pandas numpy scipy statsmodels matplotlib seaborn
jupyter notebook ab-test-analysis.ipynb
```
