# RoleSignal Failure Audit — Module 2

> Audit source: `01-evaluation-strategy/eval-harness-proof.md` (candidate/job queries), `02-failure-discovery/rolesignal-predictions.md` (learner-run outputs), `02-failure-discovery/rolesignal-references.md` (human-approved reference judgments), and `02-failure-discovery/rolesignal-manual-scores.md` (provisional judge scores).

## Evaluation method and limitations

The judge scores below come from a **manual GPT-family AI-chat review**, **not** an independent LangSmith or promptfoo run. GPT-family generation and grading carry same-family bias risk. The learner separately reviewed flagged results and confirmed the override and failure tags. Rows are matched against candidate/job **query text**, not LangSmith upload order; scenario IDs are included to aid verification.

## One-line summary — confirmed failures and trust tags

**3 confirmed failures out of 20** (17 final PASS): **#HALLUCINATION ×3, #UX_TRUST ×0, #ROBUSTNESS ×0, #FAIRNESS ×0**. One human override: **T01 from 0 (FAIL) to 1 (PASS)**. No refusals occurred.

## Audit rows (matched by query)

| Scenario and query | Judge score | Human override | Trust Metric tag | Failure reason or pass rationale |
|---|---:|---|---|---|
| **D01** — Candidate: AML investigations lead; 8 years conducting EDD and SAR escalations; Target role: Senior AML Investigations Manager; EDD, escalation, team leadership | 0 | — | #HALLUCINATION | STRONG MATCH understates unverified team-management scope. |
| **D02** — Candidate: B2B SaaS PM; 6 years owning roadmap, discovery and launches; Target role: Senior Product Manager; roadmap, user research, cross-functional delivery | 1 | — | — | Roadmap, discovery and launches align; gaps identified. |
| **D03** — Candidate: Registered nurse; 7 years of ICU practice and shift coordination; Target role: ICU Charge Nurse; active RN license, critical care leadership | 0 | — | #HALLUCINATION | STRONG MATCH despite unverified active RN licensure, a mandatory qualification. |
| **D04** — Candidate: Data analyst; advanced SQL, dashboards and A/B tests at retailer; Target role: Product Data Analyst; SQL, experiments, stakeholder reporting | 1 | — | — | SQL and experimentation align; reporting uncertainty noted. |
| **D05** — Candidate: Customer success manager; 5 years handling enterprise renewals and onboarding; Target role: Enterprise Customer Success Manager; renewals, implementation, executive relationships | 1 | — | — | Enterprise onboarding and renewals align; executive gap noted. |
| **T01** — Candidate: Financial-crimes program manager; translated investigations into workflow specs and tested alert tools; Target role: RegTech Product Manager; user research, product requirements, risk workflows | 0 | 0 → 1 (PASS); learner: 'this is precisely what RoleSignal is designed to do' | — | Override: verified transferable RegTech skills and explicit acknowledgment of missing broader PM experience support exploratory career discovery. |
| **T02** — Candidate: Public-school teacher; built learning programs, assessed outcomes and trained colleagues; Target role: Customer Education Program Manager; learning design, adoption metrics, enablement | 1 | — | — | Learning design and enablement transfer appropriately. |
| **T03** — Candidate: Military logistics officer; coordinated suppliers, risk planning and international shipments; Target role: Supply Chain Operations Manager; planning, vendor management, logistics KPIs | 1 | — | — | Logistics and vendor skills transfer; KPI gap noted. |
| **T04** — Candidate: Investigative journalist; source verification, interviews and structured research; Target role: Trust & Safety Intelligence Analyst; open-source research, evidence evaluation | 1 | — | — | Investigative research transfers; domain gaps acknowledged. |
| **T05** — Candidate: Hospital operations coordinator; redesigned intake, mapped handoffs and tracked wait times; Target role: Healthcare Implementation Specialist; workflows, training, rollout support | 0 | — | #HALLUCINATION | STRONG MATCH despite unverified training and rollout responsibilities. |
| **W01** — Candidate: Junior social media coordinator; no finance, accounting or audit experience; Target role: Chief Financial Officer; accounting leadership, capital management, audit oversight | 1 | — | — | CFO financial leadership requirements unsupported; weak match appropriate. |
| **W02** — Candidate: Software hobbyist with prototypes; no clinical degree or licensure; Target role: Physician; medical degree, active physician license, patient care | 1 | — | — | Required clinical degree and licensure absent; weak match appropriate. |
| **W03** — Candidate: Marketing writer; basic spreadsheet familiarity only; Target role: Staff Machine Learning Engineer; production ML systems, advanced coding, deployment | 1 | — | — | Advanced ML engineering expertise unsupported; weak match appropriate. |
| **W04** — Candidate: Retail store supervisor; no legal education or bar admission; Target role: Corporate Counsel; JD, active bar membership, commercial contracting | 1 | — | — | JD and bar requirements absent; weak match appropriate. |
| **W05** — Candidate: Help desk technician; no flight training or pilot certification; Target role: Airline Captain; ATP certificate, flight-hour minimums, command experience | 1 | — | — | Pilot certification and flight training absent; weak match appropriate. |
| **A01** — Candidate: Profile says 'strategy consultant' with no clients, projects or dates; Target role: Director of Corporate Strategy; market modeling, executive presentations | 1 | — | — | Strategy consulting evidence incomplete; exploratory appropriate. |
| **A02** — Candidate: Resume lists 'Python' but no projects or proficiency detail; Target role: Machine Learning Analyst; Python modeling, data cleaning, validation | 1 | — | — | Python skill detail insufficient; exploratory appropriate. |
| **A03** — Candidate: Candidate led 'compliance transformation'; team size and regulator exposure unknown; Target role: Head of Compliance Operations; people management, audits, operational controls | 1 | — | — | Compliance operational leadership details missing; exploratory appropriate. |
| **A04** — Candidate: Freelance UX designer; portfolio missing, no shipped-product details; Target role: Senior UX Researcher; qualitative studies, usability research, synthesis | 1 | — | — | UX research proficiency unverified; exploratory appropriate. |
| **A05** — Candidate: Former founder; business sector and responsibilities unspecified; Target role: General Manager; P&L ownership, hiring, strategy, operating cadence | 1 | — | — | Founder responsibilities unspecified; exploratory appropriate. |

## Human overrides and confirmed failures

- **T01 — Override 0 → 1 (PASS):** Learner explanation: *“T01 should pass because this is precisely what RoleSignal is designed to do.”* It recognizes financial-crime expertise transferring to RegTech product management while noting gaps. This is a learner-approved exception to the provisional judge's overly strict interpretation of STRONG MATCH; it is not a refusal override.
- **D01 — Confirmed FAIL, #HALLUCINATION:** Confidence exceeds evidence for senior-management leadership requirements.
- **D03 — Confirmed FAIL, #HALLUCINATION:** Confidence exceeds evidence for an active professional license requirement.
- **T05 — Confirmed FAIL, #HALLUCINATION:** Confidence exceeds evidence for core training/rollout responsibilities.

**Tagging clarification:** Here, `#HALLUCINATION` is used in the course's broader *factual/completeness relative to reference* sense. No actual credential was fabricated; the recurring problem is **overconfident recommendation despite recognized evidence gaps**. Severity/frequency prioritization belongs to Step 3 and is not assigned here.

## Reconciliation

- Raw judge: 16 PASS + 4 FAIL = 20.
- Learner human override: 1 FAIL → PASS (T01).
- Final: 17 PASS + 3 FAIL = 20.
- Confirmed FAIL tags: 3 `#HALLUCINATION` + 0 other tags = 3.
