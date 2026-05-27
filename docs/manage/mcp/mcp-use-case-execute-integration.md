---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---


## Description

A user wants to immediately trigger all active integrations between two configured systems without navigating the <code class="expression">space.vars.OIM</code> UI.

## Example Interaction

| Component | Detail |
|-----------|--------|
| **User prompt** | "Execute all active integrations between Jira and HP ALM right now." |
| **MCP tools invoked** | `get_integrations_list` (filtered by system pair and ACTIVE status) → `execute_status_change` (status: EXECUTE) |
| **AI assistant steps** | Retrieves active integrations between the specified systems → presents list for user confirmation → triggers sync cycle for each and reports results. |
| **AI assistant output** | A list of integrations that were successfully triggered, along with their IDs and names. |

