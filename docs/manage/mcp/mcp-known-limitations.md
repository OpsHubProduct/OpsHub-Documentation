---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# Known Limitations

## Authentication

Currently, only basic authentication is supported for the MCP server. LDAP and SAML users cannot authenticate via MCP.

This is because MCP clients communicate directly over HTTP headers and do not support browser-based redirect flows, which are required for LDAP and SAML login. To use MCP, create a local <code class="expression">space.vars.OIM</code> user account with the required roles.

## Delete Operations Not Supported

Delete operations (e.g., deleting a system, mapping, or integration) are not available as MCP tools. Only Read, Create, and Update operations are supported.

Delete operations are excluded because they are **irreversible** — there is no undo or restore mechanism in <code class="expression">space.vars.OIM</code> once a resource is deleted. To prevent accidental data loss through an AI-driven interface, delete operations must be performed directly through the <code class="expression">space.vars.OIM</code> UI or REST API, where the user explicitly initiates and confirms the action.

## Processing Failure Event XML

Updating the `eventXML` field for processing failures is not supported via MCP tools. The `eventXML` contains the actual data that was being synchronized at the time of failure. Allowing an AI assistant to modify this field could lead to unintended mutation of actual data, which may corrupt the record being synced or produce incorrect results on the target system.