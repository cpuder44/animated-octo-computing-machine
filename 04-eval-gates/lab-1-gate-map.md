# Module 4 · Eval Gate Map · RoleSignal

> Builds on the three **confirmed** Module 2 failures and the Module 3 D03 eligibility-gate specification. Thresholds and merge policy belong to later Module 4 steps; this file records the learner's approved placements.

## Context

The RoleSignal 20-case audit identified three confirmed failures: **D03 (P0)**, **D01 (P1)**, and **T05 (P1)**. All were classified `#HALLUCINATION` under the course's factual/completeness category, specifically **overconfident STRONG MATCH recommendations despite acknowledged evidence gaps**, not fabricated credentials. **T01 was human-overridden to PASS** and is not gated as a failure. No refusals occurred.

## Gate Map

| Row | Failure Mode | Severity | Placement | Rationale |
|---|---|---|---|---|
| **D03** | Unverified mandatory RN license, yet STRONG MATCH for an ICU Charge Nurse role | **Hard** | **PR** | **P0**: Enforce the mandatory-credential gate through deterministic regression checks before merge. An unverified required credential must prevent an unqualified STRONG MATCH; serious potential reputational harm warrants a blocking control. |
| **D01** | Senior AML manager STRONG MATCH without verified team-management scope | **Soft** | **Staging** | **P1**: Review recommendation confidence against senior-management requirements in a pre-release environment. A failure should trigger investigation and mitigation rather than automatically blocking every change. |
| **T05** | Healthcare implementation STRONG MATCH without verified training or rollout-support experience | **Advisory** | **Release** | **P1**: Track and review overconfident transferable-skill recommendations at release. Treat as a visible trust-risk signal without automatically blocking potentially valuable unconventional career discovery. |

**Learner confirmation:** D03 = Hard at PR; D01 = Soft at Staging; T05 = Advisory at Release. Learner rationale: “they make sense.” The detailed placement explanations above describe the risk trade-offs implied by those selections, not additional learner-supplied claims.

**Implementation boundary:** These are **proposed gate policies**, not evidence that GitHub Actions, staging checks, or release monitoring are already deployed. Module 4 Steps 2 and 3 will define CI floors, merge rules, release thresholds, and mitigations.

## Sample Interactions (for reference)

### D03 · Mandatory credential not verified
- **Input:** Candidate: Registered nurse with 7 years of ICU practice and shift coordination. Target: ICU Charge Nurse requiring an active RN license and critical-care leadership.
- **Output (excerpt):** “**Gaps/uncertainty:** Active RN licensure is required but current license status is not explicitly provided.” Followed by “**Recommendation: STRONG MATCH** — Strong ICU and coordination experience, subject to confirming active RN licensure and leadership expectations.”
- **Human reference:** **EXPLORATORY** until active RN licensure is verified.
- **Failure reasoning:** The recommendation's highest-confidence label was not constrained by a mandatory unverified credential. The agreed Hard PR gate targets precisely this incompatibility.

### D01 · Team-management scope not verified
- **Input:** Candidate: AML investigations lead with 8 years conducting EDD and SAR escalations. Target: Senior AML Investigations Manager requiring EDD, escalation, and team leadership.
- **Output (excerpt):** “**Gaps/uncertainty:** ‘Investigations lead’ suggests leadership responsibility, but specific team-management scope is not provided.” Followed by “**Recommendation: STRONG MATCH** — Substantial directly relevant AML, EDD, and escalation experience; leadership scope should be validated.”
- **Human reference:** **EXPLORATORY** because evidence for senior-level team management is insufficient.
- **Failure reasoning:** The model identified the management gap but nevertheless overstated readiness. The Soft Staging gate calls for review and mitigation.

### T05 · Training and rollout support not verified
- **Input:** Candidate: Hospital operations coordinator who redesigned intake, mapped handoffs, and tracked wait times. Target: Healthcare Implementation Specialist requiring workflow, training, and rollout support.
- **Output (excerpt):** “**Gaps/uncertainty:** Training delivery and direct rollout-support experience are not explicitly stated.” Followed by “**Recommendation: STRONG MATCH** — Relevant healthcare workflow expertise transfers well, with training and rollout responsibilities requiring confirmation.”
- **Human reference:** **EXPLORATORY** because direct training and rollout-support experience are unverified.
- **Failure reasoning:** Relevant transferable strengths do not independently verify implementation-specific requirements. The Advisory Release gate monitors this confidence risk while preserving discovery.

**Step 1 checkpoint:** Three verified failures placed, each with a rationale; at least one **Hard**, **Soft**, and **Advisory** gate. No later Module 4 deliverables modified.
