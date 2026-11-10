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

The three non-L3 categories below retain focused, cheaper checks. These are **approved fallback approaches**, not a claim that all monitoring workflows are already deployed.

### L2 · Context Specificity (Transferable Skill Recognition / UX Trust · P1)
- **Method:** Maintain a **human-reviewed transferable-career regression set** covering unconventional transitions and roles where relevant experience is not reflected in familiar titles. Compare candidate evidence, job requirements, RoleSignal's fit label, and explanation to expert-approved references. Include cases where transferability is plausible but a material requirement remains unverified. Record mismatches and re-test known failures after matching changes.
- **Why this fallback is defensible:** In a customer incident review, we could show that we deliberately tested the product's central career-discovery promise against labeled examples rather than treating keyword or title similarity as the standard. L2 does **not** offer comprehensive coverage, so recurring missed transferable skills or unjustified strong matches would justify escalation and additional investment.

### L2 · Source Attribution Failure (Evidence-Grounded Fit Explanations / Robustness · P1)
- **Method:** Perform **sampled manual claim-to-source verification** of fit recommendations, comparing material claims in the output with the specific candidate-profile and job-requirement evidence. Document unsupported claims and incorrect confidence labels, and add confirmed errors to future regression samples. Prioritize claims involving mandatory credentials and senior-role prerequisites.
- **Why this fallback is defensible:** For a customer incident, reviewers could inspect the actual supporting sources and trace how a recommendation was justified or overstated. The separate L3 Hallucination allocation prioritizes RoleSignal's P0 credential failure, while sampled attribution review adds an independent, less expensive check. Sampling cannot guarantee every unsupported claim is found; confirmed serious failures must trigger investigation rather than being dismissed because this category is L2.

### L1 · Cost Overruns / Latency (Latency · P3)
- **Method:** Use **scenario-run duration monitoring against the observed baseline** from the learner's November 6, 2026 screenshot (eight recorded runs ranging from **6.6 to 16.9 seconds**). Keep a simple dated log of subsequent scenario timings and examine conspicuous slowdowns or changes by scenario type. Do **not** label any single duration as a threshold violation: no user-facing latency target or validated p95 baseline has yet been established.
- **Why this fallback is defensible:** The learner's stated rationale is: “The current evidence demonstrates timing measurement but doesn't yet establish a user-facing performance threshold. Basic monitoring provides visibility while budget is concentrated on higher-impact trust risks.” In an incident review, we could present observed timings and any follow-up rather than claim an unimplemented latency SLA. A repeated user-impacting slowdown would prompt re-prioritization and development of a defined threshold.

**Learner-approved methods:** Context Specificity = human-reviewed transferable-career regression set; Source Attribution = sampled manual claim-to-source verification; Latency = scenario-run duration monitoring against the observed baseline. **Budget remains $154,750 with 2 L3 slots**, leaving $45,250 unallocated. Any stronger evaluation level requires a future, explicit allocation decision.
