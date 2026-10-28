# Module 4 · CI Eval Gate Policy — PR #218 Replay

> **Source:** Module 4 course-provided Ascend IQ PR #218 **simulated** 30-case regression-golden-set replay, not an observed RoleSignal production pull request. The learner selected these per-dimension rules and a **BLOCK** merge decision. CI policy uses deterministic fixture/replay results; it does not call a live model at merge time.

## Per-dimension CI policy and replay result

A blocking dimension fails if **either** its PR score is **below its floor** or its drop from main **exceeds** its maximum allowed regression. Warn-only failures are surfaced but do not independently block. All figures are the course-provided scores/points, not raw outcome counts.

| Dimension | main | PR | Δ | Floor | Max reg | Blocking | Result |
|---|---:|---:|---:|---:|---:|---|---|
| Faithfulness (grounding) | 96 | 87 | −9 | 90 | 3 | yes | **FAIL — BLOCK** (floor breach; regression breach) |
| Task completion | 92 | 93 | +1 | 85 | 5 | yes | **PASS** |
| Tool selection | 90 | 88 | −2 | 80 | 5 | yes | **PASS** |
| Safety / policy | 99 | 99 | 0 | 98 | 1 | yes | **PASS** |
| Latency (p95) | 84 | 80 | −4 | 70 | 8 | no (warn-only) | **PASS** |
| Cost per task | 88 | 82 | −6 | 70 | 10 | no (warn-only) | **PASS** |

**Gate result: BLOCKED.** Faithfulness is the sole blocking failure. Its **87** PR score is **3 points below** the **90** floor, and its **9-point** decline from **96** on main exceeds the maximum allowed **3-point** regression by **6 points**. Other blocking dimensions pass; both warn-only dimensions pass their floors and regression limits.

## Merge decision

**BLOCK PR #218.** Learner rationale: “A nine-point decline in evidence grounding is significant enough to halt a merge, especially when RoleSignal's most serious risk involves recommendations that exceed the available evidence.” A gain in task completion (+1) does **not** cancel a faithfulness gate failure. Latency and cost are **warn-only**, so neither would block the merge on its own.

**Relationship to RoleSignal:** This course replay illustrates the per-dimension gating pattern we would apply to RoleSignal's evidence-grounding and mandatory-credential P0 control. It is **not** evidence that RoleSignal's real 30-case CI suite or a GitHub Actions gate has already been implemented. Module 3's **100% mandatory-credential catch target** remains a separate, P0-specific regression acceptance criterion.

**Step 2 checkpoint:** Six dimensions with learner-confirmed floors, maximum regressions, blocking/warn-only flags, scored results and justified BLOCK call. Stop before Module 4 Step 3.
