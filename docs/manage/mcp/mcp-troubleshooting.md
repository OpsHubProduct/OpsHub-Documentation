---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

## MCP logs

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

> **Tip**: These logs can also be viewed directly from the <code class="expression">space.vars.OIM</code> UI using the **MCP Logs** toggle on the Global Log screen, without needing server file access. Refer to [MCP Logs](../administrator/log-viewer.md#mcp-logs) for details, including the log format, correlation ID, sensitive data masking, and permissions required.

### What the logs contain

Each log entry follows this format:

```
<Timestamp> <Log Level> [<Thread>] <Class> - [User:<username>] [ReqId:<correlation_id>] <Message>
```

The `[User:<username>]` and `[ReqId:<correlation_id>]` prefixes identify the user who made the tool call and a unique correlation ID assigned to that call, which is useful for tracing a single call end-to-end when multiple calls are logged concurrently. See [Correlation ID (ReqId)](../administrator/log-viewer.md#correlation-id-reqid) for more details.

For example:
```
2026-08-13 10:38:26.570+05:30 DEBUG [boundedElastic-1] co.op.mc.McpToolRegistrar - [User:admin] [ReqId:448d8ff2-dab5-4da6-ba8a-24bdde8e57c9] Executing tool=get_schema with arguments={toolName=update_system}
2026-08-13 10:38:26.701+05:30 DEBUG [boundedElastic-1] co.op.mc.McpToolRegistrar - [User:admin] [ReqId:448d8ff2-dab5-4da6-ba8a-24bdde8e57c9] Successfully executed MCP tool: update_system, Tool Call Result: ...
```

Typical entries include:

- **Tool invocations**: Logged  with prefix `Executing tool=<tool_name>` — shows the tool called and the arguments passed
- **Tool results**: Logged  with prefix `Successfully executed MCP tool: <tool_name>` — shows the result returned

> **Note**: Any credential-like values (passwords, tokens, API keys, secrets) present in tool call arguments or results are masked as `********` before being written to the log.

## Debugging

- **To verify MCP server started and tools are registered**: Search for `Registering MCP tool` — confirms the MCP server started and all tools are available.
- **To check if an MCP request is being processed**: Search for `Executing tool=<tool_name>` (e.g., `Executing tool=get_integrations_list`) — confirms the request reached the server and processing has begun.
- **To check the result of a processed request**: Search for `Successfully executed MCP tool: <tool_name>` — confirms the request completed and returned a result.
- **To trace a single tool call end-to-end**: Search the log for its `[ReqId:<id>]` correlation ID — this returns the request, the response, and any error logged for that call. If a tool call fails, the same correlation ID is also included in the error returned to the client.
- **To find failures**: Search for `ERROR` or `WARN` in the log.
---

## Common issues

- [AI assistant does not connect to MCP Server](#ai-assistant-does-not-connect-to-mcp-server)
- [Authentication failure](#authentication-failure)
- [Tool calls succeed but return unexpected results](#tool-calls-succeed-but-return-unexpected-results)
- [HTTPS / SSL certificate errors](#https--ssl-certificate-errors)

---

### AI assistant does not connect to MCP server

**Symptom**: The AI client reports that it cannot connect to the MCP server, or no OpsHub tools appear.

**Resolution**:
1. Verify the MCP endpoint URL is correct: `<OpsHub Integration Manager URL>/OpsHubWS/mcp`
2. Confirm the <code class="expression">space.vars.OIM</code> instance is running and accessible — open it in a browser to verify.
3. Check that no firewall or proxy is blocking the connection to the <code class="expression">space.vars.OIM</code> host and port.
4. In the log file, check whether `Registering MCP tool` entries are present — if absent, the MCP server did not start correctly.

### Authentication failure

**Symptom**: The AI client connects but operations return authentication or authorization errors.

**Resolution**:
1. Verify the username and password (or Base64-encoded `Authorization` header value) in your client configuration are correct.
2. Confirm the user account is a local <code class="expression">space.vars.OIM</code> user — LDAP and SAML accounts cannot authenticate via MCP.
3. Confirm the user has the required roles and permissions for the operations being attempted.

### Tool calls succeed but return unexpected results

**Symptom**: The AI assistant invokes tools successfully but the data returned seems stale or incorrect.

**Resolution**:
- Add _"Do not use previously fetched data"_ to your prompt. AI assistants may cache tool results within a conversation session, so this forces a fresh query to <code class="expression">space.vars.OIM</code>.

### HTTPS / SSL certificate errors

**Symptom**: The MCP client reports an SSL certificate error when connecting to an HTTPS <code class="expression">space.vars.OIM</code> instance.

**Resolution**:
Refer to the [HTTPS Configuration](mcp-configuration.md#https-configuration) section for steps to trust your server's certificate in the MCP client environment.
