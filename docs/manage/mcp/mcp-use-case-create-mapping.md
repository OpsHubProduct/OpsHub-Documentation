---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

## Description

A user wants to create a new field mapping between entity types of two systems — for example, mapping Jira Issues to Rally Defects.

## Example interaction

| Component | Detail |
|-----------|--------|
| **User prompt** | "Create a mapping between Jira Issues and Rally Defects for the Alpha (Jira) - Beta (Rally) project integration." |
| **MCP tools invoked** | `mapping_planner` → `get_fields_meta` (for both systems) → `create_mapping` |
| **AI assistant steps** | Retrieves field metadata for both entity types → checks for duplicate mappings → presents proposed mapping for user confirmation → creates on confirmation. |
| **AI assistant output** | Confirmation of the created mapping with its ID and a summary of the fields mapped. |

## Notes

- The AI assistant will always check for existing mappings before creating and will warn of potential duplicates.
- Advanced configurations such as XSLT transformations, conflict detection rules, and overwrite settings can be applied by requesting them in your prompt.