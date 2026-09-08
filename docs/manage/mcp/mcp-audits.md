---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

## Overview

AI assistants can now create, update, and configure your integrations directly through MCP - which raises a natural question: what did the AI actually change, and when? **MCP Audits** answer that.

<code class="expression">space.vars.OIM</code> records an audit entry for every configuration change made in the application, capturing the entity that was changed, the user who changed it, when the change was made, the type of change, and the field-level values that changed. Every audit entry also records the **Origin** of the change - the channel it came through. Since the same user can make changes from the <code class="expression">space.vars.OIM</code> UI, the Admin API, or an MCP client, **Origin** makes it clear which one was used, so changes made by an AI assistant through MCP can always be told apart from the rest.

Audits are available for all audited entities, such as **Systems**, **Integrations**, **Mappings**, **Workflows**, **Users**, **Roles**, **Login Servers**, **Excel Uploads**, **Job Schedules**, **API Keys**, and **Processing Failures**. To view them, click the audit icon on the top right corner of the respective list view.

<p align="center">
  <img src="../../assets/mcp-audit-origin.png" width="1000"/>
</p>

---

## Origin Values

| Value   | Description                                                                                 |
|---------|---------------------------------------------------------------------------------------------|
| **UI**  | The change was made from the <code class="expression">space.vars.OIM</code> user interface.  |
| **API** | The change was made through the [Admin API](../api/getting-started-with-api.md).             |
| **MCP** | The change was made through an [MCP](getting-started-with-mcp.md) client.                    |

---

## Filter and Sort by Origin

- The **Origin** filter is available on every audit screen. Select a value to view only the changes made through that channel - for example, select **MCP** to review everything an AI assistant changed. Click **Reset** to restore the default view.
- The **Origin** column can be sorted like the other columns, which is useful to group all the changes of a channel together.

---

## Important Notes

- **Historical audit records are displayed with Origin as UI** because the source channel was not captured before this <code class="expression">space.vars.OIM</code> version upgrade. To maintain a complete and consistent audit trail, existing audit entries are backfilled with the value **UI**. Changes made after the upgrade correctly capture and display their actual **Origin**, such as **UI**, **Admin API**, or **MCP**.
- Audit attribution is based on the credentials used, not the individual behind them. So if an MCP client or the Admin API is accessed using a shared or a service account, that account is recorded as the **Author** for every change made through it. Use individual user accounts or per-user [API Keys](../administrator/api-key-management.md) where attributing a change to a specific person matters.
