# Product Requirements Document (PRD)
## Cashflow Forecast Tool — Phase-Lifecycle Cashflow & Management Module

**Document version:** 1.0
**Status:** Prototype / Working Spec
**Last updated:** September 4, 2026
**Owner:** Hub Product Team

---

## 1. Overview

The Cashflow Forecast Tool is a construction project cashflow management module that models a project's cash curve as it **matures through four lifecycle phases**. The central idea: forecast accuracy and control increase as more upstream data sources connect. Each phase unlocks only once its required data source is connected, and the two "mapping" phases are what allow owner billing and CMiC job-cost actuals to reconcile against the forecast.

The tool is built around a real construction workflow: an AI-generated prediction at pursuit time, followed by an estimate-driven billing structure, followed by cost-system phase-code mapping, and finally forecast-versus-actuals tracking with a per-code source of truth.

### 1.1 Problem statement

Construction finance teams struggle to maintain an accurate, trustworthy cashflow forecast across a project's life because the data lives in disconnected systems (CRM, estimating, scheduling, and job-cost/ERP). Values are re-keyed, billing structures diverge from cost-system phase codes, and actuals never cleanly line up with the forecast lines they belong to. The result is forecasts that drift from reality and manual reconciliation work.

### 1.2 Solution summary

A single, phase-gated workspace that:
- Generates a baseline cash curve automatically from CRM contract data.
- Lets teams build an owner billing structure and roll estimate scope into it.
- Validates and maps cost-system (CMiC) phase codes to billing codes so actuals flow to the correct forecast line.
- Tracks forecast vs. actuals with a **per-billing-code source of truth** (estimate-based vs. CMiC-based).

### 1.3 Goals

- Provide one continuous forecast that evolves from pursuit through construction.
- Eliminate manual reconciliation between owner billing and job-cost actuals.
- Make forecast maturity explicit and gated on real data availability.
- Preserve auditability via snapshots at each maturity milestone.

### 1.4 Non-goals

- Line-level (estimate-item-to-actual) reconciliation. Reconciliation happens at the **group billing code** level only.
- Replacing the source systems (Cosential, Ediphi, Schedule Viewer, CMiC). The tool integrates and maps, it does not replace.
- General ledger accounting or invoicing.

---

## 2. Users & personas

| Persona | Role | Primary needs |
|---|---|---|
| **Project Executive / PM** | Owns the forecast | See maturity, current forecast vs. contract, variance |
| **Project Accountant / Finance** | Maintains billing structure & mapping | Build billing codes, map estimate + CMiC, manage source of truth |
| **Preconstruction / Estimator** | Provides the estimate | Ensure estimate scope maps cleanly into billing structure |
| **Owner / Client (indirect)** | Approves billing format | Sign off on billing groupings via mock-bill approval gate |

---

## 3. Core concepts & domain model

### 3.1 Project lifecycle phases

The project advances through an ordered set of phases. Each phase requires a specific connected data source to unlock.

| # | Phase (id) | Label | Required source | Purpose |
|---|---|---|---|---|
| 1 | `prediction` | Early Prediction | Cosential | AI-generated cash curve from contract dates & value |
| 2 | `estimate-billing` | Estimate & Billing | Ediphi | Pull the estimate, build a billing structure, map estimate items (Mapping A) |
| 3 | `cmic-mapping` | CMiC Phase Mapping | CMiC | Validate & map CMiC phase codes to billing codes (Mapping B) |
| 4 | `forecast-actuals` | Forecast vs Actuals | CMiC Actuals | Track actuals vs. forecast with mixed source-of-truth per code |

### 3.2 Data sources

| Source | Label | Description |
|---|---|---|
| `cosential` | Cosential | CRM — contract dates & value |
| `ediphi` | Ediphi | Estimate line items |
| `schedule` | Schedule Viewer (OPC) | Activity dates |
| `cmic` | CMiC | Job cost phase codes & budgets |
| `cmicActuals` | CMiC Actuals | Posted job-cost actuals |

### 3.3 The two mappings (the heart of the tool)

- **Mapping A — Estimate → Billing:** Multiple Ediphi estimate line items roll up into a single owner billing (group) code. This defines how estimate scope is billed to the owner.
- **Mapping B — CMiC → Billing:** Each CMiC job-cost phase code maps up to a single billing code so posted actuals land on the correct forecast line. Because CMiC uses CSI-style numbering that does not textually equal the billing codes, a **validation step** determines whether remapping is required (e.g., CMiC `15-0200` Mechanical must be mapped to billing `05-Services`).

### 3.4 Billing structure

A multi-level tree of **billing codes**. Key properties per code:
- `code`, `name`, `parentId`, `level`, `isGroup` (rolls up children)
- `sourceOfTruth`: `estimate` | `cmic` (per code)
- `cmicBudget`: present once a CMiC budget lands
- `estimateValue`: rolled up from mapped estimate items
- `mockBillApproved`: owner sign-off gate before CMiC phase-code setup

**Seed options** (`BillingSeed`): Company Standards, Client Template, Regional Template, Estimate WBS, or From Scratch.

### 3.5 Source of truth (per code)

Each billing code carries its own source of truth. A code forecasts from estimate-based scope until a real CMiC budget lands, at which point it can be switched to CMiC as the source of truth. Reconciliation is at the **group code** level — there is no line-level reconciliation.

### 3.6 Distribution curves

Estimate item monthly spread is modeled with distribution curves: **Front-Loaded**, **Bell** (default), **End-Loaded**, **Linear**, and **Custom** (manual edits). Curves are normalized patterns interpolated to fit each item's active duration.

### 3.7 Snapshots

Point-in-time captures of the forecast (name, timestamp, author, phase, total forecast, estimate items) for auditability — e.g., "AI Prediction (baseline)" and "User Update #1 — Estimate loaded."

---

## 4. Functional requirements

### 4.1 Global shell & navigation

- **Left sidebar** with: back-to-hub link, project identity (name, contract value, number), a **Lifecycle Overview** link, and a **Phase Stepper** listing all four phases with lock/complete/current status.
- **Data-source strip** across the top of the main content showing connection state of all sources.
- **Save controls**: "Save Changes" (enabled only with unsaved changes) and "Save Snapshot."
- Content is rendered client-side with a loading fallback (avoids hydration issues).
- `/` redirects to `/cashflow`.

### 4.2 Lifecycle Overview (`/cashflow`)

- Header showing current phase (e.g., "Phase 2 of 4 · Estimate & Billing").
- Three metric cards: **Contract Value**, **Current Forecast**, **Actuals to Date** (with over/under variance sub-label).
- A card per phase showing: index, label, description, status pill (Complete / In progress / Available / Locked), and per-phase progress bars for the two mapping phases (estimate items mapped; CMiC codes mapped).
- Locked phases show "Connect {source} to unlock this phase."
- Each unlocked phase has a CTA (Open / Continue / Review) routing to its page.

### 4.3 Phase 1 — AI Cash Prediction (`/cashflow/prediction`)

- Auto-generated **cumulative** cash curve from contract value + start/end dates using a bell distribution.
- Read-only (badges: "AI generated", "Read-only").
- Metric cards for Contract Value, Start, Finish.
- Area chart of predicted cumulative cashflow.
- Single CTA: "Build billing structure" → Phase 2.

### 4.4 Phase 2a — Billing Structure (`/cashflow/billing`)

- **Seed selector** (Company Standards, Client Template, Regional, Estimate WBS, From Scratch) with description.
- **Billing tree** with group codes rolling up mapped estimate values.
- **Add code** dialog (create new billing codes, optionally nested under a group).
- Total mapped estimate summary.
- **Mock-bill approval** count and gate: group codes must be owner-approved before CMiC setup.
- CTA: "Map estimate to billing" → Phase 2b.

### 4.5 Phase 2b — Map Estimate to Billing / Mapping A (`/cashflow/mapping-estimate`)

- Progress bar: N/total estimate items mapped.
- **Two-column layout**: left = unmapped estimate items (multi-select), right = owner billing group codes with their rolled-up members.
- **Assignment action bar** (sticky): shows selected count + total, target billing-code selector, and Assign button.
- Unassign action per mapped member (returns item to unmapped list).
- Empty state when all items are mapped.
- CTA: "CMiC phase mapping" → Phase 3.

### 4.6 Phase 3 — CMiC Phase Mapping / Mapping B (`/cashflow/mapping-cmic`)

- **Step 1 — Validation gate:** "Run validation" compares billing structure to CMiC phase codes.
  - **Exact match** → no mapping required; offer "Push Hub codes to CMiC" to lock structure by construction.
  - **Mismatch** → shows count of unmatched CMiC codes; offer "Auto-suggest by division prefix."
- **Step 2 — Remap table** (revealed after validation): each CMiC phase code maps to a single billing code, with a mapped progress indicator and per-row suggested match.
- **Completion CTA** appears when all CMiC codes are mapped → Phase 4.

### 4.7 Phase 4 — Forecast vs Actuals (`/cashflow/forecast`)

- Totals: **Total Forecast**, **Actuals to Date**, **Variance** (color-coded).
- **Cumulative cashflow** composed chart: forecast area + actuals line (actuals connect nulls, stop at current month).
- **Monthly planning grid** (matrix of forecast/actuals per month; locked cells where actuals exist).
- **Source-of-truth table** per leaf billing code: Estimate value, CMiC budget, Actuals (rolled up via Mapping B), and a **source toggle** (Estimate ↔ CMiC) shown only where a CMiC budget exists; otherwise an "Estimate only" badge. Actuals roll up to the billing code through the CMiC→billing mapping.

### 4.8 Editing & forecast behavior

- Editing a month's forecast switches that item's curve to **Custom** and recomputes variance; **locked** (actualized) months cannot be edited.
- Changing an item's curve or dates redistributes its forecast across active months (locked months preserved).
- All edits set an unsaved-changes flag.

### 4.9 Save & snapshots

- **Save Changes** clears the unsaved flag.
- **Save Snapshot** captures a named point-in-time forecast (author, phase, total forecast, deep-copied estimate items).

### 4.10 PDF export

- Landscape PDF report via jsPDF + autoTable: header, project info, summary band (Total Budget, Forecast, Actuals, Variance), detail tables (by bid package or owner billing/SOV), and a monthly forecast breakdown page with paginated footers.

---

## 5. Data model reference

**Project:** `id`, `name`, `number`, `client`, `region`, `status` (`pursuit`/`precon`/`active`/`closeout`), `contractValue`, `startDate`, `endDate`, `currentPhase`, `connectedSources`, `billingStructureId`, `predictionAccepted`.

**BillingCode:** `id`, `code`, `name`, `parentId`, `level`, `isGroup`, `sourceOfTruth`, `cmicBudget`, `estimateValue`, `mockBillApproved`.

**EstimateItem:** `id`, `code`, `name`, `category`, `wbs`, `value`, `billingCodeId`, `startDate`, `endDate`, `distributionCurve`, `monthlyData[]`.

**CMiCPhaseCode:** `id`, `code`, `description`, `billingCodeId`, `cmicBudget`, `hasActuals`, `actualsToDate`.

**MonthlyData:** `month` (`YYYY-MM`), `forecast`, `actual`, `isLocked`, `variance`.

**Snapshot:** `id`, `name`, `createdAt`, `createdBy`, `phase`, `totalForecast`, `estimateItems[]`.

### 5.1 Reference dataset (prototype)

- **Project:** "DPR Medical Center Phase 2" (PRJ-2026-0042), Regional Healthcare System, Southwest, active.
- **Timeline:** 2026-01 → 2027-06; mock "today" = 2026-04 (months before can have actuals).
- **Contract value:** sum of 14 estimate bid packages (~$48.15M).
- **Billing structure:** "DPR Standard Billing" — 11 codes across GC, Sitework (group), Structure, Building Services/MEP (group), Envelope, Interior Finishes (group), Medical Equipment.
- **CMiC:** 10 phase codes using CSI numbering designed to force a mismatch (e.g., `15-0200` Mechanical → `05-Services`), demonstrating the remap flow.
- Deterministic variance generation (sine-based, not random) to avoid hydration mismatches.

---

## 6. Business rules & logic

1. **Phase gating:** a phase is unlocked only when its required source is connected.
2. **Mapping A rollups:** billing code `estimateValue` = sum of directly mapped estimate items; group codes additionally sum their children.
3. **Mapping B validation:** `exact-match` only when every CMiC code maps to a billing code **and** every leaf billing code is covered; otherwise `mismatch`.
4. **Actuals attribution:** actuals aggregate to a billing code via the CMiC→billing mapping; unmapped CMiC actuals do not flow.
5. **Source of truth:** togglable only where a CMiC budget exists; reconciliation is at group-code level.
6. **Locked months:** months with posted actuals are immutable in forecast editing.
7. **Mock-bill approval:** group codes should be owner-approved before CMiC phase-code setup.

---

## 7. Non-functional requirements

- **Architecture:** Next.js App Router; client-rendered module with Zustand for state; mock data layer (prototype has no backend persistence).
- **Charts:** shadcn chart wrappers over Recharts (Area / ComposedChart).
- **Determinism:** no `Math.random` in data generation (avoids SSR/CSR hydration mismatch).
- **Accessibility:** semantic landmarks (`aside`, `main`, `nav`), ARIA labels on icon-only controls and loading states.
- **Design system:** shadcn/ui components; themed via design tokens; 2-font, limited-palette system.
- **Performance:** memoized aggregations; live selectors for rollups, mapping progress, validation, and totals.

---

## 8. Success metrics

- % of projects with a fully mapped estimate (Mapping A completion rate).
- % of projects reaching CMiC exact-match / fully mapped (Mapping B completion rate).
- Reduction in manual reconciliation time between billing and actuals.
- Forecast-to-actual variance accuracy over the project lifecycle.
- Time-to-first-forecast (pursuit → Phase 1 curve).

---

## 9. Future considerations

- Real integrations replacing the mock layer (Cosential, Ediphi, Schedule Viewer, CMiC) with backend persistence and auth.
- Multi-project portfolio rollups.
- Schedule-driven redistribution (using Schedule Viewer activity dates to drive curves).
- Change-order handling and contract-value revisions.
- Collaboration: comments, approval routing, and audit trail on snapshots.
- Line-level reconciliation as an optional advanced mode.

---

## 10. Route & file map

| Route | Purpose |
|---|---|
| `/` | Redirects to `/cashflow` |
| `/cashflow` | Lifecycle Overview |
| `/cashflow/prediction` | Phase 1 — AI Prediction |
| `/cashflow/billing` | Phase 2a — Billing Structure |
| `/cashflow/mapping-estimate` | Phase 2b — Mapping A |
| `/cashflow/mapping-cmic` | Phase 3 — Mapping B |
| `/cashflow/forecast` | Phase 4 — Forecast vs Actuals |

**Key modules:** `lib/cashflow/types.ts` (domain types), `lib/cashflow/store.ts` (Zustand store + selectors), `lib/cashflow/mock-data.ts` (dataset + rollup/validation helpers), `lib/cashflow/distribution-curves.ts` (curve math), `lib/cashflow/pdf-export.ts` (report export).
