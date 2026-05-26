---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# List and Retry Processing Failures

## Description

A user wants to review the current processing failures across integrations and retry those that are eligible, without navigating to the <code class="expression">space.vars.OIM</code> UI.

## Example Interaction

| Component | Detail |
|-----------|--------|
| **User prompt** | "Show me the processing failures and retry them." |
| **MCP tools invoked** | `get_processing_failures_list` → `retry_processing_failures` |
| **AI assistant output** | A list of current processing failures with failure messages and item details, followed by confirmation of which failures were successfully retried |

## What the AI Assistant Does

1. Retrieves all processing failures.
2. Presents the failures with their messages, item IDs, and timestamps.
3. Asks for user confirmation before retrying.
4. Calls the retry tool for the selected failures and reports results.

## Notes

- Global failures can be listed and retrieved for review.
- Updating `eventXML` for processing failures is not supported via MCP tools.