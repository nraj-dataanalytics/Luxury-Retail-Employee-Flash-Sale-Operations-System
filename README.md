# Luxury Retail Employee Flash Sale Operations System

A Power Platform portfolio project — end-to-end operational support system for managing employee flash sales in a luxury retail environment.

---

## Overview

Employee flash sales in luxury retail are time-sensitive, tightly controlled events. They require coordinating eligibility verification, access approvals, pre-launch readiness, live-event support, and post-sale access revocation — all within strict operational and compliance standards.

This project is a fully designed, low-code operational system built on Microsoft Power Platform. It manages the complete flash sale lifecycle: from sale setup and access request management through launch authorisation, issue tracking, and post-sale cleanup.

The system is designed to demonstrate production-level thinking across Power Apps, Power Automate, SharePoint Online, Power BI, and SQL validation — including documentation, data modelling, workflow design, and operational reporting.

---

## Business Problem

Without a purpose-built system, employee flash sale operations typically rely on email chains, spreadsheets, and manual approval processes. The common failure points are:

- Employees gain access without completing the required approval process
- Approval requests are missed because there is no centralised queue
- Launch readiness cannot be confirmed — events are delayed or cancelled
- Active-sale issues have no structured intake channel
- Access is not revoked after the sale ends, creating compliance exposure
- There is no audit trail to reconstruct who had access, when, and why

In luxury retail, these failures carry additional weight. Brand integrity, access exclusivity, and audit accountability are non-negotiable operational standards.

---

## Solution

A Canvas App in Microsoft Power Apps, connected to a SharePoint Online backend, with Power Automate handling all workflow automation and Power BI providing refreshable operational reporting.

The system handles:

- Sale event creation and configuration
- Employee access requests with eligibility validation
- Manager approval routing via automated email workflow
- Pre-launch readiness checklist with gated launch authorisation
- Live-sale issue tracking with priority classification
- Post-sale access revocation and cleanup tracking
- SQL validation scripts for data quality and SLA monitoring
- Refreshable Power BI dashboard for operational KPIs

---

## Tools and Technologies

| Layer | Tool |
|---|---|
| App Interface | Microsoft Power Apps (Canvas App) |
| Workflow Automation | Microsoft Power Automate |
| Data Backend | Microsoft SharePoint Online |
| Operational Reporting | Microsoft Power BI |
| Data Validation | SQL Server / T-SQL |
| Documentation | Markdown, Word, PDF |

---

## System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                  PRESENTATION LAYER                      │
│          Microsoft Power Apps (Canvas App)               │
│   Role-based navigation · 10 screens · Power Fx logic   │
└──────────────────┬──────────────────────────────────────┘
                   │ reads / writes
┌──────────────────▼──────────────────────────────────────┐
│                    DATA LAYER                            │
│            Microsoft SharePoint Online                   │
│   8 structured lists · linked via SaleID foreign key    │
└──────────┬───────────────────────────┬──────────────────┘
           │ triggered by              │ connects to
┌──────────▼───────────┐  ┌───────────▼──────────────────┐
│   PROCESS LAYER      │  │       REPORTING LAYER         │
│  Power Automate      │  │       Microsoft Power BI      │
│  7 cloud flows       │  │  4-page refreshable dashboard │
│  approvals · alerts  │  │  DAX measures · star schema   │
│  reminders · cleanup │  │  KPIs · readiness score       │
└──────────────────────┘  └──────────────────────────────┘
```

---

## Key Modules

**SharePoint Backend** — 8 structured lists forming the data layer: Sale Master, Employee Access Requests, Approval Log, Issue Tracker, Notification Log, Change History, Sale Readiness Checklist, and User Role Reference. All lists are linked via a shared `SaleID` field.

**Power Apps Canvas App** — 10 screens with role-based navigation controlled by the User Role Reference list. Roles: Operations Admin, Manager, Employee, Read-Only. Screens cover the full lifecycle from sale setup through post-sale cleanup.

**Power Automate Flows** — 7 cloud flows: Access Request Approval, Sale Setup Approval, Launch Reminder, High-Priority Issue Alert, Status Notification, Post-Sale Cleanup Reminder, and Daily Active Sale Summary.

**SQL Validation Scripts** — 9 T-SQL scripts for data integrity checks, SLA monitoring, expiry detection, and operational reporting. Includes window functions, conditional aggregation, and multi-label SLA classification.

**Power BI Dashboard** — 4-page refreshable dashboard: Sale Operations Overview, Access and Approvals, Issues and Support, and Sale Readiness / Post-Sale Summary. Star schema data model with DAX measures.

---

## Current Implementation Status

| Component | Status |
|---|---|
| SharePoint Backend (8 lists, full schema) | Design Complete — Build Pending |
| Power Apps Canvas App (10 screens) | Design Complete — Build Pending |
| Power Automate Flows (7 flows) | Design Complete — Build Pending |
| SQL Validation Scripts (9 scripts) | Design Complete — Build Pending |
| Power BI Dashboard (4 pages) | Design Complete — Build Pending |
| GitHub Documentation | In Progress |
| Portfolio Case Study | Planned |

See [`implementation-status.md`](./implementation-status.md) for detailed status.

---

## Repository Structure

```
luxury-retail-flash-sale-ops/
│
├── README.md                        ← This file
├── implementation-status.md         ← Build progress tracker
│
├── docs/
│   ├── Project_Charter.pdf          ← Project objective, scope, business value
│   ├── System_Build_Plan.pdf        ← Architecture, modules, build sequence
│   └── SharePoint_Backend_Schema.pdf ← Full SharePoint list specifications
│
├── data/
│   └── sample-data-placeholder.md  ← Sample data plan (data added after build)
│
├── sql/
│   └── validation-scripts-placeholder.md ← SQL script plan (.sql files added after build)
│
└── screenshots/
    └── README.md                    ← Screenshot checklist (images added during build)
```

---

## Planned Next Steps

1. Build and configure all 8 SharePoint lists from the schema specification
2. Import sample data and verify list relationships
3. Build the Canvas App — starting with Home and Admin Control Panel screens
4. Build and test all 7 Power Automate flows
5. Write and test all 9 SQL validation scripts against mirrored tables
6. Build the Power BI dashboard and configure scheduled refresh
7. Capture screenshots and add to this repository
8. Publish complete documentation and portfolio case study

---

## Screenshots

*Screenshots will be added as the build progresses. See [`screenshots/README.md`](./screenshots/README.md) for the full capture checklist.*

| Screen | Status |
|---|---|
| SharePoint lists (sample data loaded) | Pending |
| Power Apps — Home screen (employee view) | Pending |
| Power Apps — Access request with validation | Pending |
| Power Apps — Admin control panel | Pending |
| Power Apps — Readiness checklist complete | Pending |
| Power Automate — Approval flow diagram | Pending |
| Power BI — Sale overview dashboard | Pending |
| Power BI — Readiness score (100%) | Pending |
| SQL — SLA status check output | Pending |

---

## Notes

- All sample data in this repository is **synthetic and created for demonstration purposes only**. No real employee names, company data, or business records have been used.
- Power Fx formulas included in the build plan are draft implementation patterns. They should be tested against final SharePoint internal column names and control names before use.
- The `SaleID` generation formula used in the Power Apps design (based on `CountRows`) is acceptable for portfolio demonstration but is not production-safe. A production deployment should use SharePoint item ID, `GUID()`, or a Power Automate-generated sequence.

---

*Portfolio project — Nandani Raj*
