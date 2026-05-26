---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# Integration Health Check

## Description

A user wants to get a health overview of all active integrations between two systems — including how many are active, whether any have processing failures, and whether any global errors occurred recently.

## Example Interaction

| Component | Detail |
|-----------|--------|
| **User prompt** | "Give me a health check of all integrations between Jira and Rally. Are there any failures?" |
| **MCP tools invoked** | Health checkup planner tool → `get_integrations_list` → `get_global_failures_list` → `get_processing_failures_list` |
| **AI assistant output** | A structured health summary covering active integrations, failure counts, and any global errors with timestamps |

## Output Includes

- Number of active integrations between the two systems
- Number of active synchronizations
- Processing failure count per integration
- Whether a global error occurred in the last sync cycle, and when
- OIM instance resource usage and system information (CPU, memory, disk) via the system information tool