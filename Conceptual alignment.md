# D365FSCM for Winsol: phase II conceptual alignment document (Helios nv pilot)

> **Purpose**  
> Establish a shared understanding of scope, high‑level solutions, and effort/budget for Phase II of Winsol’s Dynamics 365 journey—focused on configure‑to‑order (CTO/MTO) manufacturing with CPQ/PLM orchestration, MRP adoption, WIP control, and cost transparency. This is a **conceptual alignment** document, not a detailed blueprint.

---

## 1. executive summary

**Context & ambition**  
Winsol is a configure‑to‑order manufacturer in the construction sector (doors, windows, pergolas, screens, solar shading). Engineering and configuration are driven by **external CPQ** and **PLM**, with D365 FSCM as the operational and financial backbone. Finance and procurement are already live in D365; Phase II focuses on **production, planning (MRP), costing, and WIP**—piloted at **Helios nv (Aalter)** and reusable for other legal entities.

**Why Phase II matters**

- **Cost transparency & margin visibility** per order/config (today fragmented; manual financial dimensions; limited post‑calcs).
- **WIP valuation & control**, reducing month‑end stress (current WIP ≈ €500k, limited stage insight).
- **MRP adoption for materials**, bringing end‑to‑end supply visibility; lightweight approach to capacity (handled outside D365).
- **Procurement for MTO purchases with late price determination**, enabling three‑way match and reliable accruals.
- **Data orchestration**: CPQ→PLM→D365 with readiness gating to prevent incomplete orders from polluting plans.

**Scope in one line**  
Orchestrate CTO flows across CPQ/PLM/D365/MES, enable MRP for materials, integrate MES actuals (time, materials, output/scrap), implement standard costing with post‑calculation, and govern WIP—all with a **fit‑to‑standard** mindset.

**Budget & timeline (conceptual)**

- **External consulting**: \~€600k
- **Internal effort**: \~€600k
- **Target go‑live window**: September (seasonality‑aware), pilot Helios first, subsequent roll‑outs with minor adjustments.

---

## 2. understanding Winsol’s configure‑to‑order business

- **CTO at scale**: High variability (colors, sizes, glass types, motors) but **standardized execution** (route templates; repeatable operations).
- **System roles**:
  - **CPQ**: quotation, configuration, pricing, order confirmation.
  - **PLM**: creates **unique MTO item variants + order‑specific BOM & route**.
  - **D365**: planning (materials), production control, procurement, costing, WIP, financials.
  - **MES (external)**: records actuals (operation time, materials, outputs/scrap) and integrates to D365 (no backflushing in D365).
- **48‑hour cooling‑off** after customer order before earliest production start.
- **No formal ECM during fulfillment (today)**; exceptions (ETO‑like) can occur but are to be minimized.
- **Allocation by design**: unique configuration/variant per SO line → no need for reservation; pegging maintained via planning‑relevant dimension(s).

---

## 3. current challenges and improvement goals

**Cost transparency**

- Today: margin uncertainty at order/config level; manual financial dimensions and fragmented postings.
- Target: **standard cost per configuration**, consistent post‑calculation with **variance analysis**; visibility at **SO line** and **aggregate (project/site via BI)**.

**WIP control**

- Today: large WIP (\~€500k) with limited stage insight; month‑end pressure.
- Target: configurable **WIP by stage** (materials, labor, subcontracting), clean month‑end with clear cut‑off playbook.

**Planning & visibility**

- Today: no MRP in legacy AS/400; limited foresight.
- Target: **MRP for materials** in D365, capacity balancing/scheduling in external tool; **readiness gating** ensures only complete orders are planned.

**Procure‑to‑pay for MTO**

- Today: MTO purchased items (e.g., glass) often priced after supplier configuration; three‑way match difficult.
- Target: introduce a **“CPQ for purchase”** concept (options below) to secure specification + price and achieve reliable matching.

**Quality & rework**

- Today: rework affects schedule and cost but limited structured insight.
- Target: define rework handling (separate operation vs scrap+extra time) during blueprint for transparency and throughput control.

---

## 4. end‑to‑end MTO process concept

### 4.1 order intake & orchestration (CPQ → PLM → D365)

- **Ownership**: CPQ (quote & confirm), PLM (product definition), D365 (execution & finance).
- **Flow (happy path)**
  1. CPQ confirms order.
  2. PLM generates **unique item variant** + **order‑specific BOM/route**.
  3. D365 receives master data + sales order line(s).
  4. External validation framework runs completeness checks and writes back a **readiness status** to D365.
  5. **Lifecycle state** on item/variant controls inclusion in **MRP**.
- **Design principle**: D365 **consumes completeness**, does not create it.

### 4.2 product definition & readiness gating

- **Always PLM‑provided** **BOM and route** for MTO lines (no fallback to route templates in D365 for MTO).
- **Readiness**: external validation controls whether item/variant is **included in planning** (via lifecycle state); status replicated to SO line for visibility.
- **No phantoms** needed for MES simplification in current concept.

### 4.3 planning & material explosion (D365 MRP)

- **Materials only**: MRP used for supply visibility and procurement triggers.
- **Capacity**: default operation times in D365 for lead‑time realism; **balancing & detailed scheduling external** (with optional bulk updates of planned/scheduled dates back to D365).
- **Pegging model**: planning‑relevant dimension (e.g., **configuration**) + optional inventory marking (not required given allocation by design).
- **Control**: coverage group configuration aligned with MTO behavior (single‑order explosion, no reuse).

### 4.4 production execution & MES

- **MES (external)** posts **all actuals**: operation time, material consumption, output, scrap.
- **D365** receives actuals for financial postings and order status updates; **no backflushing** in D365.
- **Rework**: to be decided in blueprint—separate operations vs scrap+extra time (impacts reporting and costing clarity).

### 4.5 procurement for MTO components (late price determination)

- **Challenge**: items like glass/vents configured at supplier; price known after supplier config.
- **Solution options (to be evaluated in blueprint)**:
  1. **Supplier configuration interface**: supplier system returns attributes + price to D365 (best automation, requires supplier commitment).
  2. **Internal purchasing configurator (Power App)**: purchasing specifies a structured spec; supplier confirms via **EDI/Peppol** with final price.
  3. **Pricing tolerance policy**: receive without price; later price update with **automatic price variance** postings + approval workflow (simplest to start; least proactive).
- **Goal**: **reliable 3‑way match** and accurate accruals for MTO purchases.

### 4.6 financial posting, WIP & costing

- **Manufactured MTO items**: **standard cost** per configuration + **post‑calculation variances**.
- **Purchased items**: **FIFO**.
- **WIP**: aim for **stage‑level** (materials, labor, subcontracting) if business endorses; otherwise single WIP per order (simpler, less insight).
- **Margin views**:
  - **SO line level** (linked to production order)
  - Aggregated perspectives via BI (e.g., project/site using existing **order reference** dimension—ideally defaulted rather than manual).

---

## 5. high‑level solution design (mapped to Microsoft business process catalog)

> We align with the Microsoft end‑to‑end processes where relevant—without forcing theory over Winsol’s architecture.

### 5.1 plan to produce (core)

- **In scope**: material requirements planning, pegging, production orders, MES actuals integration.
- **Handled externally**: finite capacity scheduling and detailed dispatching (with bulk date feedback to D365).

### 5.2 order to cash (ERP touchpoints only)

- **In scope**: receipt of confirmed orders from CPQ/PLM, readiness gating, production costing, invoicing.
- **Handled externally**: quotations and sales configuration (CPQ is lead).

### 5.3 acquire to dispose (procure‑to‑pay focus)

- **In scope**: purchase requisitions/orders for MTO components, receipt, invoice matching, price variances.
- **Extensions**: “CPQ for purchase” concept (interface, Power App, and/or policy‑based variance handling).

### 5.4 record to report

- **In scope**: WIP valuation (preferred by stage), post‑calculation, variances, month‑end playbook.
- **Objective**: reduce manual effort, increase reliability and speed at period close.

> Each subsection will be elaborated in blueprint with detailed parameters, entities, and integration contracts where needed.

---

## 6. integration landscape & responsibilities

**Principles**

- Clear **system of record** per domain.
- **Readiness gates** prevent incomplete data from flowing downstream.
- **Idempotent, traceable interfaces** with functional status visible in D365.

**Roles**

- **CPQ**: master of sales configuration, options, and pricing; sends confirmed orders.
- **PLM**: master of item variants, MTO BOMs & routes.
- **MES**: master of execution actuals (time, material, scrap, output).
- **D365**: master of planning (materials), production orders, procurement, inventory, costing, WIP, and all financial postings.

**Key interfaces**

- CPQ → D365: confirmed sales orders (or via PLM orchestrator).
- PLM → D365: items/variants, BOMs, routes (complete for MTO).
- MES → D365: operational actuals.
- D365 → MES (optional): planned dates/quantities; **no backflushing**.

---

## 7. scope statement (in / out / later)

**In scope (Phase II)**

- Production control (discrete), plan‑to‑produce (materials MRP), integration with MES actuals.
- Procurement enhancements for MTO purchases (three solution options to assess).
- Costing model (standard cost for manufactured MTO; FIFO for purchases), post‑calculation, variance analysis.
- WIP valuation (target: by stage).
- Orchestration & readiness gating using lifecycle states + external validation write‑back.
- Limited WHS (as‑is + targeted improvements aligned with manufacturing flows).

**Explicitly out of scope (this phase)**

- Project Operations; CRM; advanced APS (handled outside D365); product configurator inside D365; full shop floor execution in D365; broad Power BI program (beyond targeted reporting).

**Future evolution (later phases)**

- CRM for opportunity‑to‑order integration with CPQ.
- Advanced scheduling/APS integration deepening.
- Purchasing configurator maturation and supplier adoption (EDI/Peppol confirmations).

---

## 8. implementation approach and rollout

- **Phased per legal entity** with **Helios nv** as pilot; reusable template for other companies.
- **Fit‑to‑standard first**; customizations only if **cross‑entity reusable** or **high ROI**.
- **Blueprint** will decide: rework handling model, WIP staging level, purchase pricing solution option(s), quotation/confirmation handling (CPQ vs D365), month‑end cut‑off policy.
- **Change management**: focused enablement for planners (MRP usage), buyers (MTO purchase practices), finance (post‑calc & WIP playbook), production leads (MES posting discipline).

---

## 9. high‑level effort, budget, and timeline

> **Budget envelope** provided by Winsol is used as the planning baseline; detailed estimates will be validated after blueprint.

**Budget (conceptual ranges)**

- **External consulting**: \~€600k
  - Core D365 (SCM/Production/Planning): 25–30%
  - Integrations (CPQ/PLM/MES + readiness gating): 30–35%
  - Procurement enhancements (“CPQ for purchase” options exploration & minimal viable rollout): 10–15%
  - Costing/WIP & post‑calculation: 10–15%
  - Data migration (open transactions), testing, and training: 10–15%
  - PMO & change: 5–10%
- **Internal effort**: \~€600k
  - Process ownership, data preparation, UAT, cut‑over support, MES and supplier collaboration.

**Timeline toward September go‑live (illustrative)**

- **Blueprint & architecture**: 6–8 weeks
- **Build & integrations**: 12–16 weeks
- **Validation (SIT/UAT) & training**: 8–10 weeks
- **Cut‑over & go‑live prep**: 2–3 weeks

> Overlaps expected; a detailed plan will be produced post‑blueprint. Buffer for seasonal constraints included.

**Key assumptions**

- PLM delivers **complete BOMs & routes** for MTO lines.
- MES posts **all actuals**; D365 performs no backflushing.
- CPQ remains lead for **quotes/config/pricing**; D365 receives confirmed orders.
- Lifecycle state/readiness gating is enforceable across systems.
- Supplier and/or internal capabilities exist to realize a minimum viable **purchasing configuration** approach.

---

## 10. risks, dependencies, and mitigations

| Area                 | Risk / dependency                                   | Mitigation                                                                                       |
| -------------------- | --------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| Product definition   | Incomplete or late BOM/route from PLM               | Readiness gating via lifecycle state; integration monitoring; exception SLAs                     |
| MRP adoption         | Cultural shift for planners                         | Focused training; limited scope (materials only); clear exception handling                       |
| MTO purchase pricing | Supplier cooperation for configuration/price return | Stage‑gated approach: start with policy‑based variance + workflow; evolve to interface/Power App |
| MES integration      | Accuracy/timeliness of actuals                      | Early interface design; integrated test cycles with real scenarios; posting discipline           |
| WIP by stage         | Complexity of accounting model                      | Validate with finance during blueprint; fall back to single WIP if needed                        |
| Month‑end            | Cut‑off policies unclear                            | Define playbook in blueprint; simple, repeatable procedures                                      |
| Roll‑out reusability | Helios specifics vs group                           | Template governance; design for reuse from the start                                             |

---

## 11. open decisions to be taken in blueprint

1. **Quotations & confirmations**: fully CPQ vs partial D365 involvement.
2. **Rework handling**: separate routing operations vs scrap + extra time.
3. **WIP valuation granularity**: by stage vs single WIP account.
4. **Month‑end policy**: continuous vs defined cut‑off windows.
5. **Purchasing configuration approach**: supplier interface vs internal Power App vs variance policy (or a hybrid roadmap).
6. **Bulk date updates**: mechanism and frequency for external scheduling feedback to D365.
7. **Financial dimension defaults**: automate “order reference” defaults (pegging‑aware) to remove manual effort.

---

## 12. conclusion

This Phase II design aligns tightly with **how Winsol works**: configuration and engineering owned by CPQ/PLM, manufacturing and finance governed by D365, and execution actuals provided by MES. The approach is **fit‑to‑standard**, **integration‑first**, and **reusable** across legal entities. It directly addresses the highest‑value outcomes: **order‑level margin**, **WIP control**, **MRP‑driven material visibility**, and **three‑way match reliability** for MTO purchases.

With your go‑ahead, the next step is to schedule the **blueprint workshops**, using the open decision list as the agenda backbone.

---

### appendix (optional, if you want me to add visuals)

If you’d like, I can append 1–2 clean diagrams:

- **Orchestration swimlane** (CPQ→PLM→D365→MES with readiness gates)
- **Cost & WIP posting model** (manufactured vs purchased flows)
