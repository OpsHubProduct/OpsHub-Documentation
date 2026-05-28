---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

- **Authentication**: Only basic authentication is supported. LDAP and SAML users cannot authenticate via MCP.
  - MCP clients do not support browser-based login flows required by LDAP and SAML.

- **Delete operations are not supported**: Only Read, Create, and Update operations are available via MCP.
  - Deletions are irreversible in <code class="expression">space.vars.OIM</code>. To avoid accidental data loss, deletions must be performed directly from the UI.

- **Updating failed synchronization data is not supported**: The data of a failed sync record cannot be modified via MCP.
  - It contains the original record being transferred at the time of failure. AI-driven changes could unintentionally modify the actual record and cause incorrect updates on the target system.