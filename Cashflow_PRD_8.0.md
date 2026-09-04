# Cashflow Projection Module Product Requirements Document

> Source: Cashflow_PRD_8.0.docx
> Purpose: Complete Markdown reference for designing the overall clickable mockup.

# Cashflow & Management Module PRD v7.6

# Cashflow & Management Module - PRD v7.6

Module / Product Name: Cashflow Projection Module
Version: v7.6
Status: Integrated PRD Draft for PiR / Dev Discovery / Prototype Planning
PM Owner: Roopa
PO / Tech Lead: TBD

Solution Architect Ravi Kumar
UX/UI Lead: Marina Rambo

## 1. Product Summary

The Cashflow Projection Module is a Hub-based project planning layer that helps DPR project teams create, maintain, review, and share monthly cashflow forecasts.

There can be 4 versions of Cashflow for the lifecycle of the project.

AI generated cashflow curve: The module starts with an AI-generated monthly cashflow summary, with project start and end dates, and contract value from project meta data.

User should be able to provide the following parameters to scenario plan the project cashflow curve.

Start Date

End Date

Contract Value

Upfront Payment Value

Upfront Payment Date

Change Order Value

At this point, no cashflow forecast grid is created.

Manual Cashflow - Forecast Grid + Cashflow Curve: Allows the project team to refine that projection into a detailed, editable, forecast that connects the following parameters. project/opportunity attributes such as number, name

- contract value and project start and end dates

- payment terms, upfront payment value, upfront payment date.

- Schedule of values (sov) and schedule duration for each row

- Distribution curves for each sov

- Allow forecast to be manually edited.

- forecast snapshots

- owner-facing report exports

At this point, there is no connection to any source systems such as Ediphi, P6 or CMiC.

Estimate Connected Cashflow - Forecast Grid + Cashflow Curve: When a project estimate becomes available, a notification triggers to enable the project team to connect the estimate to generate a cashflow forecast grid and a more realistic cashflow curve.

Owner Billing Connected Cashflow - Forecast Grid + Cashflow Curve: When a CMiC project becomes available, a notification triggers to enable the project team to connect SoVs in CMiC to Billing Codes and P6 activity groups. This is when the cashflow becomes real, with actuals data from billing tied to forecast, helping teams maintain cashflow through the life of the job.

### Product positioning

This is not a full treasury cash position model in MVP. MVP focuses on projected owner billings by month, with actual billing comparison and forecast maintenance.

Future phases may expand into full cash position modeling, receipt timing, retainage release, payment timing, trade partner input, accrual logic, advanced payment payback, and portfolio-level dashboards.

## 2. Strategic Fit & Outcomes

### 2.1 Company / Org Objectives

DPR currently lacks a standardized project-level workflow for creating, maintaining, and sharing cashflow / billing forecasts. Project teams often rely on spreadsheets, local assumptions, and disconnected reconciliation across estimating, scheduling, accounting, billing, and actuals systems.

The Cashflow Forecast Module creates a connected planning workflow in The Hub. It allows users to start with a credible system-generated projection, refine it using project knowledge, map estimate scope to owner billing and CMiC financial structures, maintain the forecast against actual billings, and preserve trusted snapshots over time.

### 2.2 Primary Outcomes

The module should enable DPR to:

- Create a monthly billing forecast for every qualifying opportunity/project once enough project information exists.

- Reduce or eliminate the need for blank-sheet Excel forecasting work.

- Give project teams a credible starting projection.

- Connect estimate structure, owner billing structure, schedule timing, and CMiC actuals.

- Provide a maintainable monthly forecast grid.

- Lock actual months and preserve editable future months.

- Track forecast vs actual variance.

- Save monthly snapshots with revision numbers.

- Support owner-facing export/reporting in the owner-required grouping.

- Create a trusted planning signal for controllers through MSR, EPM, and future roll-up.

### 2.3 Success Metrics

Initial success measures:

## 3. Problem & Opportunity

### 3.1 Problem Statement

DPR does not currently have a standard project-level monthly billing forecast workflow. Forecasts are often created manually, separately from the systems that already contain estimate, schedule, budget, owner billing, and actual billing data.

This creates inconsistent forecasts, duplicated controller/project-team effort, limited trust in forecast freshness, and weak connections between owner-facing billing expectations and CMiC actuals.

### 3.2 Current Pain Points

- No repeatable cashflow/billing forecast baseline exists across projects.

- Project teams often start from a blank spreadsheet.

- Controllers may manually assemble or reconcile forecasts with siloed information.

- Estimate, schedule, owner billing, CMiC phase codes, budgets, and actual billings are disconnected, and there is seldom connection all the way through from an estimate through owner billings.

- Forecasts are difficult to maintain once actual billings begin.

- Owner-facing forecast views may not align with internal job-cost structures.

- Bid packages, owner billing codes/SOV/WBS, and CMiC phase codes are not consistently mapped.

- Actual billings do not reliably land against the same structure used for forecast planning.

- Forecast freshness and review status are difficult for downstream consumers to trust.

- Complex and mega-project teams rely on sophisticated Excel workbooks because standard tools are too rigid.

### 3.3 Opportunity

The opportunity is to create a standard, guided, but flexible Hub workflow where every qualifying project can:

- Start with an AI/system-generated monthly forecast summary.

- Review the assumptions and source inputs behind the forecast.

- Choose whether to keep the summary view, manually build a forecast, or create a detailed estimate-forward forecast and eventually a forecast tied to owner billings.

- Organize the forecast around the billing structure required by the owner/client.

- Map estimate scope to billing codes/SOV/WBS.

- Map CMiC phase codes and actuals into that same billing structure.

- Track forecast vs actual variance and adjust future months.

- Save monthly snapshots and share reviewed views.

## 4. Users, Personas, and Review Workflows

### 4.1 Primary Users

#### PM / Project Team

Primary owner of the working project forecast.

Needs:

- review AI-generated starting projections

- understand expected monthly owner billings structure

- refine forecast structure

- adjust monthly forecast values and distribution curves

- prepare owner-facing views

- save reviewed snapshots

#### PX / Project Executive

Responsible for business confidence, review, and sign-off expectations.

Needs:

- review forecast structure and major changes

- confirm forecast readiness for owner-facing reviews

- understand variance, billing trend, and stale status

- support owner/project-level communication

#### Precon Manager

Early-stage user who may initiate or review forecast assumptions before project execution.

Needs:

- use early project/opportunity data to connect estimate information to the forecast

- support transition from early AI forecast to estimate-forward forecast

#### Project Controls

Supports schedule logic, distribution curves, forecast timing, and complex project breakdowns.

Needs:

- define and maintain groupings such as building, area, phase, package, or WBS

- tie forecast rows to schedule dates or activity groups

- apply distribution curves

- support manual date fallback

#### Project Accountant

Supports billing structure, CMiC mapping, actual billing alignment, and reconciliation.

Needs:

- validate owner billing/SOV/WBS alignment

- map CMiC phase codes/group codes to billing codes

- review actual billings and locked periods

- support forecast vs actual maintenance

#### Regional Controller / Controller

Review-oriented consumer who needs confidence in forecast quality and freshness.

Needs:

- see reviewed vs stale status

- understand mapping completeness

- review forecast vs actual variance

- consume reliable project-level forecast data for finance/EPM workflows

### 4.2 Secondary Users

Exact review workflow behavior remains TBD. MVP should avoid heavy approval workflows, but should preserve review status, reviewer identity, and snapshot/revision history.

### 4.4 Permissions

## 6. Workflow

### End-to-End Workflow Modules

- Executive Summary

- AI Cashflow Summary

- Manual Cashflow Forecast Setup Utility

- Estimate-Forward Cashflow

- CMiC Billing & Phase-Code Mapped Cashflow

- External Report Setup & Export

### 1. Module 1 - Executive Summary

Provide a single page The application shall provide an Executive Summary dashboard for each project that automatically consolidates project metadata, estimate information, cost information, schedule information, and cash-flow forecast results into a visual summary comparable to the provided reference.

The Executive Summary shall update automatically when underlying project setup, budget, mapping, schedule, or cash-flow forecast information changes.

### 2. Module 1 - AI Cashflow Summary

- User opens the Cashflow Module in The Hub.

- System generates an initial benchmark cashflow.

- User sees the AI cashflow summary, current graph, and available project metadata.

- User can edit metadata such as:

- start date

- end date

- contract value

- upfront payment value

- upfront payment date

- change order value

- payment terms, if available

- User can continue with the AI summary and export it, or click on "Manual Cashflow Forecast" to create a detailed forecast.

- Reference screenshot below. Included to inform prototyping language, not as a mandated final UI.

### 3. Module 3 - Manual Cashflow Forecast Setup Utility

Use this path when estimate data is not yet available, or the project team wants to manually set up the forecast.

- User selects Setup Manual Project Cashflow.

- User enters SOV values:

- Allow for SOV parent & child structure

- duration for each SOV at the lowest level

- budget for each SOV at the lowest level

- select distribution curve

- User clicks Generate Cashflow.

- Tool populates the forecast grid.

- User can export as Excel.

- User can save a snapshot with revision number and timestamp.

- User can continue to keep this forecast grid updated monthly.

### 4. Module 4 - Estimate-Connected Cashflow Mapping

Use this path when Ediphi estimate data is available. Send a notification to the PM assigned to the project about an ediphi estimate becoming available to produce an estimate connected Cashflow.

- Auto select the primary estimate, but allow user to select an alternative Ediphi estimate/version.

- User selects upto 3 levels of input/grouping structure.

- System shows available estimate dimensions such as bid package, MF, UF, location, building, WBS, or other estimate grouping data.

- If schedule data is available, user selects P6 schedule.

- System maps selected SOV/billing structure to P6 activities.

- Durations are auto populated.

- User selects the Distribution Curve for each SOV

- Based on owner requirements, user selects project forecast grouping. This defines the forecast grid the owner would like to see.

- User can override:

- budget

- date range

- curve type.

MVP should support standard distribution curves:

- flat / straight-line

- front-loaded

- back-loaded

- bell / centered curve

- monthly values

- User selects "generate cashflow"

- Tool generates/updates the forecast grid.

- Allow comments at a SOV line item level.

### 5. Export Estimate Grouping Utility

### Provide the ability for the user to export SOV Id, description to Group Code 1, 2, 3 as selected in the tier.

### 6. Module 5 - Cashflow Forecast Grid

- Based on the estimate and/or schedule mapping, and the grouping selected, the forecast grid is populated.

- User can override:

- curve type

- monthly forecast values for current and future months

- forecast is locked for past months

- User can export the forecast grid to share internally/externally.

- User can take snapshots that will save as a new revision with the timestamp.

### 6. Module 6 - CMiC Group Codes & Phase-Code Mapped Cashflow

- CMiC job is set up and budget is loaded.

- User opens mapping utility.

- This utility auto-maps group codes to bill codes.

- Monthly forecast grid is now populated or enriched with:

- SOVs

- CMiC budgets

- actual billing

- distribution-curve-based forecast

- Actual billing months are locked once actuals are posted/closed. Actual billings display for the posted/closed months.

- Future forecast remains editable so that user can adjust forecast data for remaining forecast months.

- Forecast vs actual variance is visible.

- System calculates monthly and cumulative forecast, actuals, trends, and variance.

- User saves monthly snapshot/revision.

- If no user initiated snapshot is taken in a month, the system auto-generates a snapshot on the last day of the month.

## 7. Data Model and Key Objects

### 7.1 Core Objects

### 7.2 Forecast Line Fields

Minimum fields:

- line ID

- parent line ID

- line type

- description

- billing code / owner SOV / owner WBS

- estimate source reference

- bid package / estimate grouping reference

- CMiC phase code/group code reference

- schedule driver reference

- start date

- finish date

- duration

- budget

- retention held

- curve type

- monthly forecast values

- monthly actual values

- locked period indicator

- variance

- manual override flag

- review status

- mapping completeness status

## 8. Systems and Integrations

### 8.1 Source Systems and Roles

### 8.2 Systems of Record

## 9. Functional Requirements

## 10. Non-Functional Requirements

## 11. UX / UI Expectations

### 11.1 UX Goals

The user experience should make project teams feel that the module already has a useful starting point, while still giving them control to adjust, override, map, review, and share the forecast.

The experience should be:

- guided but flexible

- AI-assisted but human-reviewed

- clear about data sources and assumptions

- organized around owner billing structure

- transparent about mapping completeness

- easy to maintain monthly

- explicit about actuals and locked periods

- safe for owner-facing output

- flexible enough for complex projects

## 12. AI / Model Behavior

### 12.1 AI Use Cases

AI/model/rules-based logic may be used to:

- generate initial benchmark cashflow summary

- infer monthly projection from project attributes

- suggest comparable curve assumptions

- suggest estimate-to-billing mappings

- suggest CMiC-to-billing mappings

- suggest distribution curves

- identify likely source changes or forecast issues

- support future AI reforecasting after actuals

### 12.2 Human-in-the-Loop Rules

- AI output is assistive, not authoritative.

- System-generated forecasts must be visibly labeled.

- Users must be able to review and override.

- Owner-facing export should warn if the forecast is system-generated only, stale, or unreviewed.

- Low-confidence AI/model output should fall back to default curves/manual inputs.

- Forecast status should be visible to downstream consumers.

- Manual override must always remain available.

### 12.3 Fallback Plan

If AI/model/source data is unavailable or not credible, the module should still work using:

- manual cashflow setup

- standard curves

- manual dates

- manual mapping

- user-entered monthly forecast values

- Excel/paste/import support, if feasible

### 12.4 Evaluation Plan

Pilot evaluation should answer:

- Is the AI starting projection credible enough to be useful?

- Does the AI summary make users more likely to create a detailed forecast?

- Is the detailed workflow faster than building a spreadsheet?

- Can users map estimate scope to billing codes without confusion?

- Can users map CMiC phase codes to billing codes so actuals land correctly?

- Do actual months lock cleanly?

- Can users adjust remaining forecast after variance?

- Do controllers trust status/freshness/mapping completeness metadata?

- Can complex project teams see a path away from Excel?

## 13. Risks, Dependencies, and Open Questions

### 13.1 Risks

### 13.2 Dependencies

### 13.3 Open Questions

- What defines a qualifying project for automatic AI cashflow creation?

- Should AI cashflow be created for all new projects or only projects above a threshold?

- Which source provides the earliest reliable project attributes: Hub, Cosential, CMiC, or another source?

- What exact project parameters can be used in the AI benchmark forecast?

- What is the minimum acceptable standard for a credible AI starting forecast?

- Should users be required to confirm the Ediphi estimate version before import?

- How should active estimate changes affect an existing forecast?

- What estimate dimensions are consistently available from Ediphi?

- What is the canonical owner billing/SOV/WBS source for MVP?

- Should billing codes be created inside the module when no owner structure exists?

- What is the exact CMiC phase-code/group-code mapping source?

- Does CMiC mapping require loaded budgets, or can phase codes be mapped before final budget load?

- What is the actual billing source and monthly lock rule?

- How should retention held be calculated or entered in v1?

- Is retention release fully deferred?

- What owner-facing export format is required?

- Should owner-facing export require PX/accountant acknowledgement?

- What should PX Review, Accountant Review, and Regional Controller Review mean in MVP?

- Should review be a lightweight status or a formal workflow?

- What variance thresholds should trigger review?

- What source changes should mark a forecast stale?

- What monthly snapshot revision naming convention should be used?

- Should users be able to compare snapshots?

- How should multiple jobs/sub-jobs/related jobs be handled?

- What complex/mega-project grouping fields are required in MVP?

- Should configurable review cadence be visible only or also trigger notifications?

- What MSR status/link/prompt is required?

- What EPM payload and metadata are required?

- Should Excel paste/import be required in MVP?

- When should AI reforecasting after actuals be introduced?

## 14. Phase 2 / Future Discovery

Potential future enhancements:

- AI reforecast based on actual billing trends

- full cash position modeling

- payment receipt timing

- retainage release forecasting

- pay-when-paid modeling

- advanced payment/payback engine

- accrual forecasting logic

- trade partner forecast input

- Project Portal integration

- Textura integration, if validated

- comparable-project curve builder

- user-selected comparable-project benchmarking

- more advanced variance warnings

- mapping drift detection

- change-order-specific forecast logic

- cost-category forecasting

- Resource Management / GCGR integration

- quarterly owner variance reporting

- portfolio/BU/regional dashboards

- scenario planning

- snapshot comparison

- formal approval workflow, if required


## Extracted Table 1

| Success Area | Target / Indicator |
| --- | --- |
| Starting forecast coverage | Every project over $10M contract value and 6 month duration receives an AI/system-generated monthly starting projection when contract value, project start and end dates are available. |
| Manual effort reduction | Controller/project-team time spent assembling project-specific forecasts is reduced, with a target of 50%+ reduction where the module replaces manual Excel workflows. |
| Adoption | PMs/PXs/Project Controls/Project Accountants use the module as part of the monthly billing/MSR rhythm. |
| Detail conversion | A meaningful share of AI summary forecasts are converted into detailed forecast grids. |
| Mapping completeness | Users can identify and resolve unmapped estimate, billing code, or CMiC phase-code records. |
| Maintenance quality | Actual months are locked, future months remain editable, and variance is visible. |
| Snapshot discipline | Users save monthly snapshots/revisions before sharing or downstream consumption. |
| Controller trust | Controllers can see forecast status, freshness, review state, and mapping completeness. |
| Complex-project viability | Complex/mega-project users can see a credible path away from standalone Excel models. |


## Extracted Table 2

| User | Primary Need |
| --- | --- |
| Leadership / BU / Region | Read-only visibility into project-level billing forecast trends and risk signals. |
| EPM / F&A Consumers | Downstream forecast payload, status, and confidence in metadata. |
| Owner-facing/internal report consumers | Exported or shared views organized by owner-required billing structure. |


## Extracted Table 3

| Role | View Cashflow Grid | Edit Cashflow Grid | Export / Share | Notes |
| --- | --- | --- | --- | --- |
| PM / Project Team | Yes | Yes | Yes | Primary forecast owner/editor. |
| PX | Yes | Yes | Yes | Review/sign-off oriented. |
| Precon Manager | Yes | Yes | Yes | Early projection and estimate-forward setup. |
| Project Controls | Yes | Yes | Yes | Schedule/distribution/grouping support. |
| Project Accountant | Yes | Yes | Yes | Billing, actuals, mapping, reconciliation. |
| Controller / Regional Controller | Yes | No | Yes | Review/downstream finance consumer. |
| Leadership | Yes | No | Yes | Read-only trend/risk visibility. |
| Other project user | Yes | Request-based | Yes | Lightweight access model. |


## Extracted Table 4

| Object | Description |
| --- | --- |
| Project | Hub project/opportunity context for forecast. |
| Forecast | Current working forecast for a project. |
| Forecast Snapshot | Point-in-time saved forecast, assigned revision number and metadata. |
| Forecast Line | Row in the forecast grid; may represent bid package, billing code, SOV item, WBS node, manual line, or grouping node. |
| Billing Code / Owner SOV / Owner WBS | Central owner-facing structure used for reporting, forecast organization, and mapping. |
| Estimate Source | Ediphi estimate/version and selected estimate dimensions. |
| Estimate Dimension | Bid package, MF, UF, building, location, WBS, or other estimate grouping. |
| Schedule Driver | Schedule activity, milestone, start/end date, manual date, or activity group. |
| Distribution Curve | Rule for spreading a line's budget across months. |
| CMiC Phase Code / Group Code | Internal job-cost/financial structure used to connect actuals. |
| Actual Billing | Actual billing value from validated financial source. |
| Retention Held | Retention amount held by line/period; retention release is future phase. |
| Review Status | Reviewed, stale, draft, etc. |
| Mapping Record | Saved relationship among estimate scope, billing code/SOV/WBS, and CMiC phase/group code. |


## Extracted Table 5

| System / Source | MVP Role |
| --- | --- |
| The Hub | User entry point and planning layer. Stores forecast, mapping decisions, snapshots, review status, and user edits. |
| AI / Rules-Based Forecasting Layer | Generates starting cashflow summary and benchmark curve. |
| Ediphi | Primary source for detailed estimate, and estimate grouping dimensions. |
| Schedule Viewer / P6 / OPC | Timing source for forecast distributions and schedule activity groups; manual fallback required. |
| CMiC | Source for budgets, phase codes, group codes, actual billings, and locked periods. |
| Cosential / Opportunity Source | Potential early source for opportunity/project attributes used in AI summary. |
| Snowflake / CDM | Likely data layer for downstream consumption/reporting. |


## Extracted Table 6

| Data Domain | Source of Truth |
| --- | --- |
| Estimate / bid package values | Ediphi |
| Estimate grouping dimensions | Ediphi |
| Schedule dates / milestones / activity groups | P6 / OPC; manual fallback in Hub |
| Budgets / phase codes / group codes | Ediphi / CMiC |
| Owner billing / SOV | CMiC |
| Actual billings | CMiC |
| Forecast distributions | Hub Cashflow module |
| User overrides | Hub Cashflow module |
| Mapping decisions made in module | Hub Cashflow module |
| Forecast snapshots/revisions | Hub Cashflow module |


## Extracted Table 7

| ID | Requirement | Priority | Acceptance Criteria |
| --- | --- | --- | --- |
| FR-1 | System shall generate an AI/system-assisted starting monthly cashflow forecast for eligible projects. | Must | Given sufficient project attributes, when a user opens the module, then an AI/system-generated monthly cashflow summary is visible or clearly being prepared. |
| FR-2 | System shall label AI/system-generated forecasts clearly. | Must | Users and downstream consumers can see whether a forecast is system-generated, draft, reviewed, stale, or snapshot/revisioned. |
| FR-3 | System shall show key source assumptions used in the AI summary. | Must | User can view available assumptions such as start date, end date, contract value, upfront payment, payment terms, and change order value where available. |
| FR-4 | System shall support a basic-to-detailed transition. | Must | User can open the AI summary and proceed to detailed manual or estimate-forward forecast setup. |
| FR-5 | System shall support manual cashflow setup. | Must | User can manually create SOV/forecast lines, enter duration, budget, and curve, then generate the forecast grid. |
| FR-6 | System shall support parent/child SOV or forecast-line structure. | Must | User can create or view at least one parent-child hierarchy in the forecast grid. |
| FR-7 | System shall allow export of manual forecast grid to Excel. | Should | User can export the grid to Excel format or equivalent tabular download. |
| FR-8 | System shall allow monthly forecast snapshots with revision number and timestamp. | Must | User can save a snapshot and see a revision number/history. |
| FR-9 | System shall allow user to select/confirm the Ediphi estimate version used to seed the detailed forecast. | Must | User can select or confirm the estimate source before importing estimate lines. |
| FR-10 | System shall support bid packages as a primary forecast planning structure. | Must | Bid packages from estimate appear as available forecast/grouping inputs. |
| FR-11 | System shall support additional estimate dimensions. | Should | User can use dimensions such as MF, UF, building, location, WBS, or other estimate groupings where available. |
| FR-12 | System shall support schedule-driven distribution. | Must | Forecast rows can use schedule dates, activity groups, or milestones where available. |
| FR-13 | System shall support manual date entry and manual duration. | Must | User can proceed when schedule data is unavailable or insufficient. |
| FR-14 | System shall support standard distribution curves. | Must | User can apply flat, front-loaded, back-loaded, bell/centered, and/or S-curve style distribution where enabled. |
| FR-15 | System shall allow manual monthly overrides. | Must | User can override generated monthly forecast values and see that the row is manually adjusted. |
| FR-16 | System shall use billing code / owner SOV / owner WBS as a central mapping layer. | Must | Forecast can be organized and rolled up by billing code/SOV/WBS. |
| FR-17 | System shall support estimate-to-billing-code mapping. | Must | User can map estimate rows/bid packages/groupings to billing codes/SOV/WBS and save mappings. |
| FR-18 | System shall identify unmapped or incomplete estimate-to-billing records. | Must | Unmapped items are flagged and available for correction. |
| FR-19 | System shall support CMiC-to-billing-code mapping. | Must | User can map CMiC phase codes/group codes/SOVs/activity groups to billing codes/SOV/WBS and save mappings. |
| FR-20 | System shall identify unmapped or incomplete CMiC mapping records. | Must | New or unmapped CMiC records are flagged for review. |
| FR-21 | System shall preserve mapping decisions made inside the module. | Must | Saved mappings persist in the Hub planning layer and can be reused/reviewed. |
| FR-22 | System shall populate/enrich the monthly forecast grid from CMiC billing/phase-code mapping. | Must | Forecast grid can show bid package/SOV/budget/retention/actual/forecast fields using mapped CMiC data. |
| FR-23 | System shall import or display actual billings from validated source. | Must | Actual billing values appear in relevant periods when available. |
| FR-24 | System shall lock actual billing months. | Must | Closed/actual months are visible and not editable; future months remain editable. |
| FR-25 | System shall show forecast vs actual variance. | Must | User can see variance by month and forecast line/rollup. |
| FR-26 | System shall allow remaining forecast adjustment after actual variance. | Must | User can manually reforecast future periods after actuals differ from forecast. |
| FR-27 | System shall support retention held by line item in MVP. | Must | User can see or enter retention held for line items; retention release timing is out of scope. |
| FR-28 | System shall calculate monthly and cumulative totals. | Must | Grid shows monthly forecast total, cumulative forecast total, retention totals, billing actuals, trends, and variance. |
| FR-29 | System shall support owner-facing forecast grouping. | Must | User can define/select owner-required grouping and generate owner-facing view. |
| FR-30 | System shall support owner-facing export/report. | Should | User can export/share a reviewed forecast organized by owner billing/SOV/WBS structure. |
| FR-31 | System shall provide export/share guardrails. | Should | User sees warning/acknowledgement if forecast is stale, unreviewed, system-generated only, or mapping-incomplete. |
| FR-32 | System shall display forecast status and freshness metadata. | Must | Last reviewed, last source refresh, source/version, and status are visible. |
| FR-33 | System shall surface source changes requiring review. | Should | Estimate, schedule, CMiC, actuals, owner SOV, or mapping changes can flag affected rows. |
| FR-34 | System shall support lightweight review states. | Should | PX, accountant, and regional controller review lanes can be represented through status/comment metadata without heavy approvals. |
| FR-35 | System shall support MSR visibility/linking. | Should | MSR can show cashflow status, stale flag, or link into the module. |
| FR-36 | System shall support related job/sub-job inclusion review where applicable. | Should | User can confirm inclusion/exclusion when related jobs/sub-jobs appear. |
| FR-37 | System shall support configurable review cadence. | Should | Project can indicate monthly, biweekly, weekly, or custom review cadence; exact automation TBD. |
| FR-38 | System shall support manual continuation when AI/model/source data is incomplete. | Must | User can proceed with manual inputs, default curves, and manual mapping. |
| FR-39 | System shall support special/manual forecast lines if feasible. | Could | User can add lines such as change order, contingency, advanced payment, accrual, or manual adjustment; advanced logic may be future phase. |
| FR-40 | System shall support future AI reforecasting as a Phase 2 hook. | Could | Data model does not block future AI reforecast after actuals; MVP may remain manual. |


## Extracted Table 8

| ID | Category | Requirement | Priority |
| --- | --- | --- | --- |
| NFR-1 | Performance | Module should feel quick and responsive for monthly project workflows. | Must |
| NFR-2 | Data Freshness | Source freshness and forecast review state must be visible. | Must |
| NFR-3 | Reliability | Saves, snapshots, revisions, and mappings must persist without data loss. | Must |
| NFR-4 | Usability | Forecast grid, mapping, and distribution workflows must be intuitive and low-friction. | Must |
| NFR-5 | Resilience | Users must be able to proceed when source data is incomplete. | Must |
| NFR-6 | Auditability | Save, snapshot, mapping, review, and export events should retain basic history. | Should |
| NFR-7 | Permissions | Lightweight role-based access should support view/edit/export separation. | Should |
| NFR-8 | Transparency | System-generated, reviewed, stale, locked, overridden, and mapping-incomplete states must be obvious. | Must |
| NFR-9 | Scalability | Data model should support standard projects and future complex/mega-project configurations. | Must |
| NFR-10 | Export Safety | Owner-facing exports should not silently share stale/unreviewed/system-generated-only forecasts. | Should |


## Extracted Table 9

| Risk | Impact | Mitigation |
| --- | --- | --- |
| AI projection is not credible | Users may reject the workflow early | Use visible assumptions, manual override, and fallback curves. |
| Mapping workflow becomes too broad | MVP may expand into a general enterprise mapping platform | Limit mapping to what is required for forecast, owner billing, CMiC actuals, and export. |
| Billing-code structure is unclear | Forecast cannot align to owner requirements | Make billing code/SOV/WBS a first-class setup object. |
| Actual billing source/lock rule is unclear | Locked periods and variance may be inaccurate | Validate source and close-period logic before build-lock. |
| Users do not maintain forecasts | Forecasts become stale and lose trust | Use owner, review cadence, stale indicators, MSR visibility, and monthly snapshot discipline. |
| Owner-facing export of unreviewed data | External communication risk | Add export guardrails and acknowledgement. |
| Complex project needs overload MVP | Product becomes too complex for first release | Support configurable hooks, manual overrides, nesting, and paste/import; defer automation. |
| CMiC mapping incomplete | Actuals cannot land correctly | Flag unmapped records and require correction before trusted variance view. |
| Estimate changes after setup | Forecast may become stale or inconsistent | Flag changed estimate version and affected mappings. |
| Schedule data incomplete | Distribution may be wrong | Allow manual dates and curves. |


## Extracted Table 10

| Dependency | Needed From | Notes |
| --- | --- | --- |
| Project/opportunity attributes | Hub / Cosential / source TBD | Required for AI summary. |
| Ediphi estimate data | Estimate Viewer / Ediphi integration | Required for detailed estimate-forward forecast. |
| Estimate dimensions | Ediphi | Needed for bid package, MF, UF, building, location, WBS grouping. |
| Schedule dates/activity groups | Schedule Viewer / P6 / OPC | Required for schedule-driven distribution; manual fallback required. |
| CMiC phase codes/group codes | CMiC / finance data | Required for actuals mapping. |
| Actual billing data | CMiC / validated financial source | Required for locked actual periods and variance. |
| Owner SOV/billing codes/WBS | OCS / CMiC / Project Accounting / Contract source TBD | Required for owner-facing organization. |
| EPM requirements | F&A / controller stakeholders | Must validate downstream expectations. |
| MSR connection | MSR/reporting workflow owners | Adoption and visibility surface. |
| Complex project design partners | Mega/complex project teams | Validate advanced grouping and manual override needs. |

## Project Context for Mockups

DPR Construction is a general contractor building an in-house cashflow projection and management tool for project teams in the construction industry. The product is intended to make monthly owner-billing forecasting easy to understand and maintain across the project lifecycle, from early opportunity planning through estimate connection, owner billing structure, CMiC actuals, variance review, and owner-facing reporting.

The overall mockup should feel like a world-class construction operations tool: practical for PMs, PXs, Project Controls, Project Accountants, Preconstruction Managers, and Controllers; clear about assumptions and source data; fast to update monthly; transparent about forecast health, mapping completeness, review status, stale data, actual-month locks, and future-month editability; and flexible enough for complex and mega-projects without feeling like a generic finance application.

For the Executive Summary screen, prioritize a single project-level view that answers: What is the current forecast? How does it compare with actuals and budget? Is the forecast trustworthy and up to date? What requires attention? Which forecast version/source is active? What is the next project-team action?
