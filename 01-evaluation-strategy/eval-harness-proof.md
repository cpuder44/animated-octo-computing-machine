# First LLM-as-a-Judge Eval, Module 1

> Repo file `ai-evals/01-evaluation-strategy/eval-harness-proof.md`. The eval evidence behind the **Eval Results** slide of the final pitch deck (Module 6).
>
> Fill this with the **First Eval Lab** builder, then **Copy markdown** and paste it over this file. The headings below mirror the tool's output exactly.

## Version A, Concise, system prompt used

**RoleSignal exploratory evaluation prompt (proposed for the product-specific dataset; not yet run):**

> You are RoleSignal, an AI career-fit intelligence assistant. Evaluate the candidate's background against the job description. Identify transferable skills, concrete qualifications, and meaningful gaps. Use only evidence from the supplied profile and job description. Provide a fit assessment in exactly 3 concise bullets covering strengths, gaps, and recommendation. Never invent qualifications.

**Required Module 1 email comparison, Version A (to run in Step 5):**

> You are an executive briefing assistant. Summarize in exactly 3 bullet points under 60 words. No preamble, no extra text.

## Version B, Narrative, system prompt used

**RoleSignal exploratory evaluation prompt (proposed for the product-specific dataset; not yet run):**

> You are RoleSignal, an AI career strategist. Evaluate the candidate's complete professional background against the job description. Explore non-obvious transferable skills and possible career transitions. Explain strengths, gaps, and potential opportunities in a narrative of approximately 150 words. Distinguish verified qualifications from speculative possibilities. Do not invent experience.

**Required Module 1 email comparison, Version B (to run in Step 5):**

> You are a PR communications assistant. Write a 100-word narrative summary highlighting wins first, then risks and next steps. Keep a positive tone. No bullets.

## Eval setup, dataset name + judge model/family

- **Starter dataset:** `RoleSignal-M1-Balanced-20` (20 synthetic candidate/job pairs: 5 direct matches, 5 transferable-skill matches, 5 weak/misleading matches, 5 ambiguous/incomplete profiles). Rows below are generated starting points, **not** validated golden labels.
- **Proposed generator:** ChatGPT / GPT family, using the same model for A and B.
- **Proposed independent LLM-as-a-Judge:** Claude / Anthropic model family; this is **different** from the GPT generator family. Exact model selection and actual judge execution will be recorded if used in Step 5. Do not judge GPT outputs with GPT for this test.
- **Required Module 1 run:** Compare the executive-briefing and PR-communications prompts on the **same Q4 marketing email** from the First Eval Lab Walkthrough, in separate chats or equivalent system-prompt configurations using the same generator model. Record actual outputs in Step 5; no comparison has yet run.
- **Purpose of product-specific dataset:** Subsequent RoleSignal evaluation of the three approved trust metrics. It does not replace the required Q4-email comparison.

## Cold-start, the prompt you used to seed a starter dataset

> Create exactly 20 fictional, privacy-safe candidate-profile/job-description pairs for an AI career-fit evaluation of RoleSignal. Make four balanced groups of five: (1) direct experience matches, (2) unconventional transferable-skill matches, (3) weak or misleading matches with clear skill/credential gaps, and (4) ambiguous or incomplete profiles. Vary industries and seniority. For each row provide an ID, group, short candidate evidence, and short target role requirements. Include negative evidence and uncertainty where useful. Do not assign fit scores or claim expert-validated ground truth. Keep the pairs realistic, compact, and suited to testing transferable skill recognition, evidence-grounded fit explanations, and precision of high-fit recommendations.

### Synthetic starter dataset — `RoleSignal-M1-Balanced-20`

| ID | Segment | Candidate-profile evidence | Target role requirements |
|---|---|---|---|
| D01 | Direct | AML investigations lead; 8 years conducting EDD and SAR escalations | Senior AML Investigations Manager; EDD, escalation, team leadership |
| D02 | Direct | B2B SaaS PM; 6 years owning roadmap, discovery and launches | Senior Product Manager; roadmap, user research, cross-functional delivery |
| D03 | Direct | Registered nurse; 7 years of ICU practice and shift coordination | ICU Charge Nurse; active RN license, critical care leadership |
| D04 | Direct | Data analyst; advanced SQL, dashboards and A/B tests at retailer | Product Data Analyst; SQL, experiments, stakeholder reporting |
| D05 | Direct | Customer success manager; 5 years handling enterprise renewals and onboarding | Enterprise Customer Success Manager; renewals, implementation, executive relationships |
| T01 | Transferable | Financial-crimes program manager; translated investigations into workflow specs and tested alert tools | RegTech Product Manager; user research, product requirements, risk workflows |
| T02 | Transferable | Public-school teacher; built learning programs, assessed outcomes and trained colleagues | Customer Education Program Manager; learning design, adoption metrics, enablement |
| T03 | Transferable | Military logistics officer; coordinated suppliers, risk planning and international shipments | Supply Chain Operations Manager; planning, vendor management, logistics KPIs |
| T04 | Transferable | Investigative journalist; source verification, interviews and structured research | Trust & Safety Intelligence Analyst; open-source research, evidence evaluation |
| T05 | Transferable | Hospital operations coordinator; redesigned intake, mapped handoffs and tracked wait times | Healthcare Implementation Specialist; workflows, training, rollout support |
| W01 | Weak | Junior social media coordinator; no finance, accounting or audit experience | Chief Financial Officer; accounting leadership, capital management, audit oversight |
| W02 | Weak | Software hobbyist with prototypes; no clinical degree or licensure | Physician; medical degree, active physician license, patient care |
| W03 | Weak | Marketing writer; basic spreadsheet familiarity only | Staff Machine Learning Engineer; production ML systems, advanced coding, deployment |
| W04 | Weak | Retail store supervisor; no legal education or bar admission | Corporate Counsel; JD, active bar membership, commercial contracting |
| W05 | Weak | Help desk technician; no flight training or pilot certification | Airline Captain; ATP certificate, flight-hour minimums, command experience |
| A01 | Ambiguous | Profile says 'strategy consultant' with no clients, projects or dates | Director of Corporate Strategy; market modeling, executive presentations |
| A02 | Ambiguous | Resume lists 'Python' but no projects or proficiency detail | Machine Learning Analyst; Python modeling, data cleaning, validation |
| A03 | Ambiguous | Candidate led 'compliance transformation'; team size and regulator exposure unknown | Head of Compliance Operations; people management, audits, operational controls |
| A04 | Ambiguous | Freelance UX designer; portfolio missing, no shipped-product details | Senior UX Researcher; qualitative studies, usability research, synthesis |
| A05 | Ambiguous | Former founder; business sector and responsibilities unspecified | General Manager; P&L ownership, hiring, strategy, operating cadence |

**Labeling status:** Synthetic starter inputs only. Learner/expert review, expected outcomes, adjudicated golden labels, and scoring thresholds have **not** been completed.

## Your definition of good vs bad (golden-set criteria) — the graded part, write your own

**Learner-confirmed decision: all three criteria are required.** A RoleSignal career-fit assessment **passes** only when all three are met:

1. **Transferable skill recognition:** Identifies meaningful, relevant connections between the candidate's actual experience and target role, including non-obvious transferable capabilities where supported.
2. **Evidence-grounded explanation:** Supports substantive claims with evidence in the candidate profile and job description; does not invent experience or qualifications.
3. **Recommendation quality:** Appropriately distinguishes strong, exploratory and weak matches; flags material qualification gaps and uncertainty.

**Failure rule:** Missing any one of these three conditions makes the assessment fail. Invented qualifications, missed clearly relevant transferable skills, or confidently recommending a weak match are failure examples.

**Learner-confirmed business justification:** RoleSignal's value comes from identifying career opportunities that traditional job platforms overlook, but discovery alone isn't enough. Users need to trust that the system understands their experience, can explain its conclusions, and won't waste their time with misleading recommendations. All three dimensions are essential to delivering that promise.

**Scope note:** These are RoleSignal-specific quality criteria. The Module 1 Q4 marketing-email exercise is a separate introductory test of conciseness, faithfulness and presentation; it cannot by itself validate RoleSignal career-fit quality.

### Q4 marketing email comparison — generated in ChatGPT (not independent judge scored)

**User message / source email:**

> Summarize this email for the CEO.  
> Subject: Q4 Marketing Campaign Update  
> Hi team,  
> Social media engagement is up 25% month-over-month due to the new content calendar and paid ad experiments.  
> Newsletter open rate dropped from 42% to 35%; we'll test new subject lines next week.  
> The product video campaign is delayed until November, pending legal approval; creative assets are ready.  
> Please ensure all campaign tracking links are added by Friday.  
> Best, Priya

**Version A output:**

- Social engagement increased 25% month-over-month, driven by the new content calendar and paid ad experiments.
- Newsletter open rates declined from 42% to 35%; new subject lines will be tested next week.
- Product video launch is delayed until November pending legal approval; creative assets are ready. All campaign tracking links are due Friday.

**Version B output:**

Q4 marketing activity is showing encouraging momentum. Social media engagement increased 25% month-over-month, supported by the new content calendar and paid advertising experiments. This progress provides a positive signal for the team's campaign approach.

Two areas require attention. Newsletter open rates declined from 42% to 35%, and the team plans to test new subject lines next week. The product video campaign has also been delayed until November pending legal approval, although creative assets are ready.

The immediate priority is ensuring all campaign tracking links are added by Friday. These updates will help maintain visibility into campaign performance and upcoming activities.

**Learner's winner selection:** Version A (concise executive briefing). **Learner's reasoning:** It communicates the same essential information more efficiently. **Independent judge result:** Not yet run.

**Important limitations:** These are illustrative responses generated in one ChatGPT conversation using the two prompt instructions, not verified runs with separately installed system prompts. No independent judge has scored them; the learner selected Version A as winner, with their own justification still to be recorded. Record exact separate-system-prompt runs and learner's decision before treating this as complete experimental proof.

### Learner-run A/B comparison (submitted outputs)

**Run provenance:** Learner pasted outputs from separate A/B runs. System-role configuration and model identity are learner-reported, not independently verifiable here. The original email and exact A/B prompts are recorded above.

**Version A, learner-submitted (verbatim, Markdown line structure preserved):**

```markdown
**Social media engagement increased 25% month-over-month**, driven by the new content calendar and paid advertising experiments.

1. **Newsletter open rates declined from 42% to 35%.** New subject lines will be tested next week to improve performance.
2. **Product video campaign delayed until November**, pending legal approval. Creative assets are ready; all campaign tracking links must be finalized by Friday.
```

**Version B, learner-submitted (verbatim):**

> Q4 marketing is showing encouraging momentum, with social media engagement rising 25% month over month. The new content calendar and paid advertising experiments are delivering measurable results, reinforcing the team's strategy. Some areas need attention: newsletter open rates declined from 42% to 35%, and the product video campaign has shifted to November while legal approval remains pending. Importantly, video creative assets are complete, positioning the campaign to launch once cleared. Next week, the team will test fresh newsletter subject lines to improve performance. All campaign tracking links must be in place by Friday to ensure accurate measurement across all channels.

**Descriptive checks (not an independent LLM judge):**
- A: 59 whitespace-separated words (including Markdown numbering); below 60. Preserves social +25%, newsletter 42% → 35%, video November/legal status, creative readiness, subject-line testing, Friday tracking deadline. **Format violation:** output contains an unnumbered standalone paragraph followed by a numbered list of two items, rather than exactly three bullet points.
- B: 100 whitespace-separated words, narrative without bullets, approximately 100 words. Preserves the same essential figures, risks and next steps; contains positive interpretive phrasing (e.g. strategy reinforced) that is not directly evidenced by the email.
- **Learner's preferred version:** A, because it communicates the same essential information more efficiently. This is a human preference, **not** a clean format-compliance win: A fails the exact three-bullet constraint.
- **Independent cross-family judge:** Not run (optional). **Proof:** verbatim learner-submitted outputs above; no screenshots attached.

## Screenshots, links or repo paths (optional if you followed the demo)

_2 shots: (1) eval setup (dataset + judge), (2) starter rows. Image links, or paths under `01-evaluation-strategy/screenshots/`._
