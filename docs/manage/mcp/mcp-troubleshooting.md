---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

## MCP Logs

The <code class="expression">space.vars.OIM</code> MCP server writes its activity to a dedicated log file. The log file captures all incoming MCP requests and tool invocations.

The MCP log file is located at:

```
<OpsHub Installation Directory>\AppData\logs\MCPServer.log
```

**For example** — On a default Windows installation:

```
C:\Program Files\OpsHub\AppData\logs\MCPServer.log
```

> **Note**: The installation directory may differ depending on the path chosen during setup.

### What the Logs Contain

Each log entry follows this format:

```
<Timestamp> <Log Level> [<Thread>] <Class> - <Message>
```

For example:
```
2026-05-27 14:55:22.194+05:30 DEBUG [boundedElastic-3] co.op.mc.McpToolRegistrar - Executing tool=get_schema with arguments={toolName=update_system}
2026-05-27 14:55:40.301+05:30 DEBUG [boundedElastic-3] co.op.mc.McpToolRegistrar - Successfully executed MCP tool: update_system, Tool Call Result: ...
```

Typical entries include:

- **Tool invocations**: Logged  with prefix `Executing tool=<tool_name>` — shows the tool called and the arguments passed
- **Tool results**: Logged  with prefix `Successfully executed MCP tool: <tool_name>` — shows the result returned

## Debugging

- **To verify MCP server started and tools are registered**: Search for `Registering MCP tool` — confirms the MCP server started and all tools are available.
- **To check if an MCP request is being processed**: Search for `Executing tool=<tool_name>` (e.g., `Executing tool=get_integrations_list`) — confirms the request reached the server and processing has begun.
- **To check the result of a processed request**: Search for `Successfully executed MCP tool: <tool_name>` — confirms the request completed and returned a result.
- **To find failures**: Search for `ERROR` or `WARN` in the log.
---

## Common Issues

- [AI Assistant does not connect to MCP Server](#ai-assistant-does-not-connect-to-mcp-server)
- [Authentication Failure](#authentication-failure)
- [Tool calls succeed but return unexpected results](#tool-calls-succeed-but-return-unexpected-results)
- [HTTPS / SSL Certificate Errors](#https--ssl-certificate-errors)

---

### AI Assistant does not connect to MCP Server

**Symptom**: The AI client reports that it cannot connect to the MCP server, or no OpsHub tools appear.

**Resolution**:
1. Verify the MCP endpoint URL is correct: `<OpsHub Integration Manager URL>/OpsHubWS/mcp`
2. Confirm the <code class="expression">space.vars.OIM</code> instance is running and accessible — open it in a browser to verify.
3. Check that no firewall or proxy is blocking the connection to the <code class="expression">space.vars.OIM</code> host and port.
4. In the log file, check whether `Registering MCP tool` entries are present — if absent, the MCP server did not start correctly.

### Authentication Failure

**Symptom**: The AI client connects but operations return authentication or authorization errors.

**Resolution**:
1. Verify the username and password (or Base64-encoded `Authorization` header value) in your client configuration are correct.
2. Confirm the user account is a local <code class="expression">space.vars.OIM</code> user — LDAP and SAML accounts cannot authenticate via MCP.
3. Confirm the user has the required roles and permissions for the operations being attempted.

### Tool calls succeed but return unexpected results

**Symptom**: The AI assistant invokes tools successfully but the data returned seems stale or incorrect.

**Resolution**:
- Add _"Do not use previously fetched data"_ to your prompt. AI assistants may cache tool results within a conversation session, so this forces a fresh query to <code class="expression">space.vars.OIM</code>.

### HTTPS / SSL Certificate Errors

**Symptom**: The MCP client reports an SSL certificate error when connecting to an HTTPS <code class="expression">space.vars.OIM</code> instance.

**Resolution**:
Refer to the [HTTPS Configuration](mcp-configuration.md#https-configuration) section for steps to trust your server's certificate in the MCP client environment.
