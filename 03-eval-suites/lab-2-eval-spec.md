# M3 · Lab 2 · Evaluation Specification — RoleSignal D03 P0

> Product-specific evaluation contract derived from the Module 2 confirmed D03 failure and the Module 3 Lab 1a evaluation. **This is a proposed acceptance standard, not an assertion of production performance.**

## Part 1 · The 5-Part Eval Spec

| Question | Answer |
|---|---|
| **01 · Target Risk** | RoleSignal returns **STRONG MATCH** for a role requiring a mandatory professional credential when the candidate's supplied evidence does not verify that credential. D03: ICU Charge Nurse requiring an active RN license, with the candidate's current licensure unverified. |
| Risk Type | **Output-level** recommendation/eligibility overconfidence (not a trajectory failure). Module 2 trust tag: `#HALLUCINATION` in the course's completeness-vs-reference sense; no credential was explicitly fabricated. |
| Trust Metric | **Evidence-Grounded Fit Explanations** (Module 1): recommendations must distinguish evidenced qualifications from unknown eligibility requirements; also protects High-Fit Recommendation Precision. |
| **02 · Evaluator** | **Hybrid:** deterministic mandatory-credential eligibility gate (Layer 2) as the primary blocking control; use a semantic LLM judge or human escalation for ambiguous wording or credential mappings when available. |
| Detection logic | Extract mandatory professional credentials from the target role; compare each against explicit candidate evidence with states **verified / unverified / explicitly absent**. If any mandatory credential is not verified, flag and block **STRONG MATCH**. Do not interpret missing evidence as proof the candidate lacks the credential. Route ambiguous requirements or evidence for further review rather than auto-verification. |
| **03 · Threshold** | **100% catch rate** for known unverified/absent mandatory-credential cases in the defined regression suite: **0 false-clearance STRONG MATCH outputs** on these labeled test cases. Denominator is all regression cases with a mandatory credential that is not verified; measure separately on verified-credential controls to detect overblocking. Target is a release gate, **not yet empirically validated**. |
| Strategy | **Safety-first** (prioritize avoiding false clearance of unverified mandatory requirements). |
| **04 · Business Stakes** | **P0 reputational/trust risk:** overconfident eligibility recommendations could undermine RoleSignal's core evidence-grounding promise, cause users to waste effort, and lead to abandonment or adverse word of mouth. These are potential costs, not observed churn. |
| **05 · Owner** | **Product owner (learner):** owns policy, risk acceptance, threshold, and evaluation signoff. **Engineering:** accountable for building and maintaining the gate, regression tests, logging, and operational implementation. |

**Scope and measurement note:** The 100% target applies to the labeled, defined regression suite, not a promise of perfect production detection. Track both catches (sensitivity for ineligible/unverified cases) and overblocks of genuinely verified cases. The one-case D03 test proves detection for that example only; credential extraction, synonyms, renewal status, and changing role requirements need broader coverage tests.

## Part 2 · Three Audience Messages

### A. For Engineering (Jira ticket)

**Implement a mandatory-credential strong-match gate.**

- **GIVEN** a role explicitly requires an active professional credential and the candidate profile does not verify its active status, **WHEN** RoleSignal calculates the fit recommendation, **THEN** it must **not** output STRONG MATCH, regardless of other relevant experience; it should record the unverified requirement as a gap.
- **GIVEN** a candidate's provided evidence explicitly verifies the required active credential, **WHEN** RoleSignal evaluates the role, **THEN** the credential gate must not block STRONG MATCH *on credential grounds alone*; other fit criteria still apply.
- **GIVEN** credential evidence or job requirements are ambiguous, **WHEN** verification cannot be established confidently, **THEN** classify the credential as **unverified**, route to an appropriate clarification/review pathway, and avoid STRONG MATCH until verified.
- **Release acceptance:** catch **100%** of labeled unverified mandatory-credential cases in the regression suite (zero false clearances), record pass/fail by case, and track false-positive blocks on verified-credential controls. The release gate does not claim perfect coverage beyond this suite.

### B. For UX / Design

When the gate blocks STRONG MATCH, display an **EXPLORATORY / Verification Needed** assessment rather than labeling the candidate unqualified. Clearly name the mandatory credential and state: *“This role requires an active RN license, but your current license status wasn't verified from the information provided.”* Invite the user to supply or confirm documentation/details, then rerun the assessment after verification. Keep demonstrated transferable strengths visible, but do not imply the credential is established.

### C. For Leadership (bi-weekly update)

- **P0 risk reduction:** Introduce a mandatory-credential gate to prevent unsupported **STRONG MATCH** recommendations in **100% of known unverified-credential regression cases**. This protects trust in RoleSignal's evidence-grounded fit explanations. Track **regression catch rate, false-clearance count, verified-candidate overblock rate, and user corrections**; measure any downstream retention or trust impact separately rather than assuming revenue savings.
