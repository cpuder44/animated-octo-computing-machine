# First LLM-as-a-Judge Eval, Module 1

> Repo file `ai-evals/01-evaluation-strategy/eval-harness-proof.md`. The eval evidence behind the **Eval Results** slide of the final pitch deck (Module 6).
>
> Fill this with the **First Eval Lab** builder, then **Copy markdown** and paste it over this file. The headings below mirror the tool's output exactly.

## Version A, Concise, system prompt used

**RoleSignal exploratory evaluation prompt (proposed for the product-specific dataset; not yet run):**

> You are RoleSignal, an AI career-fit intelligence assistant. Evaluate the candidate's background against the job description. Identify transferable skills, concrete qualifications, and meaningful gaps. Use only evidence from the supplied profile and job description. Provide a fit assessment in exactly 3 concise bullets covering strengths, gaps, and recommendation. Never invent qualifications.

**Required Module 1 email comparison, Version A (to run in Step 5):**

> You are an executive briefing assistant. Summarize the supplied Q4 marketing email in exactly 3 bullets and under 60 words. Be faithful to the source. Do not invent details.

## Version B, Narrative, system prompt used

**RoleSignal exploratory evaluation prompt (proposed for the product-specific dataset; not yet run):**

> You are RoleSignal, an AI career strategist. Evaluate the candidate's complete professional background against the job description. Explore non-obvious transferable skills and possible career transitions. Explain strengths, gaps, and potential opportunities in a narrative of approximately 150 words. Distinguish verified qualifications from speculative possibilities. Do not invent experience.

**Required Module 1 email comparison, Version B (to run in Step 5):**

> You are a PR communications assistant. Summarize the supplied Q4 marketing email in about 100 words as a narrative, presenting wins first and then risks. Do not use bullets. Be faithful to the source. Do not invent details.

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

_What makes a summary genuinely good or bad for THIS product? This is the judgment call that's yours — don't copy the example._

## Screenshots, links or repo paths (optional if you followed the demo)

_2 shots: (1) eval setup (dataset + judge), (2) starter rows. Image links, or paths under `01-evaluation-strategy/screenshots/`._
