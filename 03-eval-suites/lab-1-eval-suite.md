# M3 · Lab 1a · Three-Layer Eval Suite — RoleSignal D03 P0

## P0 Failure (carried from Module 2)

- **Query:** Candidate: Registered nurse with 7 years of ICU practice and shift coordination. Target: ICU Charge Nurse requiring active RN licensure and critical-care leadership.
- **Prediction (actual RoleSignal response):**
  - **Strengths:** 7 years of ICU practice plus shift coordination provides directly relevant critical-care experience and evidence of operational leadership.
  - **Gaps/uncertainty:** Active RN licensure is required but current license status is not explicitly provided.
  - **Recommendation: STRONG MATCH** — Strong ICU and coordination experience, subject to confirming active RN licensure and leadership expectations.
- **Reference (human-approved):** **EXPLORATORY.** Seven years of ICU experience and shift coordination are relevant, but active RN licensure must be verified.
- **Module 2 classification:** D03, `#HALLUCINATION` (completeness/overconfidence rather than fabricated credentials), **P0**, because unwarranted eligibility confidence risks serious reputational harm.

## 3-Layer Eval Suite Results

**Method:** RoleSignal-specific Python checks executed in ChatGPT on the D03 candidate requirements and prediction (no API key). The recorded run is a lightweight adaptation of the course's three-layer architecture, **not a complete run of the original Cortex Jupyter notebook or a LangSmith evaluation**. The live LLM judge was not executed due to unavailable API credits. In this lab, **1 = caught the failure**, **0 = missed**, and **n/a = not run**.

| Layer | Role | Score | Observed reasoning |
|---|---|---|---|
| **Layer 1 · Code** | Deterministic unsupported-credential-claim check | **0** | No affirmative assertion that the candidate *has* an active RN license appeared in the prediction. This rule checks fabricated credential claims, not overconfident recommendation strength. |
| **Layer 2 · Safety / eligibility** | Deterministic mandatory-credential gate, adapted for RoleSignal | **1** | The role requires an active RN license, candidate evidence did not explicitly establish active licensure, and the output recommended **STRONG MATCH**. The gate caught the conflict. |
| **Layer 3 · Judge** | Semantic LLM-as-a-Judge | **n/a — not run** | No API credits; a live judge verdict cannot be claimed. |

### Observed Python output

```text
D03 — RoleSignal three-layer suite
Layer 1 · Deterministic unsupported-claim check: 0 — No affirmative assertion of active licensure detected
Layer 2 · Mandatory eligibility gate:             1 — Strong match with unverified mandatory RN license
Layer 3 · Live LLM judge:                        n/a — no API credits; not run
Convention: 1 = caught a problem; 0 = did not catch a problem.
```

## Where the failure was caught, and what it means

**Learner decision: The Win.** Layer 2 caught the P0 failure. The prediction explicitly acknowledged uncertainty about the mandatory license, but failed to let that uncertainty appropriately constrain the strength of its recommendation. The gate flagged this real eligibility/recommendation mismatch rather than a superficial formatting issue. The result demonstrates detection **for this one test case**; broader coverage and false-positive testing remain future work.

## What I'd ship next

**Learner decision: Implement a mandatory-credential eligibility gate before displaying STRONG MATCH.** As the learner explained, the failure was “to let that information appropriately constrain the recommendation, and a mandatory gate would have constrained it.” At minimum, when a role has an explicitly mandatory credential that is not verified by candidate evidence, block the **STRONG MATCH** label and present a qualification-verification caveat or exploratory assessment instead. Do not infer that an unverified license is definitely absent.

**Step 1 checkpoint:** Real D03 case evaluated with two executed deterministic layers; Layer 3 unavailable and explicitly marked not run; learner defended “The Win” and selected one next change. **Stop here before Lab 1b.**
