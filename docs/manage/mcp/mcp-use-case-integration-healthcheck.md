---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# Integration Manager Health Check

## Description

A user wants to get a health overview of the <code class="expression">space.vars.OIM</code> instance — including active integrations, entity pair execution statuses, processing and global failures, and instance resource usage — without navigating the UI.

## Example Interaction

| Component | Detail                                                                                                                                                                                     |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **User prompt** | "Perform a health check on my OIM instance."                                                                                                                                               |
| **MCP tools invoked** | `health_checkup_planner` → `get_oim_system_information` → `get_integrations_list` → `get_systems_list` → `get_processing_failures_list` → `get_global_failures_list` → `get_mappings_list` |
| **AI assistant output** | Health Checkup Analysis with overall health status, integration and failure summaries, instance resource usage, and prioritised recommendations                                            |

## What the AI Assistant Does

1. Calls the health checkup planner to determine the sequence of steps.
2. Collects instance profile data: memory, disk, database connections, and thread pool usage.
3. Retrieves all integrations with entity pair execution statuses, last sync times, and failure counts.
4. Retrieves processing and global failures, grouped by cause.
5. Presents a health dashboard (HEALTHY / WARNING / CRITICAL) with recommendations.

## Notes

- You can scope the check to specific systems: _"Health check for integrations between Jira and Rally."_
- To avoid stale results from a previous query in the same session, include "Do not use previously fetched data" in your prompt.