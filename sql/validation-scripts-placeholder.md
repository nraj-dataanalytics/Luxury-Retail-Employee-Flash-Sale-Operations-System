# SQL Validation Scripts

The `.sql` files for this project will be added to this folder after the SharePoint data structure and sample data are finalised. All scripts are written in T-SQL and designed to run against a SQL Server database that mirrors the SharePoint list structure.

---

## Planned Scripts

| Script | Name | Purpose |
|---|---|---|
| 01 | Duplicate Active Access Records | Identifies employees with more than one Approved or Pending access record for the same sale — a data integrity check that should return zero rows in a clean system |
| 02 | All Pending Access Requests — SLA Status Check | Returns all pending requests with an SLA classification label: Within SLA (under 24 hours), Approaching Breach (24–47 hours), or SLA BREACHED (48 hours or more) |
| 03 | Expired Access Still Active | Identifies access records with status Approved where the sale end date has passed — flags employees who still appear active after the sale closed |
| 04 | Open High-Priority Issues | Returns all open or in-progress issues with Priority = High, with time elapsed since logging — used for escalation monitoring during an active sale |
| 05 | Incomplete Sale Setup | Validates sale records in Draft status against required fields — flags any record missing a sale name, start/end dates, discount percentage, departments, or locations |
| 06 | Sale Readiness Validation | Calculates a readiness score for each sale in Readiness Review status — counts completed vs. total checklist items and identifies which items are still open |
| 07 | Average Issue Resolution Time | Reports average, minimum, and maximum resolution hours by sale, issue category, and priority — used for post-sale retrospective analysis |
| 08 | Access Requests by Status | Summary of all access requests grouped by sale and status — provides approval rate, denial rate, and pending backlog counts used in the Power BI dashboard |
| 09 | Issues by Category and Priority | Aggregates all issues by category and priority — identifies which combinations have the highest volume and the longest resolution times |

---

## Technical Notes

- All scripts use T-SQL syntax (SQL Server / Azure SQL)
- Table names mirror SharePoint list names: `dbo.SaleMaster`, `dbo.EmployeeAccessRequests`, `dbo.ApprovalLog`, `dbo.IssueTracker`, `dbo.SaleReadinessChecklist`
- Scripts 07, 08, and 09 use window functions (`SUM OVER PARTITION BY`, `AVG OVER`) and conditional aggregation (`CASE` inside `SUM`)
- Script 02 uses `DATEDIFF(HOUR, RequestDate, GETDATE())` to calculate SLA age — no pre-filtering on request age, so all pending records are returned with their SLA label
- Script 06 produces a calculated `LaunchStatus` output label ('READY TO LAUNCH' / 'NOT READY') — this is a reporting output value only and does not correspond to any SharePoint status field

---

## File Naming Convention

```
sql/
├── 01_duplicate_active_access.sql
├── 02_pending_requests_sla_check.sql
├── 03_expired_access_still_active.sql
├── 04_open_high_priority_issues.sql
├── 05_incomplete_sale_setup.sql
├── 06_sale_readiness_validation.sql
├── 07_avg_issue_resolution_time.sql
├── 08_access_requests_by_status.sql
└── 09_issues_by_category_priority.sql
```

---

*Scripts will be added after sample data is confirmed and table schemas are finalised.*
