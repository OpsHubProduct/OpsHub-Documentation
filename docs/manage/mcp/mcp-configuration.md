---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---


This page covers how to authenticate with the <code class="expression">space.vars.OIM</code> MCP server and how to configure popular MCP-compatible clients.

---

# Authentication

The <code class="expression">space.vars.OIM</code> MCP server supports the following authentication methods. Credentials are passed as part of the MCP client configuration headers.

> **Note**: LDAP and SAML users cannot authenticate with the MCP server. This is because MCP clients do not perform browser-based or redirect-based login flows that LDAP and SAML require. Use a local <code class="expression">space.vars.OIM</code> user account for MCP access.

Credentials can be passed in one of the following ways in your client configuration:

## Option 1 — API Key header (recommended)

Use an API Key generated from the <code class="expression">space.vars.OIM</code> UI. This is the most secure option as the key is dedicated, revocable, and keeps your user credentials out of configuration files entirely. Pass it via the `x-api-key` header:

```json
{
  "servers": {
    "opshub-mcp": {
      "url": "<OpsHub Integration Manager URL>/OpsHubWS/mcp",
      "type": "http",
      "headers": {
        "x-api-key": "<your-api-key>"
      }
    }
  },
  "inputs": []
}
```

Alternatively, you can pass the API Key via the `Authorization` header:

```json
{
  "servers": {
    "opshub-mcp": {
      "url": "<OpsHub Integration Manager URL>/OpsHubWS/mcp",
      "type": "http",
      "headers": {
        "Authorization": "ApiKey <your-api-key>"
      }
    }
  },
  "inputs": []
}
```

> **Tip**: To generate an API Key, go to **Administration → API key** in <code class="expression">space.vars.OIM</code>. See [API Key Management](api-key-management.md) for step-by-step instructions.

## Option 2 — base64-encoded authorization header

Encode your credentials as a Base64 string in the format `username:password` and pass them via the standard `Authorization` header. This avoids exposing plain-text credentials in your configuration file.

```json
{
  "servers": {
    "opshub-mcp": {
      "url": "<OpsHub Integration Manager URL>/OpsHubWS/mcp",
      "type": "http",
      "headers": {
        "Authorization": "Basic <Base64 encoded username:password>"
      }
    }
  },
  "inputs": []
}
```

> **Tip**: To generate the Base64 value, encode `username:password` using any Base64 encoder. For example, `admin:password` encodes to `YWRtaW46cGFzc3dvcmQ=`.

## Option 3 — username and password as headers

```json
{
  "servers": {
    "opshub-mcp": {
      "url": "<OpsHub Integration Manager URL>/OpsHubWS/mcp",
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

---

# Client configuration

Below are sample configurations for popular MCP-compatible clients. Replace the URL and credentials with values specific to your <code class="expression">space.vars.OIM</code> instance.

## Visual Studio Code

{% tabs %}
{% tab title="API Key" %}
```json
{
  "servers": {
    "opshub-mcp": {
      "url": "<OpsHub Integration Manager URL>/OpsHubWS/mcp",
      "type": "http",
      "headers": {
        "x-api-key": "<your-api-key>"
      }
    }
  },
  "inputs": []
}
```
{% endtab %}
{% tab title="Authorization Header" %}
```json
{
  "servers": {
    "opshub-mcp": {
      "url": "<OpsHub Integration Manager URL>/OpsHubWS/mcp",
      "type": "http",
      "headers": {
        "Authorization": "Basic <Base64 encoded username:password>"
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
      "url": "<OpsHub Integration Manager URL>/OpsHubWS/mcp",
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

> **Note**: Claude Desktop does not natively support HTTP-type MCP servers. The `mcp-remote` npm package is required as a bridge. Install it by running `npm install -g mcp-remote`, then use the configuration below.

{% tabs %}
{% tab title="API Key" %}
```json
{
  "mcpServers": {
    "opshub-mcp": {
      "command": "<path-to-npm-global-bin>\\mcp-remote.cmd",
      "args": [
        "<OpsHub Integration Manager URL>/OpsHubWS/mcp",
        "--header",
        "x-api-key: <your-api-key>"
      ]
    }
  }
}
```
{% endtab %}
{% tab title="Authorization Header" %}
```json
{
  "mcpServers": {
    "opshub-mcp": {
      "command": "<path-to-npm-global-bin>\\mcp-remote.cmd",
      "args": [
        "<OpsHub Integration Manager URL>/OpsHubWS/mcp",
        "--header",
        "Authorization: Basic <Base64 encoded username:password>"
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
      "command": "<path-to-npm-global-bin>\\mcp-remote.cmd",
      "args": [
        "<OpsHub Integration Manager URL>/OpsHubWS/mcp",
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
{% tab title="API Key" %}
```json
{
  "mcpServers": {
    "opshub-mcp": {
      "type": "http",
      "url": "<OpsHub Integration Manager URL>/OpsHubWS/mcp",
      "headers": {
        "x-api-key": "<your-api-key>"
      }
    }
  }
}
```
{% endtab %}
{% tab title="Authorization Header" %}
```json
{
  "mcpServers": {
    "opshub-mcp": {
      "type": "http",
      "url": "<OpsHub Integration Manager URL>/OpsHubWS/mcp",
      "headers": {
        "Authorization": "Basic <Base64 encoded username:password>"
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
      "url": "<OpsHub Integration Manager URL>/OpsHubWS/mcp",
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
{% tab title="API Key" %}
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
        "<OpsHub Integration Manager URL>/OpsHubWS/mcp",
        "--header",
        "x-api-key: <your-api-key>"
      ]
    }
  }
}
```
{% endtab %}
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
        "<OpsHub Integration Manager URL>/OpsHubWS/mcp",
        "--header",
        "Authorization: Basic <Base64 encoded username:password>"
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
        "<OpsHub Integration Manager URL>/OpsHubWS/mcp",
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
{% tab title="API Key" %}
```yaml
mcpServers:
  - name: opshub-mcp
    command: npx
    args:
      - "-y"
      - "mcp-remote"
      - "<OpsHub Integration Manager URL>/OpsHubWS/mcp"
      - "--header"
      - "x-api-key: <your-api-key>"
    env: {}
```
{% endtab %}
{% tab title="Authorization Header" %}
```yaml
mcpServers:
  - name: opshub-mcp
    command: npx
    args:
      - "-y"
      - "mcp-remote"
      - "<OpsHub Integration Manager URL>/OpsHubWS/mcp"
      - "--header"
      - "Authorization: Basic <Base64 encoded username:password>"
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
      - "<OpsHub Integration Manager URL>/OpsHubWS/mcp"
      - "--header"
      - "username: mcpuser"
      - "--header"
      - "password: password"
    env: {}
```
{% endtab %}
{% endtabs %}

---

# HTTPS configuration

If your <code class="expression">space.vars.OIM</code> instance is configured on HTTPS, your MCP client must trust the SSL certificate used by the server.

- For clients that use `mcp-remote` as a bridge (Claude Desktop, Cline, Continue), the certificate must be trusted by your OS certificate store or Node.js environment.
- If you are using a self-signed or internal CA certificate, you may need to explicitly add it to Node.js using the `NODE_EXTRA_CA_CERTS` environment variable:

  ```bash
  NODE_EXTRA_CA_CERTS=/path/to/your/certificate.pem
  ```

- For VS Code and Claude Code, which connect directly over HTTP/HTTPS, ensure the certificate is trusted at the OS level.

> **Note**: If you encounter SSL errors, contact your system administrator to obtain the correct certificate file and follow the steps above.
