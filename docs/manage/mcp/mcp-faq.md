---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

Answers to the questions most commonly asked about the <code class="expression">space.vars.OIM</code> MCP server.

---

## Does the MCP server require any additional configuration?

No additional setup is required on the <code class="expression">space.vars.OIM</code> server. The MCP server ships as part of <code class="expression">space.vars.OIM</code> and is available at `<OpsHub Integration Manager URL>/OpsHubWS/mcp` once your instance is running. There is no separate service to install, start, or maintain.

Three things need to be in place before you can use it:

1. A license that includes the MCP feature. MCP server access is available with the Professional and Ultimate editions. To confirm it is enabled on your instance, navigate to the Footer, click Edition, and check that MCP is listed. See [Get Started](getting-started-with-mcp.md) for details.
2. An <code class="expression">space.vars.OIM</code> user account with the roles and permissions required for the operations you intend to perform. A dedicated user account is recommended, so that MCP activity is easy to identify in audits and access is limited to only what is needed.
3. Configuration on the client side. Your MCP client needs the server URL and your credentials. Credentials can be supplied as an API Key, a Base64-encoded authorization header, or username and password headers. See [Configuration](mcp-configuration.md) for ready-to-use configuration samples for each supported client.

> **Note**: If your instance is configured on HTTPS with a self-signed or internal CA certificate, the certificate must be trusted by your client. See the HTTPS section of [Configuration](mcp-configuration.md).

---

## How does <code class="expression">space.vars.OIM</code> ensure that MCP does not share information outside the customer environment?

The MCP server runs inside your own <code class="expression">space.vars.OIM</code> deployment. It is part of the application you already host, reachable on your own network at your own URL. No <code class="expression">space.vars.OIM</code> data is sent to OpsHub, and no OpsHub-hosted service sits between your AI client and your instance.

Within that boundary, the following controls apply:

- **Every request is authenticated.** The MCP server accepts no anonymous access. Requests carry an API Key or user credentials and are rejected without them.
- **Role-based access control is fully enforced.** MCP does not bypass permissions. A user who cannot perform an operation in the <code class="expression">space.vars.OIM</code> UI cannot perform it through MCP either, and only the data that user is entitled to see is returned.
- **Secrets are never returned.** Passwords, API tokens, and other credentials stored against a system are masked and are not exposed through any MCP tool.
- **Every change is audited.** Configuration changes made through MCP are recorded with **Origin = MCP**, so they can be reviewed and distinguished from changes made through the UI or the Admin API. See [MCP Audits](mcp-audits.md).
- **Destructive operations are not exposed.** Delete operations are not available through any MCP tool, and failed synchronization records cannot be modified.

**One point to be aware of when choosing a client and model.** MCP defines how your AI client talks to <code class="expression">space.vars.OIM</code>; it does not govern what your AI client does afterwards. When the assistant reads data from your instance to answer a question, that data becomes part of its conversation context and is sent to whichever model provider your client is configured to use. If you use a cloud-hosted model, the data in that conversation reaches that provider - exactly as it would if you pasted the same information into a chat window.

This is a property of the AI client you choose, not of the <code class="expression">space.vars.OIM</code> MCP server. If your policy requires that <code class="expression">space.vars.OIM</code> data never leaves your network, use an MCP client configured against a model hosted inside your environment. Your choice of client and model is the control point here, and it is worth settling with your security team before rollout.

---

## Which LLM clients are supported?

The MCP server works with any client that supports the Model Context Protocol over HTTP. The following clients are supported and have ready-to-use configuration samples in [Configuration](mcp-configuration.md):

| Client | Notes |
|--------|-------|
| [Claude Code](https://docs.anthropic.com/en/docs/claude-code/getting-started) | Connects directly over HTTP. Renders returned files as downloads. |
| [Claude Desktop](https://claude.ai/download) | Requires the `mcp-remote` npm package as a bridge, as it does not natively support HTTP-type MCP servers. |
| [Visual Studio Code](https://code.visualstudio.com/) | With a compatible MCP extension, such as GitHub Copilot. Connects directly over HTTP. |
| [Cline](https://github.com/cline/cline) | Uses `mcp-remote` as a bridge. |
| [Continue](https://www.continue.dev/) | Uses `mcp-remote` as a bridge. |

Any other MCP-compatible client with HTTP transport support will also work.

> **Note**: LDAP and SAML users cannot authenticate with the MCP server, on any client. MCP clients do not perform the browser-based login flows those methods require. Use a local <code class="expression">space.vars.OIM</code> user account or an API Key.

> **Note**: Clients differ in how they present a file returned by a tool, which affects the usage and metrics report exports. See [Receiving exported files](mcp-available-tools.md#receiving-exported-files).

---

## How can I tell what actions are being performed through the MCP server?

Through three complementary views, depending on what you need to know:

**For configuration changes - the audit trail.** Every configuration change <code class="expression">space.vars.OIM</code> records carries an **Origin**, and changes made through an MCP client are recorded with **Origin = MCP**. Audits capture the entity changed, the user who changed it, the time, the type of change, and the field-level values that changed. The **Origin** filter is available on every audit screen, so selecting **MCP** shows everything an AI assistant changed. Audits are available for Systems, Integrations, Mappings, Workflows, Users, Roles, Login Servers, Excel Uploads, Job Schedules, API Keys, and Processing Failures. See [MCP Audits](mcp-audits.md).

**For the full record of tool calls - the MCP server log.** Every tool call is written to the MCP server log with the user who made it, the tool invoked, the arguments supplied, and a correlation ID tying the request to its result. This covers read operations as well as changes, so it answers what an assistant *looked at*, which the audit trail does not record. Sensitive values are masked before anything is written. See [Troubleshooting](mcp-troubleshooting.md) for how to access and adjust the log.

**As it happens - the client's own transcript.** MCP clients show each tool call and its result inline in the conversation. This is the quickest way to follow what an assistant is doing while it works, and it is worth watching during your first sessions.

> **Note**: Audit records show the account used to make a change, not the person behind it. If your MCP client uses a shared or service account, every change appears under that account. To attribute changes to individuals, use individual user accounts or user-specific [API Keys](../administrator/api-key-management.md).
