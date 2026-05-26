---
if: >-
    visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# Overview

<code class="expression">space.vars.OIM</code> provides a rich user interface and REST API for managing integrations. The MCP (Model Context Protocol) server for <code class="expression">space.vars.OIM</code> goes a step further — it enables users and AI assistants to interact with <code class="expression">space.vars.OIM</code> using natural language.

Instead of manually constructing API calls or navigating the UI, you can instruct an AI assistant with queries like _"What systems are configured?"_ or _"Create a mapping between Rally and Jama for Project A and Project B"_, and the MCP server handles the rest.

The <code class="expression">space.vars.OIM</code> MCP server is an HTTP server deployed with your <code class="expression">space.vars.OIM</code> instance — no separate installation is required. It acts as a bridge between any MCP-compatible AI client and the <code class="expression">space.vars.OIM</code> backend, fully respecting existing role-based access control and security policies.

> **Tip**: For best results, it is recommended to also connect the **OpsHub Documentation MCP** alongside the <code class="expression">space.vars.OIM</code> MCP server. This allows your AI assistant to access OpsHub's product documentation — including connector-specific guides, field behaviours, and feature details — providing richer context when generating configurations, mappings, or answering questions about specific connectors and capabilities.

To explore what operations are supported, refer to [MCP Capability Matrix](mcp-capability-matrix.md).  
To get started with sample interactions, refer to [Sample Use Cases](mcp-sample-use-cases.md).

---

# Prerequisites

Following are the prerequisites to use the <code class="expression">space.vars.OIM</code> MCP server:

## Access to <code class="expression">space.vars.OIM</code> Instance

- An active instance of <code class="expression">space.vars.OIM</code> that is accessible from the machine where the MCP client is running.
- URL of the <code class="expression">space.vars.OIM</code> MCP endpoint. Example: `http://10.13.20.20:8989/OpsHubWS/mcp` or `https://10.13.20.20:8443/OpsHubWS/mcp`.
- Valid user credentials (username and password) for the <code class="expression">space.vars.OIM</code> instance.

>**Note**: It is advised to create a **dedicated service user** with appropriate roles and permissions for MCP access, rather than using individual user accounts. This improves traceability and access control. Please refer to [Validate access](#validate-access-to-opshub-integration-manager-instance) for validating this prerequisite.

## MCP License

- MCP server access is available with the **Professional** and **Ultimate** editions of <code class="expression">space.vars.OIM</code>.
- MCP server is **not available** with OM4ADO.

>**Note**: Please refer to [Validate MCP feature](#validate-mcp-feature) to determine whether the MCP feature is enabled on your <code class="expression">space.vars.OIM</code> instance. If you don't have a valid license, please reach out to OpsHub Sales/Support team.

## MCP-Compatible AI Client

The <code class="expression">space.vars.OIM</code> MCP server works with any client that supports the Model Context Protocol over HTTP. Supported clients include:

- [Claude Desktop](https://claude.ai/download)
- [Claude Code](https://docs.anthropic.com/en/docs/claude-code/getting-started)
- [Visual Studio Code](https://code.visualstudio.com/) with a compatible MCP extension (e.g., Continue or Cline)
- [Cline](https://github.com/cline/cline)
- [Continue](https://www.continue.dev/)
- Any other MCP-compatible client that supports HTTP transport

---

# MCP Server Endpoint

The MCP server is deployed as part of the standard <code class="expression">space.vars.OIM</code> installation. No separate installation is required.

The MCP endpoint is available at:

<center><code>&lt;Protocol&gt;://&lt;Host Name or IP of OIM Instance&gt;:&lt;Port&gt;/OpsHubWS/mcp</code></center>

**For example** — If your <code class="expression">space.vars.OIM</code> application URL is `http://10.13.20.20:8989/OIM/`, then the MCP endpoint will be:

```
http://10.13.20.20:8989/OpsHubWS/mcp
```

---

# Authentication

The <code class="expression">space.vars.OIM</code> MCP server supports **Basic Authentication** only.

>**Note**: LDAP and SAML authentication are **not supported** for MCP clients, as MCP clients do not support these authentication mechanisms in general.

Credentials can be passed in one of the following two ways:

## Option 1 — Username and Password as Headers

```json
{
  "servers": {
    "opshub-mcp": {
      "url": "http://localhost:8989/OpsHubWS/mcp",
      "type": "http",
      "headers": {
        "username": "mcpuser",
        "password": "password"
      }
    }
  },
  "inputs": []
}
```

## Option 2 — Base64-Encoded Authorization Header (Recommended)

For improved security, encode your credentials as a Base64 string in the format `username:password` and pass them via the standard `Authorization` header:

```json
{
  "servers": {
    "opshub-mcp": {
      "url": "http://localhost:8989/OpsHubWS/mcp",
      "type": "http",
      "headers": {
        "Authorization": "Basic YWRtaW46cGFzc3dvcmQ="
      }
    }
  },
  "inputs": []
}
```

>**Tip**: To generate the Base64 value, encode `username:password` using any Base64 encoder. For example, `admin:password` encodes to `YWRtaW46cGFzc3dvcmQ=`.

---

# Client Configuration

Below are sample configurations for popular MCP-compatible clients. Replace the URL, credentials, and Base64-encoded string with values specific to your <code class="expression">space.vars.OIM</code> instance.

## Visual Studio Code

{% tabs %}
{% tab title="Authorization Header" %}
```json
{
  "servers": {
    "opshub-mcp": {
      "url": "http://localhost:8989/OpsHubWS/mcp",
      "type": "http",
      "headers": {
        "Authorization": "Basic YWRtaW46cGFzc3dvcmQ="
      }
    }
  },
  "inputs": []
}
```
{% endtab %}
{% tab title="Username & Password Headers" %}
```json
{
  "servers": {
    "opshub-mcp": {
      "url": "http://localhost:8989/OpsHubWS/mcp",
      "type": "http",
      "headers": {
        "username": "mcpuser",
        "password": "password"
      }
    }
  },
  "inputs": []
}
```
{% endtab %}
{% endtabs %}

## Claude Desktop

>**Note**: Claude Desktop does not natively support HTTP-type MCP servers. The `mcp-remote` npm package is required as a bridge. Install it by running `npm install -g mcp-remote`, then use the configuration below.

{% tabs %}
{% tab title="Authorization Header" %}
```json
{
  "mcpServers": {
    "opshub-mcp": {
      "command": "<path-to-your-npm-package>\\mcp-remote.cmd",
      "args": [
        "http://localhost:8989/OpsHubWS/mcp",
        "--header",
        "Authorization: Basic YWRtaW46cGFzc3dvcmQ="
      ]
    }
  }
}
```
{% endtab %}
{% tab title="Username & Password Headers" %}
```json
{
  "mcpServers": {
    "opshub-mcp": {
      "command": "<path-to-your-npm-package>\\mcp-remote.cmd",
      "args": [
        "http://localhost:8989/OpsHubWS/mcp",
        "--header",
        "username: mcpuser",
        "--header",
        "password: password"
      ]
    }
  }
}
```
{% endtab %}
{% endtabs %}

## Claude Code

{% tabs %}
{% tab title="Authorization Header" %}
```json
{
  "mcpServers": {
    "opshub-mcp": {
      "type": "http",
      "url": "http://localhost:8989/OpsHubWS/mcp",
      "headers": {
        "Authorization": "Basic YWRtaW46cGFzc3dvcmQ="
      }
    }
  }
}
```
{% endtab %}
{% tab title="Username & Password Headers" %}
```json
{
  "mcpServers": {
    "opshub-mcp": {
      "type": "http",
      "url": "http://localhost:8989/OpsHubWS/mcp",
      "headers": {
        "username": "mcpuser",
        "password": "password"
      }
    }
  }
}
```
{% endtab %}
{% endtabs %}

## Cline

{% tabs %}
{% tab title="Authorization Header" %}
```json
{
  "mcpServers": {
    "opshub-mcp": {
      "disabled": false,
      "timeout": 60,
      "type": "stdio",
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "http://localhost:8989/OpsHubWS/mcp",
        "--header",
        "Authorization: Basic YWRtaW46cGFzc3dvcmQ="
      ]
    }
  }
}
```
{% endtab %}
{% tab title="Environment Variables" %}
```json
{
  "mcpServers": {
    "opshub-mcp": {
      "timeout": 120,
      "type": "stdio",
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "http://localhost:8989/OpsHubWS/mcp",
        "--header",
        "username: ${USERNAME}",
        "--header",
        "password: ${PASSWORD}"
      ],
      "env": {
        "USERNAME": "mcpuser",
        "PASSWORD": "password"
      }
    }
  }
}
```
{% endtab %}
{% endtabs %}

## Continue

{% tabs %}
{% tab title="Authorization Header" %}
```yaml
mcpServers:
  - name: opshub-mcp
    command: npx
    args:
      - "-y"
      - "mcp-remote"
      - "http://localhost:8989/OpsHubWS/mcp"
      - "--header"
      - "Authorization: Basic YWRtaW46cGFzc3dvcmQ="
    env: {}
```
{% endtab %}
{% tab title="Username & Password Headers" %}
```yaml
mcpServers:
  - name: opshub-mcp
    command: npx
    args:
      - "-y"
      - "mcp-remote"
      - "http://localhost:8989/OpsHubWS/mcp"
      - "--header"
      - "username: mcpuser"
      - "--header"
      - "password: password"
    env: {}
```
{% endtab %}
{% endtabs %}

---

# Logs

MCP server activity is captured in a dedicated log file, separate from the main <code class="expression">space.vars.OIM</code> application logs. The MCP log file is located at:

```
C:\Program Files\OpsHub\AppData\logs\MCPServer.log
```

Use these logs to diagnose connectivity issues, authentication failures, or unexpected tool behaviour during MCP sessions.

---

# Known Limitations

1. **Authentication**: Only Basic Authentication is supported. LDAP and SAML users cannot authenticate with the MCP server.
2. **Delete Operations**: Delete operations are not supported via MCP tools by design. Only Read, Create, and Update operations are available.

---

# Appendix

## Validate MCP Feature

To check whether the MCP feature is enabled in <code class="expression">space.vars.OIM</code> or not, please perform the below steps:

1. [Login](../../getting-started/logging-in.md) to <code class="expression">space.vars.OIM</code> with the valid <code class="expression">space.vars.OIM</code> user credentials.
2. Navigate to the Footer and find the **Edition** value.
3. Click on the Edition value of the <code class="expression">space.vars.OIM</code>.
4. Please make sure the **MCP** feature is enabled.

>**Note**: If this feature is disabled, and you have the license in which this feature is available, then please [install](Managing_Licenses) the correct license. If you don't have a valid license, please reach out to OpsHub Sales/Support team for receiving the appropriate license.

>**Note**: If <code class="expression">space.vars.OIM</code> is configured on HTTPS, then SSL certificates need to be trusted in your MCP client environment. For clients using `mcp-remote`, certificate handling may need to be configured depending on your OS and Node.js setup.
