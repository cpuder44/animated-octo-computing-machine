# Ship/Hold Memo · RoleSignal

> Repo file `ai-evals/06-culture/lab-1-ship-hold-memo.md`. A Pyramid-Principle executive memo: the recommendation comes **first**.
>
> Module 6 capstone for RoleSignal. Step 1 records the learner's launch decision; evidence and business-risk analysis remain for later steps.

> **Decision:** 🛑 **HOLD** the next broad release of RoleSignal matching changes

**To:** Product Leadership · **cc:** Engineering Lead; Trust & Safety
**From:** RoleSignal Product Owner · November 10, 2026

## The Answer

**HOLD the next broad release of RoleSignal matching changes because the mandatory-credential risk needs a validated blocking control before expanding the release.** This decision concerns broader release of matching changes, not a claim that RoleSignal's existing product or all current scenarios have failed.

## The Arguments

### 1. User trust depends on evidence-grounded recommendations

RoleSignal's core promise is to identify worthwhile career opportunities without overstating what a candidate's experience proves. The Module 2 manual review confirmed three overconfident recommendations among 20 scenarios, including a **STRONG MATCH** for an ICU Charge Nurse role even though active RN licensure had not been verified. This is a recommendation-confidence failure, not an allegation that the model fabricated a license. **An unverified mandatory requirement cannot be treated as satisfied without putting the credibility of the matching product at risk.**

### 2. Evaluation gates must be validated before broad release

The proposed P0 control requires a **100% catch rate on known mandatory-credential regression cases**, but the available artifacts do not establish that this blocking gate is implemented and enforced in RoleSignal's release pipeline. The eight newer scenario runs reported passes, including a missing-hard-requirement calibration case; their exact assertions and equivalence to the full credential gate remain unverified. **Successful individual scenarios are useful progress, but not sufficient evidence that the approved release condition has been met.**

### 3. A targeted HOLD protects business continuity while remediation proceeds

This is a **HOLD on the next broad release of matching changes**, not a recommendation to shut down the existing product or stop development. Engineering can continue controlled testing and implement the mandatory-credential gate while Product evaluates readiness against the agreed release criteria. The evaluation investment plan prioritizes hallucination and fairness, with fairness mitigation scheduled for December 15, 2026. **Keeping the HOLD scoped to expansion limits additional exposure to a known P0 trust risk without blocking productive work on the fix.**

**Learner-selected structure and rationale:** Option A, customer trust, validated evaluation gates, and targeted HOLD/business continuity; “option A because trust and readiness is key.” Specific findings are drawn from the prior RoleSignal module artifacts. Numeric result-to-gate comparisons belong in Step 3.

## Evidence · Trust Metrics

**Decision-relevant evidence, with explicit source and gate status.** These six measures cover different datasets and evaluation modes; they are **not** one combined pass rate. `UNVERIFIED` means no valid result against the stated release gate has been demonstrated, not that the system necessarily fails it.

| Metric | Recorded result | Gate / decision bar | Status | Source and evidence type |
|---|---|---|---|---|
| **Manual career-fit accuracy / overconfidence** | **17/20 PASS (85%); 3/20 FAIL (15%)** after the learner's T01 override. D01, D03 and T05 were overconfident STRONG MATCH assessments; no credential was fabricated. | **No retrospective 20-case pass-rate floor was approved.** The later D03/D01/T05 gates are targeted and require separate labeled suites. | **3 confirmed failures; no global gate verdict** | [M2 failure audit](../02-failure-discovery/audit-log.md), human-reviewed manual GPT-family chat evaluation; **RoleSignal case evidence** |
| **D03 mandatory-credential detection** | Adapted deterministic eligibility check caught **1/1 known D03 P0 case**. A separate simplistic unsupported-claim detector missed it (**0/1**); the live LLM judge **was not run**. | **Hard PR target: 100% catches on the defined mandatory-credential regression suite**, including varied verified/unverified/absent cases and controls. | **UNVERIFIED for release**: one prototype catch is not a validated suite or deployed PR gate | [M3 three-layer eval](../03-eval-suites/lab-1-eval-suite.md); [M4 release criteria](../04-eval-gates/lab-2-launch-strategy.md); **single-case prototype + proposed gate** |
| **Newer RoleSignal scenario checks** | **8/8 reported “All passed”** on **November 6, 2026**, including a missing-hard-requirement calibration scenario. | **Eight configured scenario checks**; underlying assertions and equivalence to the complete D03 gate **not established**. | **PASS on reported scenarios only; broader release UNVERIFIED** | [M5 coverage matrix](../05-scale/lab-1-coverage-matrix.md), learner-supplied scenario-run screenshot; **RoleSignal scenario-run evidence** |
| **Judge calibration / grounding** | **Cohen's κ = 0.67**, with **10/12 agreement (83.33%)** on course baked-in demo labels. | **Course calibration gate κ ≥ 0.60**. | **PASS for course demo only**; no independently re-run RoleSignal judge validation | [M3 judge calibration](../03-eval-suites/lab-judge-calibration.md); **course demo, not live RoleSignal performance** |
| **Faithfulness regression, PR #218** | **96 → 87 (−9 points)** on the course's 30-case simulated replay. | **Blocking floor ≥90; max 3-point regression**. | **FAIL / BLOCK in course simulation**; **not** a real RoleSignal PR or live CI result | [M4 CI gate policy](../04-eval-gates/lab-ci-gate-policy.md); **simulated course replay** |
| **Fairness evaluation coverage** | **❌ No demonstrated fairness testing**; Bias was one of **3/5 coverage gaps** in M5 (alongside Toxicity and Drift Monitoring). | **Critical mitigation assigned to Product owner + Engineering by December 15, 2026**; no measured fairness acceptance threshold yet. | **UNVERIFIED / coverage GAP**; no numeric bias rate established | [M5 coverage matrix](../05-scale/lab-1-coverage-matrix.md); **coverage audit and dated mitigation commitment** |

**Decision interpretation:** The **HOLD** rests on the confirmed D03 P0 failure and **absence of evidence that the 100% mandatory-credential regression gate is deployed and validated**. The 8/8 passing scenarios are favorable, but do not override that missing release assurance. The simulated PR #218 grounding failure is a policy demonstration, **not an additional observed RoleSignal failure**. The κ result validates only the course's demo judge labels.

**Supporting scale and budget context (not a seventh trust metric):** The [M5 budget decision](../05-scale/lab-2-budget-crisis.md) allocated **$154,750 of the $200,000 quarterly exercise cap**, including **$85,000 L3 for Hallucination** and **$55,000 L3 for Bias**, using **2/3 Level-3 slots**, with **$45,250 unallocated**. These are **course-budget allocations, not actual expenditure**. The supplied eight recorded scenario durations span **6.6–16.9 seconds**; **no approved RoleSignal latency threshold or validated p95** exists, so no latency PASS/FAIL is asserted.

**Learner-selected evidence package and rationale:** Full six-metric table, with simulation and deployment limitations labeled; “The judge-calibration result and evaluation budget can provide supporting context without distracting from the central decision.”

## Business Risk

**SHIP path: known trust exposure.** In the Module 2 human-reviewed, 20-scenario audit, **3/20 (15%)** recommendations failed, including the **P0 D03** STRONG MATCH despite unverified mandatory RN licensure. The adapted deterministic eligibility check caught D03 in **1/1** prototype case, but the proposed **100% catch rate across the defined mandatory-credential regression suite** has **not** been validated as a deployed PR gate. Expanding matching changes before that validation risks misleading users about eligibility, damaging confidence in recommendations and potentially causing user abandonment. **No measured churn, lost conversion, or dollar exposure is available**, and the 15% audit failure share must not be interpreted as a customer-impact or churn rate.

**HOLD path: delivery and opportunity cost.** A targeted HOLD delays the next broad release of matching changes and the potential user benefits of those changes, while Product and Engineering conduct gate validation. The existing product, remediation and controlled tests may continue. The number of delayed users, duration of the hold, resulting revenue impact, and competitive-window costs have **not** been measured. The **8/8 passing scenarios** are encouraging but do not demonstrate enforcement of the required P0 regression gate.

**Business decision:** Prioritize containing a confirmed high-severity trust risk over an unquantified near-term release benefit. Do not treat the course's simulated PR #218 block or the Module 5 hypothetical **$154,750 evaluation allocation** as actual RoleSignal production incidents or expenditure.

## Next Step · Decision Needed

**By November 13, 2026, Product Leadership should approve the targeted HOLD on the next broad release of RoleSignal matching changes and authorize the Product owner and Engineering to implement and validate the mandatory-credential regression gate.** Before broad rollout resumes, require documented evidence that the Hard PR control catches **100% of the known unverified/absent mandatory-credential regression cases in the defined suite**, with verified-credential controls reviewed for overblocking; record the test dataset, results, failures, owners, and the release sign-off. Continue controlled evaluation and existing product operations during the HOLD. **November 13 is the leadership decision deadline, not a claim that remediation will be completed by that date.**

## Reflection

“A high pass rate does not necessarily mean a product is ready to scale. We need to identify which failures matter most and build controls that prevent those failures without limiting RoleSignal's ability to discover unconventional career opportunities.”

**Product lesson:** “Good enough” is risk-dependent. A useful exploratory recommendation can acknowledge uncertainty; a STRONG MATCH for a role requiring an unverified mandatory credential needs a harder eligibility constraint. A passing scenario count alone cannot establish release readiness without testing the high-consequence failure mode.

**Learner-approved Step 4 choices:** Present observed **3/20** failures and explicitly state that financial impact is unmeasured; request a targeted HOLD and P0 gate validation, with a leadership decision by **November 13, 2026**. The quoted reflection above is the learner's own wording.
