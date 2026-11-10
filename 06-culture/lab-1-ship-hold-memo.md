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

```
- Metric: result (Gate: bar) PASS/FAIL · Source
- … cite exact numbers from M2–M5 (hallucination rate vs gate, factual grounding %, bias coverage %, p95 latency)
```

## Business Risk

_Quantified SHIP-path vs HOLD-path risk (revenue, churn, competitive window)._

## Next Step · Decision Needed

_A specific decision request with a deadline — e.g. "Approve the Hold rollback by Friday to keep the Q3 launch window."_

## Reflection

_What defining "good enough" forced you to confront._
