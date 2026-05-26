---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# Trigger Integration Execution On Demand

## Description

Given two configured systems in <code class="expression">space.vars.OIM</code>, a user wants to immediately trigger all active integrations between those systems without navigating the UI.

## Example Interaction

| Component | Detail |
|-----------|--------|
| **User prompt** | "Execute all active integrations between Jira (System ID 2) and HP ALM (System ID 3) right now." |
| **MCP tools invoked** | `get_integrations_list` (filtered by system pair and ACTIVE status) → `execute_status_change` (status: EXECUTE) for each integration |
| **AI assistant output** | A list of integrations that were successfully triggered, along with their IDs and names |

## What the AI Assistant Does

1. Retrieves all active integrations configured between the two specified systems.
2. For each active integration, calls the execute tool to trigger an immediate sync cycle.
3. Confirms which integrations were successfully executed.

## Notes

- Only integrations in **ACTIVE** status can be executed.
- The AI assistant will present the list of integrations it intends to execute and ask for confirmation before proceeding, as execution is a significant operation.