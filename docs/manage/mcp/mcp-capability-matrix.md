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

## Operations Matrix

### Systems

| Feature / Module     | Get | Create | Update | List | Execute | Notes |
|----------------------|-----|--------|--------|------|---------|-------|
| System               | ✅  | ✅     | ✅     | ✅   | —       | —     |
| System Type          | —   | —      | —      | ✅   | —       | —     |
| System Type Template | ✅  | —      | —      | —    | —       | —     |

### Metadata

| Feature / Module        | Get | Create | Update | List | Execute | Notes                                                                          |
|-------------------------|-----|--------|--------|------|---------|--------------------------------------------------------------------------------|
| Projects                | —   | —      | —      | ✅   | —       | Retrieve projects configured in a system                                       |
| Entity Types            | —   | —      | —      | ✅   | —       | Retrieve entity types for a system and project                                 |
| Fields                  | ✅  | —      | —      | —    | —       | Includes lookup values and complex field metadata (comments, attachments, relationships) |

### Mapping

| Feature / Module          | Get | Create | Update | List | Execute | Notes                                                                        |
|---------------------------|-----|--------|--------|------|---------|------------------------------------------------------------------------------|
| Mapping                   | ✅  | ✅     | ✅     | ✅   | —       | —                                                                            |
| Advanced Mapping Settings | ✅  | —      | ✅     | —    | —       | Conflict detection, overwrite rules                                          |
| Mapping XSLT              | ✅  | —      | ✅     | —    | —       | Get and update advanced mapping transformations using <code class="expression">space.vars.OIM</code> advanced methods |

### Integration

| Feature / Module              | Get | Create | Update | List | Execute | Notes                                                             |
|-------------------------------|-----|--------|--------|------|---------|-------------------------------------------------------------------|
| Integration                   | ✅  | ✅     | ✅     | ✅   | —       | —                                                                 |
| Integration Actions           | —   | —      | —      | —    | ✅      | Activate, inactivate, and on-demand execution of integrations     |
| Advanced Integration Settings | ✅  | —      | ✅     | —    | —       | Override parameters for read/write operations, criteria configuration |

### Folders & Schedules

| Feature / Module | Get | Create | Update | List | Execute | Notes |
|------------------|-----|--------|--------|------|---------|-------|
| Folder           | ✅  | ✅     | ✅     | ✅   | —       | —     |
| Schedule         | ✅  | ✅     | ✅     | ✅   | —       | —     |
| Workflow         | ❌   | ❌      | ❌      | ✅   | —       | List available workflows only; create/update not supported via MCP |

### Failures

| Feature / Module     | Get | Create | Update | List | Execute | Notes                                                  |
|----------------------|-----|--------|--------|------|---------|--------------------------------------------------------|
| Global Failure       | ✅   | —      | —      | ✅   | —       | —                                                      |
| Processing Failure   | ✅   | —      | ❌      | ✅   | —      | Retry supported; eventXML update not supported via MCP |
| Failure Notification | ✅  | ✅     | ✅     | —    | —       | —                                                              |

### Others


| Feature / Module | Get | Create | Update | List | Execute | Notes                    |
|------------------|-----|--------|--------|------|--------|--------------------------|
| Sync Report      | —   | —      | —      | ❌   | —      | —     |
| Audit            | —   | —      | —      | ❌   | —      | —     |
| Excel Upload     | ❌  | ❌    | ❌  | ❌   | —      | —      |
| Reconcile        | ❌  | —    | —   | ❌    | —      | —      |

### Health & Diagnostics

| Feature / Module | Get | Create | Update | List | Execute | Notes                                                                                              |
|------------------|-----|--------|--------|------|---------|---------------------------------------------------------------------------------------------------|
| Health Checkup   | ✅  | —      | —      | —    | —       | Includes integration failure analysis, and OIM instance system configuration and resource parameters |