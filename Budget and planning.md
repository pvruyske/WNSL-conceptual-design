# D365 FSCM Phase II — Budget & Delivery Approach
## Winsol (Helios nv pilot)

| | |
|---|---|
| **Document status** | Draft |
| **Version** | 0.1 |
| **Date** | March 12, 2026 |
| **Authors** | |
| **Reviewers** | IT Manager, Financial Controller |
| **Customer** | Winsol NV — Helios nv (pilot legal entity) |

> **Purpose** — Provide Winsol management with a structured view of the external consulting effort and the project delivery timeline for Phase II of the D365 FSCM implementation. Budget is expressed in consulting days; the indicative day rate is stated separately. Internal Winsol effort is not quantified in this document and is the responsibility of Winsol to plan.
>
> **Companion document** — [D365 FSCM Conceptual Design (Conceptual alignment.md)](Conceptual%20alignment.md) — contains scope, solution design, design principles, and the Open Decisions Log.

---

## 1. Delivery framework — PROMAR

This project follows the **PROMAR project life cycle** — delaware's standard structured delivery framework. PROMAR organizes a project into five delivery stages, each separated by **quality gates (QG)** that ensure formal closure, stakeholder sign-off, and controlled handover before proceeding.

| PROMAR stage | Purpose | Key outputs |
|---|---|---|
| **Discover** | Pre-sales alignment on objectives, scope, and value | Conceptual design, SOW, contracts |
| **Initiate** | Team mobilization, governance, workshop planning | Governance model, project plan, risk register |
| **Explore** | Process discovery; blueprint and fit-gap analysis | BPML, blueprint documents per E2E, realization backlog |
| **Execute** | Sprint-based build, integration, testing | Configured D365, integration builds, SIT and UAT reports |
| **Deploy** | Cut-over, go live, hypercare | Production system live, hypercare concluded |
| **Run** | Support handover, project closure | Lessons learned, project closure document |

Quality gates are formal validation checkpoints and serve as billing milestones for fixed-price contracts.

---

## 2. Current project stage

As of March 2026, the project is in the **Explore — Conceptual Design (CCD)** phase. The Conceptual Alignment document captures the outcomes of this phase: scope boundaries, design principles, high-level solution design, and all open decisions requiring stakeholder sign-off.

The next stage is **Explore — Blueprint (F2S/BBP)**, which resolves all open decisions, produces detailed design per E2E process, defines integration contracts, establishes the data migration strategy, and creates the realization backlog. Blueprint is contracted and governed separately.

---

## 3. Blueprint phase

### 3.1 Scope

The blueprint phase covers the following workstreams:

- **Project initiation (PROMAR Initiate)**: governance setup, ways of working, acceptance criteria, workshop schedule, risk register.
- **Fit-to-Standard workshops per E2E process**: process discovery, fit/gap analysis, and blueprint documentation for each in-scope business process area.
- **Open decisions resolution**: all decisions in the Open Decisions Log are confirmed or explicitly descoped with documented rationale.
- **Integration architecture blueprint**: interface contracts (message format, frequency, error handling, retry), middleware/framework selection (D-ITF-01), readiness gating design.
- **Data migration strategy**: migration scope per data category, cutover approach, data quality requirements and ownership.
- **Technical architecture**: environment strategy, security model, financial dimensions confirmation, D365 configuration standards.
- **Blueprint document package**: blueprint document per E2E, consolidated BPML, updated interface catalog, updated Open Decisions Log.
- **Realization backlog**: WBS and sprint backlog prepared and reviewed; sprint plan confirmed as input to the realization contract.

### 3.2 Budget

> **Reference day rate**: €1,500/day excl. VAT (indicative — final pricing per agreed rate card). Travel and accommodation costs are not included and are invoiced separately at cost.

| Workstream | Days | Notes |
|---|:---:|---|
| Project management & initiation (PROMAR Initiate + PMO setup) | 8 | Governance, ways of working, workshop planning, project board |
| Design to retire (PLM / product master blueprint) | 6 | Item master, BOM/route, lifecycle states, ECM evaluation (D-DTR-01 to D-DTR-04) |
| Forecast to plan (MRP / Planning Optimization blueprint) | 6 | Coverage groups, MTO pegging, ALU strategy, scheduler interface (D-FTP-01 to D-FTP-04) |
| Order to cash | 4 | CPQ integration design, cooling-off mechanism, dimension defaulting (D-OTC-01 to D-OTC-03) |
| Source to pay (procurement enhancements) | 4 | MTO pricing option decision, purchase agreements, accrual policy (D-STP-01 to D-STP-03) |
| Plan to produce (production control / costing / WIP) | 12 | Core manufacturing blueprint; highest decision density (D-PTP-01 to D-PTP-06) |
| Inventory to deliver (WMS blueprint) | 5 | WMS process scope, location directives, quality and transport TBDs (D-ITD-01 to D-ITD-04) |
| Record to report (GL / costing / month-end) | 5 | COA extensions, WIP model, month-end playbook (D-RTR-01 to D-RTR-03) |
| Integration architecture blueprint | 12 | Interface contracts I-01 to I-07, framework decision (D-ITF-01), readiness gating design |
| Data migration strategy | 4 | Migration scope, cutover approach, data quality and ownership |
| Realization backlog & blueprint quality gate | 4 | WBS preparation, sprint planning input, quality gate documentation and sign-off |
| **Total** | **70** | **at €1,500/day ≈ €105,000** |

### 3.3 Quality gate criteria

The blueprint phase concludes with a formal quality gate before realization commences. The following criteria must be satisfied:

- All Open Decisions Log items are confirmed or explicitly descoped with documented rationale.
- Blueprint document package reviewed and signed off by process owners for each E2E.
- Interface contracts validated by Winsol IT and the relevant external system owners (PLM, MES, CPQ vendors).
- Realization backlog reviewed, prioritized, and sprint planning completed.
- Updated consulting day estimate and timeline for realization confirmed and approved.

---

## 4. Full project budget — consulting day matrix

The table below presents the **indicative** consulting day estimate for the full project from blueprint through project close. This estimate will be validated and refined at the blueprint quality gate, at which point the realization contract (fixed-price or time-and-material) will be agreed.

> **Basis**: reference day rate €1,500/day (indicative). Blueprint days represent confirmed scope. Realization through Deploy days are subject to blueprint outcomes and will be updated after blueprint QG.
>
> **Note on integrations**: the integration estimate assumes the delaware interface framework is selected (D-ITF-01 Option 2). Selecting Option 1 (retain 9altitudes ISV) or Option 3 (custom + standard APIs) may shift this estimate; the impact will be assessed during blueprint.

| Workstream | Blueprint | Realization | SIT | BRT / UAT | Deploy & Hypercare | **Total days** | **Indicative €** |
|---|:---:|:---:|:---:|:---:|:---:|:---:|---:|
| Project management & governance | 8 | 18 | 4 | 4 | 4 | **38** | €57,000 |
| Design to retire (PLM / product master) | 6 | 12 | 3 | 3 | 1 | **25** | €37,500 |
| Forecast to plan (MRP / Planning Optimization) | 6 | 15 | 4 | 4 | 1 | **30** | €45,000 |
| Order to cash | 4 | 8 | 2 | 3 | 1 | **18** | €27,000 |
| Source to pay (procurement enhancements) | 4 | 12 | 3 | 4 | 1 | **24** | €36,000 |
| Plan to produce (production control / costing / WIP) | 12 | 30 | 6 | 8 | 3 | **59** | €88,500 |
| Inventory to deliver (WMS) | 5 | 12 | 4 | 4 | 2 | **27** | €40,500 |
| Record to report (GL / costing / month-end) | 5 | 12 | 4 | 4 | 1 | **26** | €39,000 |
| Integrations (CPQ / PLM / MES / scheduler) | 12 | 45 | 12 | 8 | 5 | **82** | €123,000 |
| Data migration | 4 | 12 | 4 | 4 | 5 | **29** | €43,500 |
| Testing & training coordination | — | 8 | 8 | 12 | 4 | **32** | €48,000 |
| **Total days** | **66** | **184** | **54** | **58** | **28** | **390** | |
| **Indicative total (€)** | **€99,000** | **€276,000** | **€81,000** | **€87,000** | **€42,000** | | **€585,000** |

### 4.1 Budget summary by phase

| Phase | Days | Indicative € | Contract status |
|---|:---:|---:|---|
| Blueprint (F2S/BBP) | 70 | €105,000 | Separate contract — confirmed scope |
| Realization through Deploy (Execute + Deploy) | 320 | €480,000 | Indicative — to be confirmed post-blueprint QG |
| **Total** | **390** | **€585,000** | |

> The indicative total of €585,000 is within the planning envelope of approximately €600,000 for external consulting. The delta provides a small contingency buffer; formal contingency provisions will be agreed in the realization contract.

### 4.2 Budget assumptions

The estimates above are based on the following assumptions. Deviations from these assumptions will be flagged as scope/budget change requests.

1. Blueprint is completed on schedule and all open decisions are closed before realization commences.
2. PLM delivers complete item variants, BOMs, and routes before go-live; no D365-side BOM authoring is required.
3. MES posts all actuals via integration; D365 performs no backflushing.
4. CPQ remains the lead for quotes and configuration; D365 receives confirmed orders only.
5. The delaware interface framework (D-ITF-01 Option 2) is selected; deviation to Option 1 or 3 will be assessed for budget and timeline impact at blueprint QG.
6. Helios nv configuration complexity is representative of other Winsol legal entities for rollout purposes.
7. No major D365 platform upgrades or Microsoft release disruptions occur during the build window.
8. External system owners (PLM vendor, MES vendor, CPQ teams) provide subject-matter experts for integration workshops during blueprint and are available for SIT.
9. Internal Winsol resources (process owners, IT lead, data team) are available per the internal effort plan to be agreed separately.

---

## 5. Project timeline

### 5.1 Phase overview

The project targets **go-live at Helios nv in September 2027**. The timeline below is based on a sequential PROMAR delivery with quality gates between each stage. Phases may partially overlap; a detailed resource-loaded plan will be produced at the blueprint quality gate.

| # | PROMAR stage | Phase | Start | End | Duration |
|---|---|---|---|---|---|
| 1 | Explore | Blueprint (F2S/BBP) | April 2026 | June 2026 | 10 weeks |
| — | — | *Blueprint quality gate* | June 2026 | | |
| 2 | Execute | Realization — S1–S2: Foundation (environment, finance extensions, WMS baseline, dimension defaulting) | July 2026 | August 2026 | 8 weeks |
| 3 | Execute | Realization — S3–S5: Plan to produce, MRP, costing, WIP | September 2026 | November 2026 | 10 weeks |
| 4 | Execute | Realization — S6–S7: Integrations (CPQ / PLM / MES / scheduler), procurement enhancements | November 2026 | January 2027 | 8 weeks |
| — | — | *XFIT (cross-functional integration test) complete* | January 2027 | | |
| 5 | Execute | SIT (System Integration Testing) | February 2027 | March 2027 | 6 weeks |
| — | — | *SIT quality gate* | March 2027 | | |
| 6 | Execute | BRT / UAT (Business Readiness Testing) | April 2027 | May 2027 | 8 weeks |
| — | — | *UAT sign-off quality gate* | May 2027 | | |
| 7 | Deploy | Final Preparation (cut-over rehearsals, data migration, end-user training completion) | June 2027 | August 2027 | 10 weeks |
| — | — | *Go / No-Go decision* | August 2027 | | |
| 8 | Deploy | **Go Live — Helios nv** | **September 2027** | | |
| 9 | Deploy | Hypercare | September 2027 | October 2027 | 4 weeks |
| 10 | Run | Project closing | November 2027 | November 2027 | 2 weeks |

### 5.2 Realization sprint breakdown

Realization follows a sprint-based iterative approach. Each sprint of 4–6 weeks includes detailed design sessions, configuration, unit testing, and a sprint review (FIT). The breakdown below is indicative; it will be revised and formalized at the blueprint quality gate.

| Sprint | Focus | Duration |
|---|---|---|
| **S1–S2** | Foundation: environment setup, legal entity configuration, GL extensions (WIP, variance, COGS accounts), financial dimension defaulting logic, WMS baseline extension (production and sales picking) | Weeks 1–8 |
| **S3** | Plan to produce: production parameters, resource and work center setup, route configuration, standard costing model, cost categories, overhead absorption | Weeks 9–13 |
| **S4** | Forecast to plan: MRP (Planning Optimization) extension — coverage groups for MTO, pegging via configuration dimension, min/max items, ALU strategy (pending D-FTP-04) | Weeks 14–17 |
| **S5** | WIP accounting model, post-calculation variances, month-end playbook, costing close process | Weeks 18–20 |
| **S6** | Integrations build: CPQ → D365 (I-01), PLM → D365 (I-02), external validation → D365 readiness gating (I-03); lifecycle state controls | Weeks 21–25 |
| **S7** | Integrations build: D365 → MES (I-04), MES → D365 actuals (I-05), scheduler → D365 (I-06), supplier confirmation (I-07); MTO purchase pricing (Source to pay — Option A/B/C) | Weeks 26–28 |

### 5.3 Key milestones

| Milestone | Target date |
|---|---|
| Blueprint kick-off | April 2026 |
| Blueprint quality gate (all decisions closed, signed off) | June 2026 |
| Realization start | July 2026 |
| XFIT (cross-functional integration test) complete | January 2027 |
| SIT start | February 2027 |
| SIT quality gate | March 2027 |
| BRT/UAT start | April 2027 |
| UAT sign-off | May 2027 |
| Go/No-Go decision | August 2027 |
| **Go Live — Helios nv** | **September 2027** |
| Hypercare complete | October 2027 |
| Project closed | November 2027 |

### 5.4 Seasonality note

Winsol's production activity peaks in spring and early summer. The timeline is designed to respect this:

- **Blueprint workshops (April–June 2026)** are planned ahead of the seasonal production peak. Process owner availability for discovery sessions should be confirmed during initiation.
- **Go-live in September 2027** is positioned immediately after the summer peak period, giving operators time to stabilize before the next peak season.
- **BRT/UAT (April–May 2027)** overlaps with a busy operational period. Process owner availability during this phase is a scheduling risk that must be addressed in the resource plan.

---

## 6. Rollout after Helios pilot

Following Helios nv go-live, subsequent legal entity rollouts (WBL, ACT, WNV, IND, SFO, INT, GRP) are expected to require only:

- Legal entity-specific configuration (company accounts, legal entity settings, applicable tax rules).
- Data migration for the new entity.
- Targeted regression testing against the Helios template.

No redesign of core D365 configuration, integration interfaces, or the data model is anticipated for rollouts, provided the pilot template is clean. Budget and timeline for each rollout legal entity will be estimated separately after Helios go-live, as part of a Phase III engagement.

---

## Changelog

| Version | Date | Author | Description |
|---|---|---|---|
| 0.1 | March 12, 2026 | | Initial draft — blueprint budget, full project consulting day matrix (phase × workstream), PROMAR-based timeline through September 2027 go-live |
