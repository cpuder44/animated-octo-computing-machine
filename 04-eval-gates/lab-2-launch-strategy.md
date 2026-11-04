# Module 4 · Launch Strategy — RoleSignal

> **Status: proposed release policy, learner-approved.** Builds on Module 2 confirmed failures D03, D01, T05; Module 3 D03 evaluation specification; and Module 4 Steps 1–2. The thresholds below are **release targets, not observed RoleSignal performance**. No deployed CI or release gate is claimed.

## 4.0 Release Criteria

| Severity | Metric | Threshold | Dataset | Method |
|---|---|---|---|---|
| **Hard · D03 (PR)** | Catch rate for **STRONG MATCH** recommendations where a mandatory professional credential is unverified or explicitly absent | **100% caught** (zero false clearances among labeled negative credential cases); failing the gate **blocks PR merge** | RoleSignal **mandatory-credential regression fixture suite** derived from D03, expanded to verified, unverified, absent, and ambiguous-credential controls (planned; actual expanded set not yet established) | Deterministic replay and credential-evidence state validation: when mandatory verification is missing, assert the recommendation is **not STRONG MATCH**; track failed cases and verified-control overblocking separately |
| **Soft · D01 (Staging)** | Share of labeled senior-management assessments incorrectly marked **STRONG MATCH** despite unverified material leadership requirements | **≤5%** overconfident leadership recommendations; above threshold requires investigation and feature-flag mitigation before controlled progression | RoleSignal **leadership-fit labeled staging evaluation set** anchored to D01 and additional varied senior-role cases (planned) | Compare fit labels with human-reviewed evidence-based references; count unsupported strong matches / all evaluated leadership cases; report numerator, denominator, and uncertainty |
| **Advisory · T05 (Release)** | Share of labeled transferable-skill transition assessments incorrectly marked **STRONG MATCH** despite unverified material requirements | **≤10%** overconfident transferable-skill recommendations as a monitoring target; exceeding it triggers review/alert, **not an automatic release block** | RoleSignal **transferable-skill labeled release monitoring set** anchored to T05 and additional transition cases (planned) | Sample and compare fit labels to human-reviewed references; report unsupported strong matches / all assessed transition cases, trends, and follow-up actions |

**Important measurement boundaries:** For D03 the 100% criterion applies to **known, labeled mandatory-credential regression cases**, not all possible real-world jobs. To measure the 5% and 10% limits meaningfully, use sufficiently large labeled cohorts and publish sample sizes; the original 20-case audit cannot validate these rates. A verified credential alone does not guarantee STRONG MATCH, and unknown credential evidence does not mean the candidate lacks the credential. Correct refusals and correct cautious assessments must not be penalized.

**Learner decisions:** D03 Hard = 100% known-case catches; D01 Soft = at most 5%; T05 Advisory = at most 10%. Learner reasoning: “they make sense.” The operational explanations here elaborate the approved choices rather than claiming separately supplied learner justifications.

## 4.1 CI Gate Policy

Use **deterministic fixture/replay** on a **golden regression set of at least 30 cases**, evaluated **per dimension**, never one blended quality score. A blocking dimension fails if **PR score < floor** OR **(main score − PR score) > max permitted regression**. Warn-only dimensions raise notifications but cannot independently block the merge. The P0 D03 credential regression gate is additionally blocking at PR.

| Dimension | Floor | Maximum regression (points) | Enforcement |
|---|---:|---:|---|
| Faithfulness (grounding) | **90** | **3** | **Block** |
| Task completion | **85** | **5** | **Block** |
| Tool selection | **80** | **5** | **Block** |
| Safety / policy | **98** | **1** | **Block** |
| Latency (p95) | **70** | **8** | Warn-only |
| Cost per task | **70** | **10** | Warn-only |

**Course PR #218 replay (illustrative, not an actual RoleSignal PR):** Faithfulness fell **96 → 87 (−9 points)**, breaching its **90** minimum and **3-point** regression limit. **BLOCK MERGE**; the other five dimensions passed their configured checks. See `lab-ci-gate-policy.md` for the scored table and the learner's rationale. Avoid live LLM calls in CI; replay fixed inputs, recorded traces, and deterministic/previously labeled evaluator outputs. Refresh golden references through a separately governed process.

## 4.2 Mitigation Plan · Soft Gate

**Selected Lever: Feature flagging.**

**Mitigation statement:** If D01's leadership-overconfidence rate exceeds **5%** in staging, keep the affected senior-management matching behavior behind a feature flag, disable or revert the risk-prone pathway, and permit progression only with documented product/engineering review and monitoring, while keeping the **D03 Hard credential gate non-bypassable**.

The flag may scope an experimental leadership recommendation change without suppressing all unconventional career discovery. Product owns risk acceptance and reviews the staging results; Engineering owns flag behavior, rollback, and telemetry. Advisory T05 breaches prompt visible monitoring and triage rather than an automatic release stop.

**Implementation status:** This is a specified release strategy, not evidence that the feature flag, monitoring, labeled cohorts, or CI are currently deployed.
