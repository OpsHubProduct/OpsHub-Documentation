---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

- **MCP currently supports only basic and API key based authentication.**
  - LDAP and SAML-based authentication methods are not supported, as MCP clients do not support browser-based authentication flows required by these mechanisms.

- **Delete operations are not supported via MCP.**
  - Deletions are irreversible and must be performed directly through the <code class="expression">space.vars.OIM</code> UI to ensure controlled execution and prevent unintended data loss.

- **Modification of failed synchronization records [failure XML] is not supported via MCP.**
  - These records contain the original data captured during synchronization. Allowing updates through AI-driven or automated interactions could unintentionally alter the original synchronization data and result in incorrect updates on the target system.
