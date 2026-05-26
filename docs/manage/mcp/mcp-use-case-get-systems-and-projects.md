---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# Query Configured Systems and Project Pairs

## Description

Given a <code class="expression">space.vars.OIM</code> instance with multiple systems configured, a user wants to find out which systems are available and which project pairs are actively synchronizing between two specific systems.

## Example Interaction

| Component | Detail                                                                                                                                 |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------|
| **User prompt** | "What systems are configured in OIM? And what project are integrated between System A and System B?"                             |
| **MCP tools invoked** | `get_systems_list` → `get_integrations_list` → extract project pairs from integration details                                          |
| **AI assistant output** | A summary of all configured systems, followed by a list of active project pairs (with sync direction) between the two specified systems |

## What the AI Assistant Does

1. Calls the system list tool to retrieve all configured endpoints.
2. Filters integrations by the two specified systems.
3. Extracts and presents the project pairs and sync directions configured in each active integration.

## Sample Output Could Look like

| System Pair | Project (System A) | Direction     | Project (System B) |
|-------------|--------------------|---------------|--------------------|
| Jira ↔ Rally | Project Alpha | BIDIRECTIONAL | Rally Project 1 |
| Jira ↔ Rally | Project Beta | FORWARD       | Rally Project 2 |

> **Tip**: To avoid stale results from a previous query in the same session, include "Do not use previously fetched data" in your prompt.