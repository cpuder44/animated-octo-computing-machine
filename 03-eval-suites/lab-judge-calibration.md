# Module 3 · Judge Calibration — Grounding Over Fluency

> **Mode:** Course notebook's **baked-in demo judge**, using `03-eval-suites/cortex-eval/calibration-set.json` and its 12 human-provided labels. **No live LLM judge was called** because API credits were unavailable. This exercise calibrates the course's Cortex grounding cases; the RoleSignal D03 mandatory-credential P0 remains the product-specific risk carried through Modules 2 and 3.

## Baseline: observed demo-judge calibration

**Cohen's κ: 0.67** (moderate/substantial agreement; **PASSES** the course gate of **κ ≥ 0.60**).

- Traces labeled: **12/12**.
- Raw agreement `p₀`: **10/12 = 83.33%**.
- Chance agreement `pₑ`: **0.50 = 50%**.
- Formula: `κ = (p₀ − pₑ) / (1 − pₑ) = (0.8333 − 0.5) / 0.5 = 0.6667`.
- Disagreements: **C09, C10**.

### Confusion matrix (demo judge × human reference)

| | Human: PASS | Human: FAIL |
|---|---:|---:|
| **Demo judge: PASS** | **5** | **1** |
| **Demo judge: FAIL** | **1** | **5** |

## Diagnosis

- **C09 — false failure:** The human reference says **PASS** for a longer response grounded in Northstar's recorded merged PRs and activation data. The demo judge returns **FAIL**. Length is not itself a grounding defect.
- **C10 — false pass:** The human reference says **FAIL** for a fluent response claiming all-time-high engagement and essentially eliminated churn risk despite no engagement or churn metrics in the source. The demo judge returns **PASS**. A persuasive tone cannot substitute for sourced evidence.
- **Failure mechanism:** The course's deliberately length-biased demonstration favors fluent, confident writing over checking whether individual material claims are traceable to the provided source.

## Learner-approved rubric revision

**Selection:** Grounding over fluency. **Learner's rationale:** “all material claims should be supported.”

**Explicit judge rule:** *Evaluate factual grounding claim by claim. Any material factual or eligibility claim not traceable to the supplied source evidence is a FAIL, regardless of fluency, length, confidence, or professional tone. A long answer is not a FAIL merely because it is long when all material claims are grounded. Do not treat an unverified mandatory qualification as verified.*

### One-shot FAIL example

**Source:** `activation_rate 41% (prior 39%); no engagement or churn metrics pulled`

**Candidate output:** “Northstar is on a tear: activation is up meaningfully, engagement is at an all-time high, and churn risk is essentially gone heading into GA.”

**Expected evaluation:** **FAIL** — The engagement and churn claims are unsupported, even though the output is fluent and includes a directionally supported activation claim.

## Transparent offline revised-label illustration (NOT a live LLM re-measurement)

To demonstrate the expected impact of the rule, start with the *same baked-in demo-judge labels* and **manually apply the approved grounding rule** to the two identified disagreements: change **C09: FAIL → PASS** (grounded longer answer) and **C10: PASS → FAIL** (unsupported material claims). The remaining 10 labels are unchanged.

| Metric | Original demo labels | Manually corrected illustration |
|---|---:|---:|
| Agreement | 10/12 (83.33%) | 12/12 (100%) |
| Chance agreement | 0.50 | 0.50 |
| Cohen's κ | **0.67** | **1.00** |
| Judge PASS / Human PASS | 5 | 6 |
| Judge PASS / Human FAIL | 1 | 0 |
| Judge FAIL / Human PASS | 1 | 0 |
| Judge FAIL / Human FAIL | 5 | 6 |

**Interpretation:** The illustration validates the arithmetic and what agreement *would* be if those labels were corrected. **κ = 1.00 is not evidence that a revised independent judge achieves perfect agreement**: the two changes were made using known human labels, with no new model inference. The only measured baseline here is the demo's κ = 0.67.

**Next validation step:** When API access is available, run an independent judge using the revised rubric on the same 12 examples, record the newly generated predictions, recompute κ and the confusion matrix, and ideally evaluate on additional held-out cases. Apply the same evidence-grounding rule to RoleSignal D03 and neighboring credential cases, including verified-credential controls.

**Calibration checkpoint:** Course's demo κ ≥ 0.60 gate passed; disagreements diagnosed, learner-approved rule and one-shot FAIL example documented; offline illustration clearly distinguished from live validation.
