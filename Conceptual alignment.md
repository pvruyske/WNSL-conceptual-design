# D365 FSCM Conceptual Design — Winsol (Helios nv pilot)

| | |
|---|---|
| **Document status** | Draft — Scope & Architecture |
| **Version** | 0.1 |
| **Date** | March 11, 2026 |
| **Authors** | |
| **Reviewers** | IT Manager, Financial Controller, Operations Manager |
| **Customer** | Winsol NV — Helios nv (pilot legal entity) |

> **Purpose** — Establish a shared understanding of scope, high-level solution design, design principles, and budget for Phase II of Winsol's Dynamics 365 FSCM journey. This document will evolve from the current *Scope & Architecture* stage toward a full *Blueprint* as the project progresses.
>
> **Audience** — IT manager, financial controller, and operations manager.
>
> **How to read this document** — Part I defines the project context and scope boundaries. Part II captures the global design principles that govern all subsequent design choices. Part III elaborates each in-scope end-to-end process. Parts IV and V cover architecture, budget, and delivery. Open decisions that require explicit stakeholder sign-off are collected in the Open Decisions Log (Section 19).

---

# Part I — Context & Scope

## 1. Company & project context

### 1.1 About Winsol

Winsol is a Belgian manufacturer in the construction and solar shading sector, producing doors, windows, pergolas, screens, and solar shading products. The business model is **configure-to-order (CTO)**: customers select from a high-variability product configurator (colors, dimensions, glass types, motors, accessories), but manufacturing execution follows repeatable, standardized route templates.

Key business characteristics relevant to this ERP implementation:

- **High SKU variability, standardized execution**: each customer order produces a unique item variant, but the production route and operations are repeatable across product families.
- **48-hour cooling-off period** between customer order confirmation and earliest production start.
- **Seasonal demand peaks**: go-live windows must respect peak production periods.
- **Multiple legal entities**: the Winsol group consists of several legal entities; this phase targets **Helios nv (Aalter)** as the pilot, with the design intended to be reusable across other entities.

### 1.2 Phase context

Phase I of the D365 FSCM implementation delivered the following capabilities for the group:

- Finance (general ledger, accounts payable, accounts receivable, cash management)
- Procurement (purchase orders, vendor management, three-way match)
- **D365 WMS app**: used for purchase order receipts and movement journals; the financial dimension *project* can be specified from within the WMS app to track component consumptions per customer project
- **MRP — min/max replenishment**: Planning Optimization is active for a limited set of standard items (fasteners, packaging materials, powder coatings), using minimum/maximum stock levels to drive purchase order suggestions

**Phase II** extends the implementation to cover:

- Production control (discrete manufacturing)
- Materials planning (MRP)
- Costing model (standard cost + post-calculation)
- WIP valuation and control
- Procurement enhancements for MTO-purchased items with late price determination
- WMS extension: automated work creation for production order picking and sales order picking, plus additional WMS processes to be defined during blueprint
- Integration with CPQ, PLM, and MES

### 1.3 Legal entities in scope

All Winsol group legal entities are already active in D365 for Finance and Procurement (Phase I). Phase II adds manufacturing scope, piloted at Helios nv.

| Legal entity | Location | D365 Phase I status | Role in Phase II |
|---|---|---|---|
| Helios nv (HLS) | Aalter, Belgium | Finance, Procurement, and WMS app live | Pilot — full Phase II manufacturing scope |
| All other group entities (WBL, ACT, WNV, IND, SFO, INT, GRP) | Belgium / France | Finance and Procurement live | Phase II manufacturing roll-out post-Helios pilot; template reuse expected |

---

## 2. Solution landscape

### 2.1 System-of-record map

Winsol operates a multi-system landscape. Each system has a clearly defined domain of ownership. D365 FSCM acts as the operational and financial backbone, but is not the system of record for configuration, product definition, or shop floor execution.

| Type | Owner domain | As-is system | To-be system | Role in Winsol's landscape |
|---|---|---|---|---|
| **CPQ** | Sales configuration, pricing | WinCal / WinsolCom / Chacal / Tekla | WinCal / WinsolCom / Chacal / Tekla *(no replacement planned)* | Quote & order confirmation; defines what the customer buys. Multiple tools serve different product lines: WinCal (awnings, shutters, garage doors), WinsolCom (windows & doors), Chacal (project quotes and windows/doors CTO), Tekla (balustrade projects). |
| **CTO / product definition** | Product definition, configure-to-order | AS/400 / XLS / Chacal *(custom CTO toolset)* | Evolved CTO platform *(to-be; system name TBD)* | Translates CPQ-confirmed orders into unique item variants, order-specific BOMs, and production instructions; pushes these to D365 |
| **ERP** | Planning, production control, procurement, inventory, costing, WIP, financials | AS/400 | D365 FSCM | Operational and financial backbone |
| **MES** | Shop floor execution | [*system name TBD*] | [*system name TBD*] | Records actuals: operation time, material consumption, output, scrap |
| **BI / Reporting** | Analytics and reporting | [*system name TBD*] | [*system name TBD*] | Cross-system reporting; financial dimensions strategy feeds this |

> **Note on "PLM" terminology** — Throughout this document, the label *PLM* is used as a shorthand for the to-be product definition and CTO layer. This does not imply adoption of a commercial PLM platform; it refers to the planned evolution of Winsol's existing custom CTO toolset (AS/400, XLS, Chacal) into an integrated system that delivers complete item variants, BOMs, and routes to D365. The chosen architecture and tooling for this layer will be confirmed during blueprint.

### 2.2 High-level architecture

> **[Architecture diagram placeholder]**
> Insert a swimlane or box-and-arrow diagram showing: CPQ → PLM → D365 (order intake, planning, costing) → MES (actuals back to D365), with readiness gating indicated. Source file: `attachments/Winsol conceptual alignment.drawio`.

**Key data flows (narrative)**

1. CPQ confirms customer order → sends confirmed sales order to D365 (directly or via PLM orchestrator).
2. PLM generates unique item variant + order-specific BOM and route → pushes to D365.
3. External validation framework runs completeness checks → writes back **readiness status** to D365 item/variant lifecycle state.
4. D365 MRP runs → explodes materials → creates planned purchase orders and production orders.
5. Production orders released to MES.
6. MES records actuals → posts back to D365 (operation time, material consumption, output, scrap).
7. D365 performs all financial postings (WIP, variances, COGS).

---

## 3. Project scope

### 3.1 Business process catalog scope

The table below maps all Microsoft Business Process Catalog (BPC) Level 1 and Level 2 processes against the project scope decision for Winsol Phase II. This is the authoritative scope boundary for this implementation.

**Legend**

| Value | Meaning |
|---|---|
| **In scope** | Will be implemented in the indicated master system |
| **Out of scope** | Not covered in this phase |
| **TBD** | Scope to be confirmed during blueprint |

| End to end | Process area | Scope | Master system |
|:---|:---|:---|:---|
| **Acquire to dispose** | Define asset strategy | Out of scope | |
| | Acquire assets | Out of scope | |
| | Manage active assets | Out of scope | |
| | Perform asset maintenance | Out of scope | |
| | Dispose of assets | Out of scope | |
| | Analyze assets | Out of scope | |
| **Case to resolution** | Establish a knowledge base | Out of scope | |
| | Define customer and employee service operations | Out of scope | |
| | Intake cases | Out of scope | |
| | Manage and work on cases | Out of scope | |
| | Analyze case performance | Out of scope | |
| **Concept to market** | Develop marketing strategy | Out of scope | |
| | Research and develop offerings | Out of scope | |
| | Manage service offerings | Out of scope | |
| | Prepare marketing campaigns | Out of scope | |
| | Manage marketing campaigns | Out of scope | |
| | Analyze marketing operations | Out of scope | |
| **Design to retire** | Develop product strategy | Out of scope | |
| | Introduce products | **In scope** | PLM |
| | Manage active products | **In scope** | PLM |
| | Retire products | **In scope** | PLM |
| | Analyze product performance | Out of scope | |
| **Forecast to plan** | Develop business strategy | TBD | |
| | Conduct sales and operations planning | **In scope** | ERP |
| | Execute sales and operations | **In scope** | ERP |
| | Conduct financial planning | TBD | |
| | Analyze business performance | Out of scope | |
| **Hire to retire** | Develop people strategy | Out of scope | |
| | Recruit and onboard talent | Out of scope | |
| | Manage workplace compliance | Out of scope | |
| | Manage performance and growth | Out of scope | |
| | Manage time and attendance | Out of scope | |
| | Manage compensation and benefits | Out of scope | |
| | Offboard talent | Out of scope | |
| | Analyze HR programs | Out of scope | |
| **Inventory to deliver** | Manage warehouse operations | **In scope** | ERP |
| | Maintain inventory levels | **In scope** | ERP |
| | Process inbound goods | **In scope** | ERP |
| | Process outbound goods | **In scope** | ERP |
| | Manage inventory quality | TBD | |
| | Manage freight and transportation | TBD | |
| | Analyze warehouse operations | **In scope** | ERP |
| **Order to cash** | Develop sales policies | Out of scope | |
| | Manage sales orders | **In scope** | ERP |
| | Manage accounts receivable | **In scope** | ERP |
| | Manage credit and collections | **In scope** | ERP |
| | Analyze sales performance | **In scope** | ERP |
| **Plan to produce** | Develop production strategies | **In scope** | ERP |
| | Plan production operations | **In scope** | ERP |
| | Run production operations | **In scope** | MES |
| | Control production quality | TBD | MES |
| | Analyze production operations | **In scope** | ERP |
| **Source to pay** | Develop procurement and sourcing strategy | **In scope** | ERP |
| | Manage supplier relationships | **In scope** | ERP |
| | Source and contract goods and services | **In scope** | ERP |
| | Procure goods and services | **In scope** | ERP |
| | Manage accounts payable | **In scope** | ERP |
| | Analyze procurement and sourcing | **In scope** | ERP |
| **Project to profit** | Develop project strategy | TBD | |
| | Manage project contracts | TBD | |
| | Plan projects | TBD | |
| | Manage project delivery | TBD | |
| | Manage project financials | TBD | |
| | Analyze project performance | TBD | |
| **Prospect to quote** | Manage customer relationships | TBD | |
| | Identify and qualify leads | TBD | |
| | Define sales strategy and policies | TBD | |
| | Pursue opportunities | TBD | |
| | Estimate and quote sales | TBD | |
| | Analyze sales | TBD | |
| **Record to report** | Define accounting policies | **In scope** | ERP |
| | Manage cash | **In scope** | ERP |
| | Manage budgets | **In scope** | ERP |
| | Record financial transactions | **In scope** | ERP |
| | Close financial periods | **In scope** | ERP |
| | Analyze financial performance | **In scope** | ERP |
| **Service to deliver** | Develop service strategy | Out of scope | |
| | Plan service work | Out of scope | |
| | Manage service work | Out of scope | |
| | Deliver services | Out of scope | |
| | Analyze service performance | Out of scope | |
| **Administer to operate** | Implement solutions | Out of scope | |
| | Define business continuity plan | Out of scope | |
| | Manage licensing and entitlements | Out of scope | |
| | Administer system features | Out of scope | |
| | Manage system access and security | Out of scope | |
| | Train users and increase adoption | Out of scope | |
| | Monitor systems, environments, and capacity | Out of scope | |
| | Manage background jobs | Out of scope | |
| | Manage notifications alerts | Out of scope | |
| | Uptake software releases | Out of scope | |
| | Manage data | Out of scope | |
| | Manage system compliance | Out of scope | |
| | Support systems | Out of scope | |

### 3.2 Explicitly out of scope (narrative)

The following items are explicitly excluded from Phase II. They are listed here to prevent scope creep and manage stakeholder expectations:

- **Project Operations**: no project-based costing or billing. Financial dimensions (e.g., WinsolSalesReference) are used for project-level visibility in BI.
- **CRM / Prospect to quote**: customer relationship management and opportunity tracking remain outside D365; CPQ is the lead system for quoting.
- **Product configurator inside D365**: all configuration logic resides in CPQ. D365 consumes confirmed, fully specified orders.
- **Advanced APS / detailed scheduling**: capacity planning and detailed finite scheduling are handled by an external tool, not D365.
- **Full advanced WMS**: the D365 WMS app is already live (Phase I) and is extended in Phase II. However, advanced WMS features such as license plate-based directed put-away at scale, advanced shipping notifications (ASN), and wave/load management beyond the manufacturing flow are out of scope unless specifically justified during blueprint.
- **Broad Power BI / analytics program**: targeted financial dimension reporting is in scope; a company-wide analytics program is not.

### 3.3 TBD items — scope to be confirmed in blueprint

The following process areas are marked TBD and require a decision during blueprint. They are captured in the Open Decisions Log (Section 19).

- **Forecast to plan — Develop business strategy / Conduct financial planning**: scope and depth of S&OP and financial planning processes.
- **Inventory to deliver — Manage inventory quality / Manage freight and transportation**: TBD based on requirements gathered in blueprint.
- **Plan to produce — Control production quality**: quality control model; may overlap with MES capabilities.
- **Project to profit**: full scope TBD. If included, this impacts the financial dimensions strategy and costing model.
- **Prospect to quote**: CRM scope TBD; depends on the CPQ integration roadmap.

---

# Part II — Design Principles

## 4. Global design principles

The following principles govern all design decisions in this implementation. They are established at this stage to prevent design drift and ensure consistency across process areas, integration interfaces, and legal entities.

### 4.1 Fit-to-standard first

D365 FSCM standard functionality is used as-is unless a deviation provides measurable, cross-entity business value that cannot be achieved through configuration. All customizations must be explicitly justified, approved, and documented. The threshold for accepting a customization is: **reusable across legal entities** and/or **high ROI relative to standard functionality change effort**.

### 4.2 Product model — PLM-owned variants

Item variants and product masters for MTO items are **created and owned by PLM**. D365 receives item masters as released products via integration. There is no product configurator inside D365. For MTO lines:

- Each configured order line results in a **unique item variant** in PLM, which is then pushed to D365.
- BOMs and routes for MTO items are **always PLM-provided**; there is no fallback to generic route templates in D365 for MTO lines.
- Standard (non-configured) items may have D365-native product masters.

> **Decision required**: confirm whether phantom items are used in D365 BOM structures for MES simplification. Current position: phantoms not required. (See Open Decisions Log D-DTR-01.)

### 4.3 Planning philosophy — materials in D365, capacity outside

MRP in D365 is used exclusively for **material supply planning** (purchase order and production order suggestions). Capacity planning and detailed scheduling are performed in an **external scheduling tool**, which may write planned/scheduled dates back to D365.

- Coverage groups are configured for MTO behavior (single-order explosion, no cross-order material reuse).
- Pegging is maintained via a planning-relevant **configuration dimension**.
- Capacity is represented in D365 only at the level needed for realistic lead-time calculation (default operation times on route groups/resources).

### 4.4 Costing model

- **Manufactured MTO items**: standard cost per configuration, calculated from PLM-provided BOM and route. Post-calculation produces **variance analysis** per production order.
- **Purchased items**: **FIFO** costing; MTO-purchased items follow the same FIFO policy.
- Standard cost updates are triggered by PLM master data events (new or revised BOM/route).
- Margin visibility is required at **sales order line level** and at aggregate level (via BI using financial dimensions).

### 4.5 WIP valuation

The target design provides **WIP visibility by stage** (materials issued, labor posted, subcontracting). A simpler single-WIP-account model is the fallback if the business does not endorse the staging complexity during blueprint.

> **Decision required**: WIP granularity — by stage vs. single WIP account. (See Open Decisions Log D-PTP-01.)

### 4.6 Financial dimensions strategy

Financial dimensions are used to provide business-level reporting visibility without requiring Project Operations. Key dimensions:

- **WinsolSalesReference** (financial dimension already established in Phase I, linked to the sales order and flowing through to production order and financial postings): enables margin tracking per configured order; must be **defaulted automatically** via integration or D365 logic, not entered manually. Automated defaulting to production and costing flows is a Phase II build requirement.
- Additional dimensions (e.g., site, product family) to be confirmed in blueprint.

Manual entry of financial dimensions is to be minimized; automation of defaults is a design requirement.

### 4.7 Integration philosophy

- **System of record**: each domain has one authoritative source (defined in Section 2.1). No data is duplicated across ownership boundaries without a clear sync contract.
- **Readiness gating**: downstream systems (D365 MRP, production) do not process incomplete records. An external validation framework writes a **readiness status** back to D365 item/variant lifecycle states. D365 consumes completeness; it does not create it.
- **Idempotent interfaces**: all integration messages are designed to be safely re-processed without creating duplicates or inconsistencies.
- **Traceability**: integration errors and status are visible in D365 as functional status indicators, not only as technical logs.
- **No backflushing in D365**: MES is the system of record for execution actuals; D365 does not backflush materials or time.

### 4.8 Rollout model — pilot first, template second

Helios nv is the pilot legal entity. The design, configuration, and integrations are built with **structural reusability** in mind. Company-specific parameters (chart of accounts, legal entity settings, local tax rules) are isolated from the reusable template. Subsequent legal entity rollouts are expected to require only configuration adjustments, not redesign.

---

# Part III — End-to-End Process Design

> This part contains one section per in-scope or TBD end-to-end process. Each section follows a consistent structure:
> - **Winsol context & challenges**
> - **Process scope** (level-2 process areas for this E2E)
> - **Proposed solution outline**
> - **Key design decisions**
> - **Integration touchpoints**
>
> Sections for TBD end-to-end processes contain placeholder content and will be elaborated during blueprint.

---

## 5. Design to retire

### 5.1 Winsol context & challenges

Product definition for Winsol's CTO portfolio is entirely driven by PLM. D365's role in this end-to-end is to **receive and maintain** item masters, BOMs, and routes — not to author them. The challenge lies in interface reliability, data completeness gating, and lifecycle management of the large number of unique MTO item variants generated per year.

Key pain points:

- Incomplete or late product master data from PLM causes planning errors in D365.
- No formal engineering change management (ECM) process during active fulfillment; ad-hoc exceptions create noise in D365.
- Item lifecycle management is not enforced today in D365, which risks orphaned variants polluting plans.

> **Note on D365 Engineering Change Management (ECM) module** — D365 FSCM includes an ECM module with features such as change orders, impact analysis, readiness policies, and product lifecycle state workflows. Full adoption of ECM as a change management process is **unlikely to be appropriate** given that PLM is the system of record for product definition: running parallel change governance in both PLM and D365 creates conflicting ownership and integration complexity. However, two specific ECM capabilities are worth evaluating during blueprint: (1) **readiness policies** — ECM's native readiness check framework could serve as the D365-side implementation of the readiness gate described in section 4.7, potentially replacing a custom write-back integration; and (2) **impact analysis** — ECM can surface open production orders, purchase orders, and sales orders affected by a BOM or route update pushed from PLM, which is operationally valuable in a high-variant CTO environment. See decision D-DTR-04.

### 5.2 Process scope

| Process area | Scope | Master system | Notes |
|---|---|---|---|
| Develop product strategy | Out of scope | PLM | PLM-internal; no D365 involvement |
| Introduce products | **In scope** | PLM | PLM pushes item variants, BOMs, routes to D365 |
| Manage active products | **In scope** | PLM | Product master updates and lifecycle state management |
| Retire products | **In scope** | PLM | Lifecycle state controls exclusion from planning |
| Analyze product performance | Out of scope | | BI / downstream reporting |

### 5.3 Proposed solution outline

- Item variants and released products are created in D365 via integration with PLM; no manual creation of MTO items in D365.
- **Item lifecycle states** in D365 are used to control MRP inclusion. An item is planned only when its lifecycle state indicates readiness, as confirmed by an external validation step or — pending blueprint evaluation — via ECM readiness policies natively in D365.
- BOM and route versions in D365 are always linked to a PLM-sourced record; version history is traceable.
- For standard (non-MTO) items, D365-native product management applies.
- No product configurator in D365.
- The D365 ECM **change order process** is not adopted: PLM governs all product definition changes. ECM is not used to author or approve changes in D365.

### 5.4 Key design decisions

| # | Decision | Status |
|---|---|---|
| D-DTR-01 | Phantom item usage in MTO BOMs | Open — to be confirmed in blueprint |
| D-DTR-02 | ECM process for in-flight production order changes | Open — exceptions to be handled via a defined deviation process |
| D-DTR-03 | Item numbering convention: PLM ID vs. D365-native | Open |
| D-DTR-04 | Selective use of D365 ECM module: readiness policies and/or impact analysis — without adopting the full change order process | Open — to be evaluated in blueprint |

### 5.5 Integration touchpoints

| Interface | Direction | Trigger | Data |
|---|---|---|---|
| PLM → D365 | Inbound | PLM item/variant creation or update | Item master, released product, BOM, route, lifecycle state |
| External validation → D365 | Inbound | Completeness check completion | Readiness status written to item lifecycle state |

---

## 6. Forecast to plan

### 6.1 Winsol context & challenges

D365 Planning Optimization is already active in a limited capacity from Phase I: minimum/maximum stock level rules drive purchase order suggestions for a small set of standard replenishment items (fasteners, packaging materials, powder coatings). This scope is deliberately narrow and does not cover MTO-driven demand.

For the broader material planning landscape, planning remains largely manual or handled outside D365, resulting in:

- Limited forward visibility on material requirements for configured MTO items.
- Reactive purchasing, especially for long-lead MTO-purchased items (e.g., glass).
- No systematic link between customer order intake and material demand in D365.
- Aluminum profiles (ALU) are replenished via a separate XLS-based forecast entirely outside D365 MRP; whether to incorporate ALU into D365 MRP in Phase II is a blueprint decision (see D-FTP-04).

Phase II extends MRP to **BOM-exploded, production-order-driven material requirements planning**, linking confirmed sales order demand directly to material supply. Capacity planning remains outside D365.

### 6.2 Process scope

| Process area | Scope | Master system | Notes |
|---|---|---|---|
| Develop business strategy | TBD | | S&OP process depth TBD during blueprint |
| Conduct sales and operations planning | **In scope** | ERP | Demand and supply balancing in D365 |
| Execute sales and operations | **In scope** | ERP | MRP execution, planned order management |
| Conduct financial planning | TBD | | Budgeting/forecasting scope TBD |
| Analyze business performance | Out of scope | | |

### 6.3 Proposed solution outline

- **MRP (Planning Optimization)** is used for material supply planning. Capacity is represented by default operation times for lead-time realism only.
- **Demand signal**: sales orders (confirmed, readiness-gated) are the primary MRP input. Forecast (if in scope) may be used for long-lead purchased items.
- **Coverage groups**: configured for MTO behavior — single-order explosion, no cross-order material reuse, minimum order quantity aligned with supplier terms.
- **Pegging**: maintained via the configuration dimension; planned orders are pegged to the originating sales order line.
- **External scheduling tool** may provide bulk date updates back to D365 for scheduled production orders.

### 6.4 Key design decisions

| # | Decision | Status |
|---|---|---|
| D-FTP-01 | Depth of S&OP process: demand forecast vs. pure SO-driven MRP | Open — TBD blueprint |
| D-FTP-02 | Mechanism for bulk date updates from external scheduler to D365 | Open |
| D-FTP-03 | Financial planning scope (budgeting module) | Open — TBD blueprint |
| D-FTP-04 | Aluminum (ALU) replenishment strategy: integrate into D365 MRP or retain separate XLS-based forecast | Open — TBD blueprint |

### 6.5 Integration touchpoints

| Interface | Direction | Trigger | Data |
|---|---|---|---|
| CPQ / PLM → D365 | Inbound | Order confirmation | Sales order lines (trigger MRP demand) |
| External scheduler → D365 | Inbound | Scheduling run | Planned/scheduled dates for production orders |

---

## 7. Order to cash

### 7.1 Winsol context & challenges

The commercial process at Winsol is managed by CPQ, which is the system of record for quotes, configuration, pricing, and order confirmation. D365 receives the **confirmed sales order** and manages order fulfillment, invoicing, accounts receivable, and credit management. The key challenge is ensuring that D365 sales orders are always complete and fully specified before they trigger planning or production.

### 7.2 Process scope

| Process area | Scope | Master system | Notes |
|---|---|---|---|
| Develop sales policies | Out of scope | | Managed in CPQ / commercial policy |
| Manage sales orders | **In scope** | ERP | D365 receives confirmed sales order from CPQ; manages fulfillment |
| Manage accounts receivable | **In scope** | ERP | Invoicing, customer payment management |
| Manage credit and collections | **In scope** | ERP | Credit limit management, collections |
| Analyze sales performance | **In scope** | ERP | Via financial dimensions + BI |

### 7.3 Proposed solution outline

- D365 receives **confirmed, fully specified sales orders** from CPQ (never partially specified orders).
- Sales order lines for MTO items reference the PLM-provided item variant; no configuration logic in D365.
- The **48-hour cooling-off period** is enforced by a requested delivery date / earliest ship date logic on the sales order.
- Invoicing and AR follow standard D365 processes; no significant customization expected.
- Margin at sales order line level is enabled by linking production order cost postings to the sales order line via financial dimensions.

### 7.4 Key design decisions

| # | Decision | Status |
|---|---|---|
| D-OTC-01 | Quotation handling: CPQ-only vs. D365 sales quotation as intermediate step | Open — to be confirmed in blueprint |
| D-OTC-02 | Cooling-off period enforcement mechanism in D365 | Open |
| D-OTC-03 | Financial dimension defaulting on sales order line (order reference automation) | Open |

### 7.5 Integration touchpoints

| Interface | Direction | Trigger | Data |
|---|---|---|---|
| CPQ → D365 | Inbound | Order confirmation | Confirmed sales order (header + lines) |
| D365 → Customer / Finance | Outbound | Sales invoice posting | Invoice document |

---

## 8. Source to pay

### 8.1 Winsol context & challenges

Source to pay is already live in D365 (Phase I). Phase II enhances procurement to address the specific challenge of **MTO-purchased items with late price determination**: items such as glass and ventilation components are specified and priced by the supplier after the customer order is confirmed. This makes three-way match and reliable accruals difficult with standard purchase order processing.

### 8.2 Process scope

| Process area | Scope | Master system | Notes |
|---|---|---|---|
| Develop procurement and sourcing strategy | **In scope** | ERP | Policies for MTO purchasing |
| Manage supplier relationships | **In scope** | ERP | Supplier master, approved supplier lists |
| Source and contract goods and services | **In scope** | ERP | Purchase agreements for standard items; MTO approach TBD |
| Procure goods and services | **In scope** | ERP | Purchase orders, receipts, three-way match |
| Manage accounts payable | **In scope** | ERP | AP, payment proposals |
| Analyze procurement and sourcing | **In scope** | ERP | Spend analysis via financial dimensions + BI |

### 8.3 Proposed solution outline

Three solution options for MTO purchase pricing are under evaluation. The preferred approach will be confirmed during blueprint:

| Option | Description | Complexity | Fit |
|---|---|---|---|
| **A — Supplier configuration interface** | Supplier system returns confirmed specification + price to D365 via integration (EDI/Peppol) | High | Best automation; requires supplier commitment |
| **B — Internal purchasing configurator (Power App)** | Buyer specifies structured purchase spec in a Power App; supplier confirms via EDI/Peppol with final price | Medium | Pragmatic; internal control |
| **C — Pricing tolerance policy** | PO raised without final price; price updated after supplier confirmation; automatic price variance posting + approval workflow | Low | Simplest to start; least proactive |

A staged approach is recommended: start with **Option C** as minimum viable implementation, with a roadmap toward Option A or B as supplier and process maturity allows.

### 8.4 Key design decisions

| # | Decision | Status |
|---|---|---|
| D-STP-01 | MTO purchase pricing solution: Option A / B / C (or hybrid roadmap) | Open — to be confirmed in blueprint |
| D-STP-02 | Purchase agreement strategy for MTO items with supplier frame contracts | Open |
| D-STP-03 | Accrual policy for MTO PO receipts without confirmed price | Open |

### 8.5 Integration touchpoints

| Interface | Direction | Trigger | Data |
|---|---|---|---|
| D365 → Supplier (Option A/B) | Outbound | PO creation | Purchase specification |
| Supplier → D365 (Option A/B) | Inbound | Supplier confirmation | Confirmed price, item attributes |
| D365 AP | Internal | Invoice matching | Three-way match: PO / receipt / invoice |

---

## 9. Plan to produce

### 9.1 Winsol context & challenges

This is the core of Phase II. Winsol currently operates without a formal production control system; planning and shop floor execution rely on the legacy AS/400 and ad-hoc processes. The current D365 implementation includes the **9A Advanced Manufacturing ISV**; the intent for Phase II is to render this ISV obsolete by replacing its functionality with standard D365 production control (see D-PTP-06). Phase II introduces:

- D365 discrete production orders, generated from MRP.
- MES integration for all execution actuals.
- Standard costing with post-calculation and variance analysis.
- WIP accounting at a stage level (target).

Key challenges:

- **Cost transparency**: current costing is fragmented and order-level margin is not systematically calculated.
- **WIP control**: WIP of approximately €500,000 with limited staging insight; month-end pressure.
- **Rework handling**: rework affects schedule and cost; currently no structured approach.
- **MES posting discipline**: actuals quality depends on MES operator discipline.

### 9.2 Process scope

| Process area | Scope | Master system | Notes |
|---|---|---|---|
| Develop production strategies | **In scope** | ERP | Production parameters, costing model, WIP policy |
| Plan production operations | **In scope** | ERP | MRP-driven planned orders → production orders |
| Run production operations | **In scope** | MES | MES records all actuals; D365 receives results |
| Control production quality | TBD | MES | Quality model to be defined; may overlay MES QC |
| Analyze production operations | **In scope** | ERP | Post-calculation, variance analysis, WIP reporting |

### 9.3 Proposed solution outline

- **Discrete production orders** in D365, exploded from MRP based on PLM-provided BOM and route.
- **No backflushing in D365**: all material consumption, operation times, and output/scrap are posted by MES; D365 receives and financially posts these actuals.
- **Standard cost** per configured MTO item (derived from PLM BOM and route + cost categories). Cost calculation triggered on item activation.
- **Post-calculation variances**: production order variance analysis (material variance, routing variance, overhead variance) posted at order close.
- **WIP by stage** (target): materials issued, labor posted, subcontracting — if endorsed by the business. Fallback: single WIP account per production order.
- **Rework**: handling model (separate routing operation vs. scrap + extra time) to be decided in blueprint.

### 9.4 Key design decisions

| # | Decision | Status |
|---|---|---|
| D-PTP-01 | WIP valuation granularity: by stage vs. single WIP account | Open — to be confirmed in blueprint |
| D-PTP-02 | Rework handling model: separate operation vs. scrap + extra time | Open — to be confirmed in blueprint |
| D-PTP-03 | Month-end cut-off policy: continuous vs. defined cut-off windows | Open |
| D-PTP-04 | Production quality control model (in or out of D365) | Open — TBD blueprint |
| D-PTP-05 | Overhead absorption model (cost categories, overhead rates) | Open |
| D-PTP-06 | 9A Advanced Manufacturing ISV: replace with standard D365 production control or retain | Open — to be confirmed in blueprint |

### 9.5 Integration touchpoints

| Interface | Direction | Trigger | Data |
|---|---|---|---|
| D365 → MES | Outbound | Production order release | Production order, BOM, route, planned dates |
| MES → D365 | Inbound | Operation completion / shift end | Operation time, material consumption, output qty, scrap qty |
| D365 | Internal | Production order close | Variance calculation, WIP settlement, COGS posting |

---

## 10. Inventory to deliver

### 10.1 Winsol context & challenges

The D365 WMS app was introduced in Phase I for two purposes: processing **purchase order receipts** and registering **movement journals** (component consumptions), with the financial dimension *project* specifiable from within the mobile app to maintain cost tracking per customer project.

A significant operational limitation today is that material consumption is **not registered live**. Component issues to production are captured through counting journals at monthly intervals, based on physical stock counts. As a result, inventory balances in D365 are unreliable between count cycles, MRP signals are only actionable immediately after a count, and order-level cost visibility depends on the quality of project dimension coding applied at the time of the counting journal. Phase II — through BOM-driven picking and issue transactions triggered by production order execution in MES — resolves this by enabling continuous, live inventory consumption registration.

Phase II builds on this foundation and extends WMS to cover the full manufacturing warehouse flow:

- **Production order picking**: automated work creation to pick raw materials and components per production order, replacing manual staging.
- **Sales order picking**: automated picking work for outbound finished goods shipments.
- **Other classic WMS processes** (e.g., put-away, cycle counting, location directives): scope and configuration to be defined during blueprint based on warehouse layout and operational requirements.

The guiding principle is **progressive adoption**: extend the WMS app that operators already use, without introducing advanced WMS complexity that is not justified by operational need.

### 10.2 Process scope

| Process area | Scope | Master system | Notes |
|---|---|---|---|
| Manage warehouse operations | **In scope** | ERP | Phase I: PO receipts + movement journals live; Phase II: extended to production and sales picking |
| Maintain inventory levels | **In scope** | ERP | Inventory transactions, physical and cycle counting |
| Process inbound goods | **In scope** | ERP | PO receipts via WMS app (Phase I); quality sampling TBD |
| Process outbound goods | **In scope** | ERP | Sales order picking via WMS app (Phase II — automated work creation) |
| Manage inventory quality | TBD | | TBD blueprint — may interact with MES QC |
| Manage freight and transportation | TBD | | TBD blueprint |
| Analyze warehouse operations | **In scope** | ERP | Inventory aging, stock levels, movement reporting |

### 10.3 Proposed solution outline

- The **D365 WMS app** is the operator interface for all warehouse transactions; no separate WMS platform is introduced.
- **Phase I baseline** (already live): purchase order receipt via WMS app; movement journals with financial dimension *project* for component consumption tracking.
- **Phase II extensions**:
  - Automated **production order picking work**: work creation triggered by production order release; operators pick via WMS app.
  - Automated **sales order picking work**: work creation triggered by sales order release to warehouse; operators pick and confirm shipment via WMS app.
  - Additional WMS processes (location directives, put-away rules, cycle counting frequency) to be configured during blueprint.
- **Inventory dimensions**: site, warehouse, location, and configuration dimension for MTO pegging.
- Advanced WMS features (license plate-based directed put-away at scale, ASN, wave/load management beyond the manufacturing flow) are out of scope unless specifically justified.

### 10.4 Key design decisions

| # | Decision | Status |
|---|---|---|
| D-ITD-01 | Scope of WMS processes to be configured in Phase II (beyond receipt, movement journals, production picking, sales picking) | Open — to be confirmed in blueprint |
| D-ITD-02 | Inventory quality management scope and integration with MES | Open — TBD blueprint |
| D-ITD-03 | Transportation management scope | Open — TBD blueprint |
| D-ITD-04 | Location directive and put-away strategy for raw materials and finished goods | Open — to be confirmed in blueprint |

### 10.5 Integration touchpoints

| Interface | Direction | Trigger | Data |
|---|---|---|---|
| D365 WMS | Internal | Production order release | Automated picking work for raw materials / components |
| D365 WMS | Internal | Sales order release to warehouse | Automated picking work for finished goods |
| MES → D365 | Inbound | Material issue from production | Inventory consumption transactions (where not covered by WMS picking) |
| D365 | Internal | Sales order shipment | Packing slip, inventory deduction, financial posting |

---

## 11. Record to report

### 11.1 Winsol context & challenges

Record to report (R2R) is partially live from Phase I (Finance). Phase II extends and deepens the R2R scope to support:

- Production costing (standard cost, WIP, variances) integrated with the general ledger.
- Financial dimension completeness for order-level margin visibility.
- Clean month-end close processes, including WIP cut-off.

### 11.2 Process scope

| Process area | Scope | Master system | Notes |
|---|---|---|---|
| Define accounting policies | **In scope** | ERP | Extended to cover production costing and WIP policies |
| Manage cash | **In scope** | ERP | Phase I scope; no Phase II changes expected |
| Manage budgets | **In scope** | ERP | Scope and depth TBD (see Forecast to plan) |
| Record financial transactions | **In scope** | ERP | Extended with production, WIP, variance postings |
| Close financial periods | **In scope** | ERP | Month-end playbook including WIP cut-off |
| Analyze financial performance | **In scope** | ERP | Profitability by order / site / product family via dimensions + BI |

### 11.3 Proposed solution outline

- The general ledger is extended with production cost accounts (WIP accounts by stage, variance accounts, COGS accounts) as part of Phase II configuration.
- A **month-end playbook** is designed in blueprint: WIP cut-off date, production order status at period end, open PO accruals, variance reconciliation steps.
- Financial dimensions (WinsolSalesReference + site/product family) enable margin analysis at the sales order line level without Project Operations.
- **Automated financial dimension defaulting** (from sales order → production order → financial posting) is a design requirement; no manual entry.

### 11.4 Key design decisions

| # | Decision | Status |
|---|---|---|
| D-RTR-01 | Chart of accounts extensions for production cost accounts | Open — to be designed in blueprint |
| D-RTR-02 | Month-end cut-off policy and WIP snapshot approach | Open |
| D-RTR-03 | Profitability reporting level: SO line, product family, site | Open |

### 11.5 Integration touchpoints

| Interface | Direction | Trigger | Data |
|---|---|---|---|
| Production → GL | Internal | Production order events (issue, report as finished, close) | WIP, COGS, variance postings |
| Procurement → GL | Internal | PO receipt and invoice | Accruals, AP postings |

---

## 12. Project to profit *(TBD)*

> **Status**: Scope not yet confirmed. This section is a placeholder pending blueprint decisions.

### 12.1 Context

Project to profit processes would apply if Winsol requires project-based cost tracking, project invoicing, or resource management beyond what financial dimensions provide. The current design uses financial dimensions (order reference) for order-level visibility without Project Operations. The scope of this end-to-end will be confirmed during blueprint.

### 12.2 Process scope (all TBD)

| Process area | Scope | Notes |
|---|---|---|
| Develop project strategy | TBD | |
| Manage project contracts | TBD | |
| Plan projects | TBD | |
| Manage project delivery | TBD | |
| Manage project financials | TBD | |
| Analyze project performance | TBD | |

---

## 13. Prospect to quote *(TBD)*

> **Status**: Scope not yet confirmed. This section is a placeholder pending blueprint decisions on CRM and CPQ integration.

### 13.1 Context

Prospect to quote is managed by CPQ, which is external to D365. A future CRM integration may bring opportunity and quotation data into D365 or a linked Dynamics 365 Sales environment. The scope for Phase II is TBD; it has no impact on the core Phase II manufacturing and finance design.

### 13.2 Process scope (all TBD)

| Process area | Scope | Notes |
|---|---|---|
| Manage customer relationships | TBD | |
| Identify and qualify leads | TBD | |
| Define sales strategy and policies | TBD | |
| Pursue opportunities | TBD | |
| Estimate and quote sales | TBD | |
| Analyze sales | TBD | |

---

# Part IV — Architecture & Integrations

## 14. Integration architecture

> **Integration middleware** — Phase I integrations between D365 and the legacy AS/400 were routed through the **Invictus platform** (Codit integration bus). Winsol IT is decommissioning Invictus as part of the move to Phase II. The Phase II integration strategy is **direct interfaces**: source systems will produce messages in a D365-compatible format and deliver them without a centralized middleware layer, to the extent technically feasible. This places message format ownership with individual source system teams and increases the importance of D365-native error visibility and monitoring (see §14.3).

### 14.1 Interface catalog

The table below provides a consolidated view of all cross-system integration interfaces. This catalog will be elaborated into full interface contracts (message format, frequency, error handling, retry policy) during blueprint.

| # | Source | Target | Trigger | Data | Frequency | Status |
|---|---|---|---|---|---|---|
| I-01 | CPQ | D365 | Order confirmation | Confirmed sales order (header + lines) | Real-time / near-real-time | TBD |
| I-02 | PLM | D365 | Product creation/update | Item master, released product, BOM, route, lifecycle state | Event-driven | TBD |
| I-03 | External validation | D365 | Completeness check result | Item lifecycle state update (readiness status) | Event-driven | TBD |
| I-04 | D365 | MES | Production order release | Production order, BOM, route, planned dates/quantities | Event-driven | TBD |
| I-05 | MES | D365 | Operation completion / shift end | Operation time, material consumption, output qty, scrap | Batch / near-real-time | TBD |
| I-06 | External scheduler | D365 | Scheduling run | Planned/scheduled dates for production orders (bulk update) | Batch | TBD |
| I-07 | Supplier (Option A/B) | D365 | Supplier configuration confirmation | Confirmed price, item specification | Event-driven | TBD |

### 14.2 Readiness gating design

Readiness gating prevents incomplete or unvalidated records from triggering downstream D365 processes (MRP, production order creation). The gating mechanism operates as follows:

1. PLM creates item variant + BOM + route → pushes to D365.
2. External validation framework checks completeness and consistency.
3. Validation result is written back to D365 as an **item lifecycle state** (e.g., "Draft", "Ready for planning").
4. D365 MRP coverage filter excludes items with lifecycle states below "Ready for planning".
5. Sales order lines referencing non-ready items are flagged; a status field on the sales order line reflects the readiness state for visibility to order management.

### 14.3 Error handling and monitoring principles

- All integration interfaces implement an acknowledgment / status write-back visible in D365 — not only in the middleware log.
- Reprocessing of failed messages must be possible without side effects (idempotent design).
- Integration exceptions are surfaced as functional exceptions in D365 (e.g., blocked orders, warning indicators) — not only as technical alerts.
- Integration monitoring and SLA definitions (max latency per interface, retry policy) will be specified in interface contracts during blueprint.

---

# Part V — Delivery

## 15. Master data governance

> Master data quality is a critical success factor given the multi-system landscape (CPQ / PLM / D365 / MES). This section defines ownership and governance for the key master data domains.

### 15.1 Master data ownership

| Domain | System of record | D365 role | Governance |
|---|---|---|---|
| Item variants (MTO) | PLM | Consumer / golden copy | PLM-triggered; no manual creation in D365 for MTO items |
| BOMs (MTO) | PLM | Consumer | PLM-provided; validated by readiness gate |
| Routes (MTO) | PLM | Consumer | PLM-provided; validated by readiness gate |
| Standard items (non-MTO) | D365 | Owner | Standard D365 item management |
| Customers | AS/400 | Consumer (via integration) | Customer master is maintained in AS/400 and synchronized to D365 via integration; Phase I scope. Migration of ownership to D365 or a future CRM system is a Phase III roadmap item. |
| Vendors / suppliers | D365 | Owner | Maintained by procurement |
| Cost prices (MTO items) | D365 | Owner | Calculated from PLM BOM/route; triggered by lifecycle state |
| Chart of accounts | D365 | Owner | Finance-owned |
| Financial dimensions | D365 | Owner | Defaults automated; manual override restricted |
| Work centers / resources | D365 | Owner | Aligned with MES resource model |

### 15.2 Master data quality requirements

- **Completeness gate**: MTO item variants may not enter planning until BOM, route, and item lifecycle state confirm readiness.
- **Naming conventions**: item numbering, BOM version numbering, and route version numbering conventions must be agreed between PLM and D365 teams before integration build.
- **Cost price activation**: a defined process (owner, frequency, approval) for activating standard cost prices for new MTO variants is required before go-live.
- **Work center alignment**: the D365 work center / resource group structure must align with the MES resource model to ensure accurate cost category and time registration mapping.

### 15.3 Data migration scope

> *This section will be elaborated as the project progresses. Placeholder content below.*

The following master data and open transaction categories require migration or cut-over preparation. Detailed scope will be defined during blueprint.

| Category | Migration type | Notes |
|---|---|---|
| Item masters (standard items) | Migration from legacy | Volume and cleansing effort TBD |
| Item masters (MTO variants) | Created via PLM integration | No historical migration; PLM integration creates these |
| Open sales orders at cut-over | Cut-over transaction | Strategy TBD (migrate open orders vs. close + re-enter) |
| Open production orders at cut-over | Cut-over transaction | Complex; WIP balance migration required |
| Open purchase orders at cut-over | Cut-over transaction | Strategy TBD |
| Customer master | Migration or Phase I carryover | Confirm if complete from Phase I |
| Vendor master | Migration or Phase I carryover | Confirm if complete from Phase I |
| Cost prices (standard cost) | Activation in D365 | Requires PLM BOM/route data to be available first |
| Historical transactions | Out of scope | No historical transaction migration; BI / reporting uses legacy data for pre-go-live history |

---

## 16. Reporting & analytics

### 16.1 Scope

Reporting and analytics in Phase II are focused on enabling the core business outcomes: order-level margin, WIP visibility, procurement spend, and production variance analysis. A broad Power BI program or a standalone analytics platform is **out of scope for Phase II**.

| Reporting area | In scope | Approach |
|---|---|---|
| Order-level margin (SO line) | Yes | Via financial dimensions (order reference) + D365 standard cost reports |
| Production variance analysis | Yes | D365 standard production variance report |
| WIP by stage | Yes (if staged WIP confirmed) | D365 WIP aging report + financial dimension filter |
| Procurement spend / AP aging | Yes | D365 standard procurement analysis |
| Inventory levels and aging | Yes | D365 standard inventory reports |
| Sales performance | Yes | D365 standard + financial dimensions |
| Cross-entity / group-level reporting | TBD | Requires BI layer; scope and tooling TBD |
| Advanced analytics / Power BI dashboards | Out of scope | Future phase |

### 16.2 Financial dimensions as the reporting backbone

Financial dimensions replace the need for Project Operations as the mechanism for profitability tracking. The following principles apply:

- **WinsolSalesReference dimension**: populated automatically from the sales order line; flows through to the production order and all financial postings. No manual entry.
- **Dimension defaulting logic** is a Phase II build requirement, not a configuration task. The defaulting rules (from sales order line → production order → sub-ledger posting) must be designed and tested as part of the integration and finance workstreams.
- Additional dimensions (e.g., product family, distribution channel) are to be confirmed during blueprint based on reporting requirements.

---

## 17. Budget

### 17.1 Budget envelope

The following budget envelope is used as the planning baseline for Phase II. Detailed estimates will be validated and refined after the blueprint phase.

| | Envelope | Notes |
|---|---|---|
| **External consulting** | approx. €600,000 | Fit-to-standard design; minimizes customization cost |
| **Internal effort (Winsol)** | approx. €600,000 | Process ownership, data preparation, UAT, cut-over support |
| **Total** | approx. €1,200,000 | |

### 17.2 External consulting — breakdown by workstream

| Workstream | Indicative share | Notes |
|---|---|---|
| Core D365 SCM / Production / Planning | 25–30% | Base configuration, production control, MRP, costing |
| Integrations (CPQ / PLM / MES + readiness gating) | 30–35% | Largest effort driver; complexity depends on interface maturity |
| Procurement enhancements (MTO purchase pricing) | 10–15% | Depends on Option A/B/C selection |
| Costing, WIP & post-calculation | 10–15% | |
| Data migration, testing & training | 10–15% | |
| PMO & change management | 5–10% | |

### 17.3 Internal effort — breakdown by activity

| Activity | Notes |
|---|---|
| Process ownership and decision-making | Required throughout blueprint and build phases |
| Master data preparation | Item master cleansing, cost price data, work center alignment |
| User acceptance testing (UAT) | Led by process owners; consulting support |
| Cut-over planning and execution | Production order status at go-live, WIP cut-over, open transaction migration |
| MES and supplier collaboration | Interface testing, MES posting discipline training |
| Change management and user adoption | Planner, buyer, finance, and production lead enablement |

### 17.4 Budget assumptions

The budget envelope is based on the following assumptions:

1. PLM delivers complete BOMs and routes for all MTO lines before go-live.
2. MES posts all actuals; D365 performs no backflushing.
3. CPQ remains the lead for quotes, configuration, and pricing; D365 receives confirmed orders only.
4. Lifecycle state / readiness gating is technically enforceable across all systems.
5. The selected procurement solution (Option A/B/C) does not require a large supplier-side integration program in Phase II.
6. Helios nv entity configuration complexity is representative of other Winsol legal entities for rollout purposes.
7. No major D365 platform upgrades or Microsoft release changes disrupt the build schedule.

---

## 18. Implementation approach & timeline

### 18.1 Methodology

- **Fit-to-standard first**: design follows D365 standard processes; customization only where cross-entity reusable and high ROI.
- **Blueprint before build**: all open decisions (see Section 19) are resolved during blueprint before build commences.
- **Pilot at Helios nv**: full Phase II scope implemented and validated at Helios; design artifacts serve as the rollout template.
- **Seasonality-aware go-live**: target go-live in September, ahead of the next peak demand season.

### 18.2 Phase timeline (indicative)

| Phase | Duration | Key outputs |
|---|---|---|
| Blueprint & architecture | 6–8 weeks | All open decisions resolved; detailed design per E2E; interface contracts; updated budget |
| Build & integrations | 12–16 weeks | D365 configuration, integration build, unit testing |
| Validation (SIT / UAT) & training | 8–10 weeks | System integration testing, user acceptance testing, training delivery |
| Cut-over & go-live preparation | 2–3 weeks | Data migration, cut-over rehearsals, go-live sign-off |

> Phases overlap. A detailed project plan with milestones and resource loading will be produced post-blueprint.

### 18.3 Rollout after Helios pilot

After Helios go-live, subsequent legal entity rollouts are expected to require:

- Legal entity-specific configuration (company accounts, legal settings, local tax).
- Data migration for the new entity.
- Targeted regression testing.

No redesign of core D365 configuration or integration interfaces is anticipated for rollouts, provided the pilot is clean.

---

## 19. Open decisions log

> This log collects all design decisions that require explicit stakeholder sign-off. It serves as the agenda for blueprint workshops. Decisions are linked to the E2E section where they are elaborated.
>
> Status values: **Open** | **In discussion** | **Confirmed**

| # | Decision | E2E section | Status | Owner | Target date |
|---|---|---|---|---|---|
| D-DTR-01 | Phantom item usage in MTO BOMs | §5 Design to retire | Open | | |
| D-DTR-02 | ECM process for in-flight production order changes | §5 Design to retire | Open | | |
| D-DTR-03 | Item numbering convention: PLM ID vs. D365-native | §5 Design to retire | Open | | |
| D-DTR-04 | Selective use of D365 ECM module (readiness policies and/or impact analysis) without adopting the full change order process | §5 Design to retire | Open | | |
| D-FTP-01 | Depth of S&OP process: demand forecast vs. pure SO-driven MRP | §6 Forecast to plan | Open | | |
| D-FTP-02 | Bulk date update mechanism from external scheduler to D365 | §6 Forecast to plan | Open | | |
| D-FTP-03 | Financial planning scope (budgeting module) | §6 Forecast to plan | Open | | |
| D-FTP-04 | Aluminum (ALU) replenishment strategy: integrate into D365 MRP or retain separate XLS-based forecast | §6 Forecast to plan | Open | | |
| D-OTC-01 | Quotation handling: CPQ-only vs. D365 sales quotation | §7 Order to cash | Open | | |
| D-OTC-02 | Cooling-off period enforcement mechanism in D365 | §7 Order to cash | Open | | |
| D-OTC-03 | Financial dimension defaulting on sales order line (automation) | §7 Order to cash | Open | | |
| D-STP-01 | MTO purchase pricing solution: Option A / B / C | §8 Source to pay | Open | | |
| D-STP-02 | Purchase agreement strategy for MTO items | §8 Source to pay | Open | | |
| D-STP-03 | Accrual policy for MTO PO receipts without confirmed price | §8 Source to pay | Open | | |
| D-PTP-01 | WIP valuation granularity: by stage vs. single WIP account | §9 Plan to produce | Open | | |
| D-PTP-02 | Rework handling model | §9 Plan to produce | Open | | |
| D-PTP-03 | Month-end cut-off policy | §9 Plan to produce | Open | | |
| D-PTP-04 | Production quality control model | §9 Plan to produce | Open | | |
| D-PTP-05 | Overhead absorption model | §9 Plan to produce | Open | | |
| D-PTP-06 | 9A Advanced Manufacturing ISV: replace with standard D365 production control or retain | §9 Plan to produce | Open | | |
| D-ITD-01 | Scope of WMS processes to configure in Phase II (beyond receipt, movement journals, production picking, sales picking) | §10 Inventory to deliver | Open | | |
| D-ITD-02 | Inventory quality management scope | §10 Inventory to deliver | Open | | |
| D-ITD-03 | Transportation management scope | §10 Inventory to deliver | Open | | |
| D-ITD-04 | Location directive and put-away strategy for raw materials and finished goods | §10 Inventory to deliver | Open | | |
| D-RTR-01 | Chart of accounts extensions for production cost accounts | §11 Record to report | Open | | |
| D-RTR-02 | Month-end cut-off policy and WIP snapshot approach | §11 Record to report | Open | | |
| D-RTR-03 | Profitability reporting level | §11 Record to report | Open | | |

---

## Changelog

| Version | Date | Author | Description |
|---|---|---|---|
| 0.1 | March 11, 2026 | | Initial document skeleton — scope, design principles, architecture, process outlines, budget |
| 0.2 | March 11, 2026 | | Phase I cross-check: MRP context (§6.1), CPQ toolset names (§2.1), PLM/CTO terminology note (§2.1), legal entity table (§1.3), WinsolSalesReference dimension name throughout, month-end counting pain point (§10.1), customer master ownership (§15.1), Invictus middleware context (§14), 9A ISV decision D-PTP-06, ALU decision D-FTP-04, D-ITD ordering fix in §19 |
