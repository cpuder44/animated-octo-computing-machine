# M3 · Lab 1b · Trajectory Evaluation — Cortex T-LOOP

> Recorded trajectory: `03-eval-suites/cortex-eval/cortex-traces.json`, trace `T-LOOP`. This lab uses the course's recorded Cortex path to practice trajectory evaluation; RoleSignal's D03 credential P0 from Module 2 remains the separate output-level risk evaluated in Lab 1a.

**Matching mode:** **Unordered** — learner-selected because strict ordering often penalizes valid alternative workflows. Required steps must be present, but their order need not be identical.

**Score:** **2 PASS / 1 PARTIAL / 3 FAIL** across six dimensions (equivalently 2 fully passed of 6). **Verdict: HOLD** — learner-selected, consistent with notebook logic.

## Dimension scores

| Dimension | Score | Note |
|---|---|---|
| Tool selection | **FAIL** | Attempted `predict_churn(P-NORTH)`, a nonexistent tool. |
| Argument correctness | **PASS** | The trace contains no `wrong_arg` flags; project IDs on recorded calls are consistent. This score does not excuse the nonexistent tool. |
| No redundant / looping steps | **FAIL** | Repeated identical `get_activity(P-NORTH)` calls twice after the initial successful call. |
| Recovery | **PASS** | The notebook's flag-based rule marks this PASS because no step is flagged `tool_error`; however the nonexistent `predict_churn` call errored and no recovery is shown. **Rubric blind spot:** a stricter semantic recovery review could grade this FAIL. |
| Plan coherence | **PARTIAL** | Skipped the required `get_norms` step (flag `missing_step`); the remainder of the path was not flagged out of order. |
| Task completion | **FAIL** | Drafted a plausible update without the required `get_norms` check. |

## Recorded agent path

1. `get_project(P-NORTH)` — OK.
2. `get_activity(P-NORTH)` — OK.
3. `get_activity(P-NORTH)` — redundant repeat.
4. `get_activity(P-NORTH)` — redundant repeat.
5. `predict_churn(P-NORTH)` — hallucinated nonexistent tool; call errors.
6. `draft_reply()` — produced draft without `get_norms`.

**Final answer:** “DONE (queued for your review): Northstar looks healthy; activation is trending up.”

## Verdict

**HOLD.** The plausible final answer cannot compensate for a nonexistent tool call, repeated redundant calls, and a skipped required norms check. Unordered matching allows legitimate alternative ordering **without waiving mandatory steps**. The learner explicitly chose unordered matching and HOLD; their stated reason for unordered matching was that strict ordering often penalizes valid alternative workflows.

**Execution evidence:** In ChatGPT, the notebook's `trajectory_eval` flag-based logic was executed against three recorded paths without an API key: `T-GOLD → SHIP`, `T-LOOP → HOLD`, and `T-RECOVER → SHIP`. This table records the notebook's computed T-LOOP dimensions, with the recovery blind spot disclosed instead of silently changing the score.

**Step 2 checkpoint:** Matching mode selected, six dimensions scored, path-aware HOLD verdict recorded. Stop before Step 3.
