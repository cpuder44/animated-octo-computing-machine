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

### Hallucination — ⚠️ Partial
- **Method:** Evaluate RoleSignal fit recommendations against candidate-profile evidence and target-job requirements. For the Module 2 manual audit, compare each prediction with its human-approved reference judgment; flag material claims lacking support, missing qualifications presented as verified, and unsupported **STRONG MATCH** conclusions (including D03's unverified mandatory credential). The newer scenario runner reports eight passing scenarios, including a missing-hard-requirement calibration case, but its exact assertions have not been inspected; therefore this is **partial demonstrated coverage**, not proof of comprehensive automated hallucination testing.
- **Ground truth:** The **human-approved Module 2 RoleSignal reference judgments** in `02-failure-discovery/rolesignal-references.md`, evaluated alongside the actual **candidate-profile evidence and job requirements** in the Module 1 evaluation dataset (`01-evaluation-strategy/eval-harness-proof.md`). The original predictions and human-reviewed audit support traceability; they do not independently verify any candidate credential that is not explicitly supplied.

### Latency — ⚠️ Partial
- **Method:** Use the scenario runner's recorded end-to-end execution durations as the **current observed baseline**; compare durations across scenario types and, as repeated runs become available, track distributions and changes over time. The supplied screenshot shows one run for each of eight scenarios: **6.6s, 8.4s, 6.8s, 6.7s, 8.5s, 10.9s, 16.9s, 16.8s**. A timing record is **not** evidence that a latency acceptance gate exists.
- **Ground truth:** The scenario runner's **recorded elapsed-time values** displayed in the learner-supplied **November 6, 2026** results screenshot. **No approved latency performance threshold or stable p95 baseline has been established**; these eight heterogeneous one-off timings are observations, not a validated service-level objective.

**Learner decision:** Hallucination is grounded in the human-approved Module 2 references plus candidate/job evidence. Latency uses recorded execution durations without an approved threshold. Learner rationale: “because they make sense.”

## Strategic acceptance

**Accepted gap:** **Toxicity — ❌**, temporarily accepted as an **uncovered evaluation risk**, not represented as a passing control.

**Why acceptable for now:** The current RoleSignal scenario suite includes generated outreach and cover-letter cases, but the screenshot does **not** establish dedicated harmful-language assertions. Product has chosen a temporary, explicitly monitored acceptance while prioritizing fairness evaluation. This decision does not establish that toxicity incidents are unlikely or that existing writing tests provide toxicity protection.

**Kill criterion (learner-approved):** **Any confirmed severe harmful-language output, or two substantiated harmful-language incidents within any rolling 30-day period**, ends the acceptance and triggers immediate Product/Engineering review and a decision to pause or restrict the affected generation flow pending mitigation.

**Interim oversight (proposed implementation):** Provide an in-product or support reporting path, preserve user-submitted examples for authorized review with appropriate data minimization, and maintain a dated incident register so the above trigger is observable. This process is **not yet evidenced as deployed**.

## Critical mitigation

- **Critical gap:** **Bias / Fairness — ❌**
- **Why critical (learner rationale):** “RoleSignal's central promise is to identify overlooked opportunities. Systematic unfairness would directly undermine that promise.”
- **Accountable owners:** **Product owner and Engineering** (learner-selected).
- **Deadline:** **December 15, 2026** (learner-selected).
- **Mitigation plan (proposed, to complete by deadline):**
  1. **Define the fairness contract (Product):** Specify legitimate fit factors (documented skills, qualifications, role requirements, user constraints) and which irrelevant or protected/proxy attributes must **not** change fit outcomes absent a job-relevant explanation. Require expert review of any contested criteria.
  2. **Build paired counterfactual cases (Product + Engineering):** Create a labeled baseline of at least **30 candidate/job pairs** as a **proposed initial scope**, keeping qualifications and job requirements constant while varying only irrelevant signals, such as name cues or non-job-relevant background descriptors. Include conventional and nontraditional career histories to assess the product's transferable-skill promise. Avoid treating unequal outcomes as automatically discriminatory when a relevant variable differs.
  3. **Run repeatable checks (Engineering):** For each matched pair, compare recommendation class (STRONG MATCH / EXPLORATORY / WEAK MATCH), fit-score movement if applicable, and explanation grounding. Flag unexplained class changes or material score differences for human adjudication. Record the exact inputs, model/prompt version, outputs, adjudications, and pass/fail criteria.
  4. **Triage and correct (Product + Engineering):** Review flagged differences, distinguish genuine unfairness from legitimate evidence-based distinctions, correct prompts/rubrics or matching logic, and rerun the paired set. Add confirmed failures as regression fixtures and report residual gaps.
  5. **Deliverable by December 15, 2026:** A versioned fairness test set, written evaluation rubric, first baseline results with denominators and adjudicated disparities, remediation owners, and a proposed recurring regression schedule. Do not mark Bias as covered until those artifacts and checks exist.

**Measurement caution:** The 30-pair initial scope is a recommended test-design proposal, **not** a learner-confirmed numerical acceptance threshold or evidence of an existing fairness suite. Counterfactual consistency is a useful first test but is not a complete fairness assessment.

**Remaining gap:** **Drift Monitoring — ❌** remains uncovered and explicitly visible for the Module 5 budget allocation decision. No acceptance or mitigation commitment for drift was made in this step.
