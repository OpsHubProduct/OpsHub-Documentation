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
| Mapping                   | ✅  | ✅     | ✅     | ✅   | —       | Supports writing complex mapping transformation XSLTs using advanced methods provided by <code class="expression">space.vars.OIM</code> |
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
| Failure Notification | ❌  | ❌     | ❌     | —    | —       | —                                                              |
| Health Checkup   | ✅  | —      | —      | —    | —       | Includes integration failure analysis, and OIM instance system configuration and resource parameters |


### Metadata

| Feature / Module        | Get | Create | Update | List | Execute | Notes                                                                          |
|-------------------------|-----|--------|--------|------|---------|--------------------------------------------------------------------------------|
| Projects                | —   | —      | —      | ✅   | —       | —                                       |
| Entity Types            | —   | —      | —      | ✅   | —       | —                                 |
| Fields                  | ✅  | —      | —      | —    | —       | Includes lookup values and complex field metadata (comments, attachments, relationships) |

### Others

| Feature / Module | Get | Create | Update | List | Execute | Notes                    |
|------------------|-----|--------|--------|------|--------|--------------------------|
| Sync Report      | —   | —      | —      | ❌   | —      | —     |
| Audit            | —   | —      | —      | ❌   | —      | —     |
| Excel Upload     | ❌  | ❌    | ❌  | ❌   | —      | —      |
| Reconcile        | ❌  | —    | —   | ❌    | —      | —      |
