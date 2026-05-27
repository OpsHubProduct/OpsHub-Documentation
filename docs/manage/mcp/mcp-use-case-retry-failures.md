---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

## Description

A user wants to review the processing failures across integrations and retry them without navigating to the <code class="expression">space.vars.OIM</code> UI. Processing failures are record-level failures — individual items that failed to sync — and can be re-queued for synchronization once the underlying issue is resolved.

## Example Interaction

| Component | Detail |
|-----------|--------|
| **User prompt** | "Show me the processing failures and retry them." |
| **MCP tools invoked** | `get_processing_failures_list` → `retry_processing_failures` |
| **AI assistant steps** | Retrieves failures with messages and item details → presents list for user review → retries on confirmation → reports results. |
| **AI assistant output** | A list of processing failures with failure details, followed by confirmation of which failures were successfully re-queued. |

## Notes

- Global failures can be listed and retrieved for review.
- Updating `eventXML` for processing failures is not supported via MCP tools, as the `eventXML` contains actual source record data and modifying it could lead to unintended mutation of user data.