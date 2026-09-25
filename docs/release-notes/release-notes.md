{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}
# New Versions
* Codebeamer: 3.3

# New Entities
* Aha: Approval and Workrequest

# Enhancements
## Common
* OIM MCP Server production rollout with support for a comprehensive set of functionalities.
  * Reconciliation
  * Failure Notification
  * Usage and Metrics Reports
  * Health and diagnostics tools
* For more details, refer to the [MCP documentation](../manage/mcp/getting-started-with-mcp.md).

## DOORS Next Generation
* Enhanced Basic Authentication support for Jazz-enabled DOORS NG, ETM, and EWM to automatically handle the Jazz Authorization Server (JAS) login flow when required, without additional configuration.

## Codebeamer
* Enhanced rich text synchronization for Codebeamer to improve preservation of content structure and formatting, including nested ordered and unordered lists, line breaks, inline styles, tables, colors, and hyperlinks.

# Major Bug Fixes
## Common
* Resolved an issue where the OIM REST API Swagger screen was not loading due to Content Security Policy (CSP) restrictions.

## Azure DevOps Server/Services
* Resolved an issue where mapping could not be saved when the ADO Pipeline entity was mapped with a different entity type.

## Aha
* Resolved a global failure where regular hyperlinks (with an anchor tag) were added in Aha descriptions or comments.
* Resolved an issue where a NullPointerException occurred while synchronizing a To-Do entity whose parent entity was a Goal or Idea entity.
* Resolved an issue where Aha Requirements were not polled during synchronization when Requirements were associated with Features on later pages, particularly when earlier Features had no or fewer Requirements than the configured page size.

## GitHub
* Fixed GitHub app-based authentication issues causing global failures by ensuring expired tokens are properly regenerated after expiry.

## ServiceNow
* Resolved an issue where synchronization resulted in a global failure when an attachment had a size of 0 B.
* Resolved an issue where ServiceNow integrations could not be created or updated through the OIM REST API when authentication override parameters were provided from the API.

## qTest
* Resolved an issue where child Test Cycle relationships were not available in qTest while configuring mapping for Test Cycle.
{% endif %}

{% if "OM4ADO" === visitor.claims.unsigned.product %}
# Major Bug Fixes
* Resolved various Azure DevOps test entity synchronization issues, including requirement-based test suite naming, shared step result handling, and test result parameter and attachment link behavior.
{% endif %}