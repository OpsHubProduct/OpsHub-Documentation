---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# Create a New Mapping Between Two Systems

## Description

A user wants to create a new field mapping between entity types of two systems — for example, mapping Jira Issues to Rally Defects.

## Example Interaction

| Component | Detail                                                                                                            |
|-----------|-------------------------------------------------------------------------------------------------------------------|
| **User prompt** | "Create a mapping between Jira Issues and Rally Defects for the Alpha (Jira) - Beta (Rally) project integration." |
| **MCP tools invoked** | Mapping planner tool → `get_fields_meta` (for both systems) → `create_mapping`                                    |
| **AI assistant output** | Confirmation of the created mapping with its ID and a summary of the fields mapped                                |

## What the AI Assistant Does

1. Uses the mapping planner tool to determine the correct sequence of steps.
2. Retrieves available fields and their metadata for both entity types.
3. Checks for any existing mappings between the same entity types to avoid duplicates.
4. Presents the proposed mapping to the user for confirmation.
5. Creates the mapping upon confirmation.

## Notes

- Advanced configurations such as XSLT transformations, conflict detection rules, and overwrite settings can also be applied by requesting them in your prompt.