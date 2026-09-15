---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---


This document provides an overview of the operations available through the <code class="expression">space.vars.OIM</code> MCP server. It outlines which operations (Get, Create, Update, List, Execute) are supported across functional areas exposed as MCP tools.

Use this matrix as a quick reference to understand MCP coverage.

> **Note**: Delete operations and modification of failed synchronization records are not supported via MCP. Refer to [Known Behaviours and Limitations](mcp-known-limitations.md) for details.
---

## Legend

| Symbol | Meaning               |
|--------|-----------------------|
| ✅     | Supported via MCP     |
| ❌     | Not Supported via MCP |
| —      | Not Applicable        |

---

## Operations matrix

### Systems, Mappings & Integrations

| Feature / Module     | Get | Create | Update | List | Execute | Notes                                                                                                                                |
|----------------------|-----|--------|--------|------|---------|--------------------------------------------------------------------------------------------------------------------------------------|
| System               | ✅  | ✅     | ✅     | ✅   | —       | —                                                                                                                                    |
| System Type          | —   | —      | —      | ✅   | —       | —                                                                                                                                    |
| System Type Template | ✅  | —      | —      | —    | —       | —                                                                                                                                    |
| Mapping                   | ✅  | ✅     | ✅     | ✅   | —       | Includes advanced/customized mapping with XSLTs and mapped fields settings |
| Integration                   | ✅  | ✅     | ✅     | ✅   | ✅       | —                                                                                                                                    |

### Folders & Schedules

| Feature / Module | Get | Create | Update | List | Execute | Notes |
|------------------|-----|--------|--------|------|---------|-------|
| Folder           | ✅  | ✅     | ✅     | ✅   | —       | —     |
| Schedule         | ✅  | ✅     | ✅     | ✅   | —       | —     |
| Workflow         | ❌   | ❌      | ❌      | ✅   | —       | — |

### Integration monitoring & maintenance

| Feature / Module     | Get | Create | Update | List | Execute | Notes                                                  |
|----------------------|-----|--------|--------|------|---------|--------------------------------------------------------|
| Global Failure       | ✅   | —      | —      | ✅   | —       | —                                                      |
| Processing Failure   | ✅   | —      | ❌      | ✅   | —      | — |
| Failure Notification | ✅  | ✅     | ✅     | —    | —       | Configured per integration. Update replaces the configuration rather than merging into it |
| Health Checkup   | ✅  | —      | —      | —    | —       | Includes integration health analysis, failure diagnostics, and visibility into OIM instance configuration and resource utilization details |


### Metadata

| Feature / Module        | Get | Create | Update | List | Execute | Notes                                                                          |
|-------------------------|-----|--------|--------|------|---------|--------------------------------------------------------------------------------|
| Projects                | —   | —      | —      | ✅   | —       | —                                       |
| Entity Types            | —   | —      | —      | ✅   | —       | —                                 |
| Fields                  | ✅  | —      | —      | —    | —       | Includes fields, comments, attachments, relationships |

### Reconciliation

| Feature / Module | Get | Create | Update | List | Execute | Notes |
|------------------|-----|--------|--------|------|---------|-------|
| Reconciliation   | ✅  | —      | ✅     | —    | ✅      | Switch into reconciliation mode and back, and change reconciliation status. The integration must be inactive, and reconcile rules must be configured on the mapping beforehand |
| Reconcile Rules  | ✅  | —      | ✅     | —    | —       | Configured on the **mapping**, through the mapping tools |

### Reporting & exports

| Feature / Module | Get | Create | Update | List | Execute | Notes |
|------------------|-----|--------|--------|------|---------|-------|
| Sync Report      | —   | —      | —      | ✅   | —       | Answers questions about synchronised entities — counts, entity pairing, sync state, and activity over a period |
| Usage Report     | ✅   | —      | —      | —    | —      | Exported as a ZIP of the last-six-months and last-one-year workbooks.|
| Metrics Report   | ✅   | —      | —      | —    | —      | Exported as a spreadsheet for the supplied filters. ``|

### Others

| Feature / Module | Get | Create | Update | List | Execute | Notes                    |
|------------------|-----|--------|--------|------|--------|--------------------------|
| Audit            | —   | —      | —      | ❌   | —      | Audits of changes made through MCP are viewed in the <code class="expression">space.vars.OIM</code> UI. See [MCP Audits](mcp-audits.md)     |
| Excel Upload     | ❌  | ❌    | ❌  | ❌   | —      | —      |
