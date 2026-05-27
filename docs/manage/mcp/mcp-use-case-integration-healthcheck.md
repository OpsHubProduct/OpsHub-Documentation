---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

## Description

To get a complete picture of <code class="expression">space.vars.OIM</code> instance — not just whether integrations are running, but also the machine's memory consumption, disk space, database connection usage, active threads, and whether there are any unresolved failures that need attention. All of this without opening the UI.

## Example Interaction

| Component | Detail |
|-----------|--------|
| **User prompt** | "Give me a full health check of my OIM instance — I want to know the resource usage, how integrations are doing, and if there are any failures I should be worried about." |
| **MCP tools invoked** | `health_checkup_planner` → `get_oim_system_information` → `get_integrations_list` → `get_systems_list` → `get_processing_failures_list` → `get_global_failures_list` → `get_mappings_list` |
| **AI assistant steps** | Fetches instance resource data (RAM allocation, memory used, disk space, DB connections, HTTP threads) → retrieves integrations with entity pair execution statuses, last sync times, and failure counts → retrieves and groups failures by cause. |
| **AI assistant output** | A health dashboard with overall status (HEALTHY / WARNING / CRITICAL), resource summary, integration and failure summaries, and prioritised recommendations. |

## Notes

- You can scope the check to specific systems: _"Health check for integrations between Jira and Rally."_
- To avoid stale results from a previous query in the same session, include "Do not use previously fetched data" in your prompt.