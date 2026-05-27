---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# Query Configured Systems and Project Pairs

## Description

A user wants to find out which systems are configured in <code class="expression">space.vars.OIM</code> and which project pairs are synchronizing between two specific systems.

## Example Interaction

| Component | Detail |
|-----------|--------|
| **User prompt** | "What systems are configured in OIM? And what projects are integrated between System A and System B?" |
| **MCP tools invoked** | `get_systems_list` → `get_integrations_list` → extract project pairs from integration details |
| **AI assistant steps** | Retrieves all configured systems → filters integrations by the two specified systems → extracts project pairs and sync directions. |
| **AI assistant output** | A summary of all configured systems, followed by a list of project pairs with sync directions between the two specified systems. |

## Sample Output

| System Pair | Project (System A) | Direction | Project (System B) |
|-------------|--------------------|-----------|--------------------|
| Jira ↔ Rally | Project Alpha | BIDIRECTIONAL | Rally Project 1 |
| Jira ↔ Rally | Project Beta | FORWARD | Rally Project 2 |

> **Tip**: To avoid stale results from a previous query in the same session, include "Do not use previously fetched data" in your prompt.