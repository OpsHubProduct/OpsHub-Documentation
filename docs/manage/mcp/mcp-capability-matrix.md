---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# MCP Capability Matrix — <code class="expression">space.vars.OIM</code>

This document provides an overview of the operations available through the <code class="expression">space.vars.OIM</code> MCP server. It outlines which operations (Get, Create, Update, List, Execute) are supported across functional areas exposed as MCP tools.

Use this matrix as a quick reference to understand MCP coverage.

> **Note**: Delete operations are not supported via MCP tools by design. Certain update operations on complex objects may behave as partial removals of sub-configurations and will require explicit user confirmation via the AI assistant before being applied.

---

## Legend

| Symbol | Meaning               |
|--------|-----------------------|
| ✅     | Supported via MCP     |
| ❌     | Not Supported via MCP |
| —      | Not Applicable        |

---

## Operations Matrix

| Feature / Module             | Get | Create | Update | List | Execute | Notes                                                                                      |
|------------------------------|-----|--------|--------|------|--------|--------------------------------------------------------------------------------------------|
| System                       | ✅  | ✅     | ✅     | ✅   | —      | —                                                                                          |
| System Type                  | —   | —      | —      | ✅   | —      | —                                                                                          |
| System Type Template         | ✅  | —      | —      | —    | —      | —                                                                                          |
| Mapping                      | ✅  | ✅     | ✅     | ✅   | —      | Includes advanced mapping config: conflict detection, overwrite rules, XSLT transformations |
| Integration                  | ✅  | ✅     | ✅     | ✅   | ✅      | Includes activate, inactivate, and on-demand execution                                     |
| Folder                       | ✅  | ✅     | ✅     | ✅   | —      | —                                                                                          |
| Schedule                     | ✅  | ✅     | ✅     | ✅   | —      | —                                                                                          |
| Workflow                     | ❌   | ❌      |❌      | ✅   | —      | List available workflows only                                                              |
| Global Failure               | ✅  | —      | —      | ✅   | —      | —                                                                                          |
| Processing Failure           | ✅  | —      | ❌      | ✅   | ✅      | Retry supported; eventXML update not supported                                             |
| Projects (Metadata)          | —   | —      | —      | ✅   | —      | Retrieve projects configured in a system                                                   |
| Entity Types (Metadata)      | —   | —      | —      | ✅   | —      | Retrieve entity types for a system and project                                             |
| Fields Meta                  | ✅  | —      | —      | —    | —      | Includes lookup values and complex field metadata (comments, attachments, relationships)   |
| Advanced XSLT                | ✅  | —      | —      | —    | —      | Reference for XSLT and core utility methods for advanced mapping                           |
| Health Checkup               | ✅  | —      | —      | —    | —       | Health checkup planner tool + OIM system information tool                                  |