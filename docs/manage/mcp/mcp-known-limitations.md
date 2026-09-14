---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

- **MCP currently supports only basic authentication.**
  - LDAP and SAML-based authentication methods are not supported, as MCP clients do not support browser-based authentication flows required by these mechanisms.

- **Delete operations are not supported via MCP.**
  - Deletions are irreversible and must be performed directly through the <code class="expression">space.vars.OIM</code> UI to ensure controlled execution and prevent unintended data loss.

- **Modification of failed synchronization records [failure XML] is not supported via MCP.**
  - These records contain the original data captured during synchronization. Allowing updates through AI-driven or automated interactions could unintentionally alter the original synchronization data and result in incorrect updates on the target system.

- **Deletion of failure notifications is not supported via MCP.**
  - A failure notification can be created, read, and updated through MCP. To remove one, use the <code class="expression">space.vars.OIM</code> UI.

- **How an exported report is presented depends on your MCP client.**
  - The usage and metrics reports are returned over MCP as file content. Some clients render an attached file and save it for you; others display only the text of a tool result and do not surface attachments. Each export is therefore returned with a text summary and, where available, a download link alongside the file itself, so the report is retrievable on any client. See [Receiving exported files](mcp-available-tools.md#receiving-exported-files).

- **Reconciliation cannot be started unless its prerequisites are already in place.**
  - An integration must be inactive, reconcile rules must be configured on the field mappings of its entity pairs, and a reconciliation workflow must exist before the integration can be switched into reconciliation mode. Reconcile rules are configured on the **mapping** and can be set through MCP; the reconciliation workflow must be uploaded from the <code class="expression">space.vars.OIM</code> UI.

- **Reconciliation applies to comments, attachments, and links as well as fields.**
  - Where these are configured on the mapping, a reconciliation reconciles them along with the mapped fields. They cannot be excluded for a single reconciliation run — they are mapping settings shared with normal synchronization, so disabling them also changes how the integration syncs afterwards.
