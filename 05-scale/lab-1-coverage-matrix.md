# Lab 1, Ascend Analytics Coverage Matrix

> Repo file `ai-evals/05-scale/lab-1-coverage-matrix.md`. Feeds the **Coverage / scale** slide of the final pitch deck (Module 6).
>
> Fill this with the **Coverage Matrix Tool**, then **Copy markdown** and paste it over this file. The headings below mirror the tool's output exactly. **Force ≥2 ❌ gaps** — an all-green matrix isn't real.

**Product:** RoleSignal

## Coverage row

| Product | Hallucination | Bias | Latency | Toxicity | Drift Monitoring |
|---|---|---|---|---|---|
| **RoleSignal** | ⚠️ Partial | ❌ Gap | ⚠️ Partial | ❌ Gap | ❌ Gap |

### Coverage rationale (Step 1 only)

- **Hallucination — ⚠️ Partial:** Screenshot of a RoleSignal scenario run dated **November 6, 2026**, using `google/gemini-3.7-flash`, shows **8/8 scenarios reporting “All passed”**: Fraud Risk Strategist fit score; Hiring manager outreach note; Referral message keeps the link; Cover letter opening paragraph; Career bridge pitch; Calibration A (strong evidence, strong fit); Calibration B (sparse posting lowers confidence); Calibration C (missing hard requirement). This demonstrates scenario-level testing relevant to evidence-grounded outputs, but **the screenshot does not reveal the exact assertions**, and the previous manual D03 failure shows why broad hallucination protection cannot yet be claimed.
- **Bias — ❌ Gap:** Neither the eight scenario titles/results nor the documented Module 1–4 work establishes subgroup fairness tests or bias evaluation coverage.
- **Latency — ⚠️ Partial:** The eight scenario results display individual execution durations (**6.6s, 8.4s, 6.8s, 6.7s, 8.5s, 10.9s, 16.9s, 16.8s**). Timing is observed, but **no formal latency thresholds, percentiles, or pass/fail assertions for latency** are visible.
- **Toxicity — ❌ Gap:** Outreach and cover-letter scenarios are present, but their reported passes do **not** establish explicit toxicity or harmful-language checks.
- **Drift Monitoring — ❌ Gap:** The screenshot captures one dated scenario run; it does **not** demonstrate longitudinal model-quality drift monitoring, distribution shift alerts, or recurring trend comparisons.

**Evidence boundary:** Screenshot supplied by the learner shows **eight passing scenarios**, not the underlying prompts, graders, or full historical test coverage. These are learner-confirmed **current coverage ratings**, not a claim that all proposed Module 3/4 release gates have been deployed. **Three ❌ gaps** are explicitly acknowledged, satisfying the Module 5 minimum of two.

## Method + Ground Truth (two ✅/⚠️ cells)

### _Risk name 1_
- **Method:** _how you evaluate it_
- **Ground truth:** _what you grade against_

### _Risk name 2_
- **Method:** _how you evaluate it_
- **Ground truth:** _what you grade against_

## Strategic acceptance

**Accepted gap:** _which ❌ you're accepting_

> _Why it's an acceptable risk right now + the kill criterion / date that would change the call._

## Critical mitigation

- **Critical gap:** _the ❌ you cannot accept_
- **Why critical:** _…_
- **Mitigation plan:** _concrete plan with a date/owner — not "we'll add it later"._
