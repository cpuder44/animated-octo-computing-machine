# Lab 2, Ascend IQ Budget Crisis

> Repo file `ai-evals/05-scale/lab-2-budget-crisis.md`. Allocate Level 1/2/3 coverage across the 5 failure modes under the **$200K/quarter cap** with **max 3 at Level 3**.
>
> Fill this with the **Budget Crisis Tool**, then **Copy markdown** and paste it over this file. The headings below mirror the tool's output exactly.

**Quarterly budget cap:** $200,000
**Total allocation:** **$154,750**
**Unallocated capacity:** **$45,250**
**Total Level 3 spend:** **$140,000 (2 of max 3 L3 slots used)**

## Portfolio decision grid

| Failure | Trust metric | Risk | Level | Cost |
|---|---|---|---|---:|
| Data Fabrication (Hallucination) | Evidence-Grounded Fit Explanations / Hallucination Rate | **P0** | **L3** | **$85,000** |
| Context Specificity | Transferable Skill Recognition / UX Trust | **P1** | **L2** | **$7,000** |
| Source Attribution Failure | Evidence-Grounded Fit Explanations / Robustness | **P1** | **L2** | **$6,500** |
| Data Bias | High-Fit Recommendation Precision / Fairness | **P2 in course; critical mitigation for RoleSignal** | **L3** | **$55,000** |
| Cost Overruns (Latency) | Latency | **P3** | **L1** | **$1,250** |
| **Total** | | | **2 L3 slots** | **$154,750** |

**Running spend:** $85,000 → $92,000 → $98,500 → $153,500 → **$154,750**. This is **$45,250 below** the $200,000 quarterly cap and uses **2 of 3** permitted L3 slots.

**Learner's investment rationale:** “prioritizing Hallucination and Bias for comprehensive coverage, given your previous decisions. That protects the P0 credential problem and invests in the fairness gap you've committed to addressing.” The P0 refers to RoleSignal's unverified mandatory-credential recommendation risk; Bias/Fairness is a critical gap from Module 5 Lab 1 even though the generic course budget labels it P2.

**Budget assumptions:** The supplied exercise sets L3 reference costs at Hallucination $85K, Context $70K, Attribution $65K, Bias $55K, and Latency $25K; L2 is approximately 10% and L1 approximately 5% of each L3 cost. Figures represent a **course allocation exercise**, not verified RoleSignal expenditures.

## Fallback methods (non-Level 3 items)

### L_n_ · _Failure name_ (_metric_ · _risk_)
- **Method:** _the cheaper fallback you'll run instead of L3_
- **Why this fallback is defensible:** _the story you could defend in a customer incident review — especially if you downgraded a P0/P1._
