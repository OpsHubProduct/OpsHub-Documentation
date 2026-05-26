{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}

<table data-view="cards" data-full-width="false">
  <thead>
    <tr>
      <th align="center" data-card-cover></th>
      <th data-hidden data-card-target data-type="content-ref"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center">⚙️ <strong>Administration</strong></td>
      <td><a href="administrator.md">Administration</a></td>
    </tr>
    <tr>
      <td align="center">🧰 <strong>Advanced Utilities</strong></td>
      <td><a href="advanced-utilities.md">Advanced Utilities</a></td>
    </tr>
    <tr>
      <td align="center">🧩 <strong>APIs</strong></td>
      <td><a href="api.md">APIs</a></td>
    </tr>
    <tr>
      <td align="center">🤖 <strong>MCP Server</strong></td>
      <td><a href="mcp.md">MCP Server</a></td>
    </tr>
    <tr>
      <td align="center">⬆️ <strong>Upgrade</strong></td>
      <td><a href="upgrade-index.md">Upgrade</a></td>
    </tr>
  </tbody>
</table>

{% endif %}

{% if "OM4ADO" === visitor.claims.unsigned.product %}

<table data-view="cards" data-full-width="false">
  <thead>
    <tr>
      <th align="center" data-card-cover></th>
      <th data-hidden data-card-target data-type="content-ref"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center">⚙️ <strong>License Installation</strong></td>
      <td><a href="administrator/license_installation.md">License Installation</a></td>
    </tr>
    <tr>
      <td align="center">🧰 <strong>Advanced Utilities</strong></td>
      <td><a href="advanced-utilities.md">Advanced Utilities</a></td>
    </tr>
    <tr>
      <td align="center">⬆️ <strong>Upgrade</strong></td>
      <td><a href="upgrade-index.md">Upgrade</a></td>
    </tr>
  </tbody>
</table>

{% endif %}