# Failure Taxonomy Canvas · Ascend IQ

> Repo file `ai-evals/02-failure-discovery/failure-taxonomy.md`. Becomes the **Failure Taxonomy** slide of the final pitch deck (Module 6) and feeds the Module 3 eval suite.

## How to complete this file

1. First complete `audit-log.md` (the failure audit) — this canvas prioritizes the failures you found there.
2. Open the **M2 · Failure Taxonomy Canvas** tool from the Module 2 deck. Fill the three risk cards (click **↺ Load Ascend IQ defaults** to see a worked example first), then click **📋 Copy markdown** and paste it over the template below.
3. Anchor severity to the **user promise / trust metrics you chose in the Module 1 Strategy Canvas** (`ai-evals/01-evaluation-strategy/strategy-canvas.md`) — severity is a strategic judgment, not just a frequency count.

**Definition of done —** you're finished when the Top 3 table is fully filled (no `_…_` left), the #1 risk has a one-sentence Business Impact Statement in leadership language, and the prioritization is defended in 2–3 bullets.

### Scoring guides

**Frequency** = how many of the 20 audited rows carry this Trust Metric tag. **≥ 3 of 20 = HIGH** frequency; ≤ 2 = LOW.

**Severity (P0–P3)** — a strategic call about business cost, independent of how often it happens:

| Level | Meaning | Rough test |
|---|---|---|
| **P0** | Crisis Zone | Blocks the core promise; legal, compliance, or contract-breaking. |
| **P1** | Hidden Risk | Real damage to trust or revenue, but survivable short-term. |
| **P2** | Annoyance | Degrades experience; a workaround exists. |
| **P3** | Low Priority | Cosmetic or rare. |

**Agentic mode** (optional) — if the failure lives in the *trajectory* (the path of tool calls), tag it: `TOOL_MISUSE`, `REASONING_LOOP`, `SCOPE_ESCALATION`, or `RECOVERY_FAILURE`. Leave blank for output-only failures.

## Top 3 Prioritized Failures

| Rank | Failure Type | Trust Tag | Agentic Mode | Frequency | Severity | Business Impact |
|---|---|---|---|---|---|---|
| 1 | D03 — Strong-match recommendation with unverified mandatory RN licensure | `#HALLUCINATION` | Output-level (none) | 1/20 · LOW | **P0** | Potential serious reputational harm from overstating eligibility for a credential-dependent role; users may lose confidence and trust in RoleSignal. |
| 2 | D01 — Overstated senior-management readiness with unverified team-leadership scope | `#HALLUCINATION` | Output-level (none) | 1/20 · LOW | **P1** | Misleading strong-match recommendations for leadership roles could waste users' effort and erode confidence in the product. |
| 3 | T05 — Overconfident transferable-skill match despite unverified training and rollout experience | `#HALLUCINATION` | Output-level (none) | 1/20 · LOW | **P1** | Overstating readiness for a career transition could weaken trust in RoleSignal's core transferable-skills promise. |

**Prioritization rationale (learner-confirmed):** All three errors risk reputational harm and users losing faith and trust in the product. Mandatory-credential uncertainty is the highest priority due to its potentially serious reputational consequences.

**Frequency note:** Each distinct failure type occurred once (LOW, 1/20). Their common mechanism, overconfident recommendations despite acknowledged evidence gaps, occurred 3/20 (HIGH in aggregate); that aggregate is not the individual failure-type frequency.

## #1 Risk · Business Impact Statement

> This failure matters because recommending candidates as strong matches for roles requiring unverified mandatory credentials undermines confidence in RoleSignal's career-fit intelligence, creating serious reputational risk and potentially driving user abandonment.

## Defending the Prioritization

- **Core promise at risk:** RoleSignal's value depends on distinguishing demonstrated qualifications from missing or unverified requirements. Failing that distinction undermines evidence-grounded career intelligence.
- **Severity over frequency:** This specific mandatory-credential failure appeared in only 1 of 20 test cases (LOW frequency), but a misleading recommendation involving mandatory professional credentials can cause disproportionate reputational harm; that potential impact supports the learner's P0 designation. The broader overconfidence mechanism appeared in 3 of 20 cases (HIGH aggregate frequency).
- **Commercial implications:** If users stop trusting strong-match recommendations, they may disengage from the platform, decline to subscribe, or discourage others from using it. These are potential business consequences, not measured churn or revenue outcomes.
