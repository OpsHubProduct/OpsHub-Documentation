---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

## MCP Logs

The <code class="expression">space.vars.OIM</code> MCP server writes its activity to a dedicated log file. The log file captures all incoming MCP requests, tool invocations, authentication events, and any errors or exceptions that occur during MCP sessions.

The MCP log file is located at:

```
<OpsHub Installation Directory>\AppData\logs\MCPServer.log
```

**For example** — On a default Windows installation:

```
C:\Program Files\OpsHub\AppData\logs\MCPServer.log
```

> **Note**: The installation directory may differ depending on the path chosen during setup. If you cannot find the log at the path above, check the directory where <code class="expression">space.vars.OIM</code> is installed.

### What the Logs Contain

Each log entry includes a timestamp, log level, and a description of the event. Typical entries include:

- Incoming MCP tool call requests, identified by entries containing `MCP Request` or the tool name being invoked
- Tool execution results and any validation errors
- Exceptions or unexpected errors during request processing

### Finding Relevant Entries

To locate entries related to a specific request or session:

- Search for the **tool name** (e.g., `get_integrations_list`, `create_mapping`) to find log lines for a specific operation
- Search for `ERROR` or `WARN` to quickly identify failures

---

## Common Issues

### AI Assistant Does Not Connect to MCP Server

**Symptom**: The AI client reports that it cannot connect to the MCP server, or no OpsHub tools appear.

**Resolution**:
1. Verify the MCP endpoint URL is correct: `<OpsHub Integration Manager URL>/OpsHubWS/mcp`
2. Confirm the <code class="expression">space.vars.OIM</code> instance is running and accessible from the machine where the MCP client is running — open <code class="expression">space.vars.OIM</code> in a browser to verify.
3. Check that no firewall or proxy is blocking the connection to the <code class="expression">space.vars.OIM</code> host and port.
4. Review the MCP log file for connection or startup errors.

### Authentication Failure

**Symptom**: The AI client connects but operations return authentication or authorization errors.

**Resolution**:
1. Verify the username and password (or Base64-encoded `Authorization` header value) in your client configuration are correct.
2. Confirm the user account exists in <code class="expression">space.vars.OIM</code> and is a local user — LDAP and SAML accounts cannot authenticate via MCP.
3. Confirm the user has the required roles and permissions for the operations being attempted.

### Tool Calls Succeed but Return Unexpected Results

**Symptom**: The AI assistant invokes tools successfully but the data returned seems stale or incorrect.

**Resolution**:
- Add _"Do not use previously fetched data"_ to your prompt. AI assistants may cache tool results within a conversation session, so this forces a fresh query to <code class="expression">space.vars.OIM</code>.

### HTTPS / SSL Certificate Errors

**Symptom**: The MCP client reports an SSL certificate error when connecting to an HTTPS <code class="expression">space.vars.OIM</code> instance.

**Resolution**:  
Refer to the [HTTPS Configuration](mcp-configuration.md#https-configuration) section for steps to trust your server's certificate in the MCP client environment.
