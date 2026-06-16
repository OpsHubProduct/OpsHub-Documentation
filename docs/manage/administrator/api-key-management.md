# API Key Management

## What Are API Keys?

API Keys give you a secure, dedicated way to connect your scripts and automated systems to the Admin APIs and MCP (Model Context Protocol) integrations — no need to share your username and password.

Think of an API Key as a separate credential created just for programmatic access. You can generate one from the UI, use it in your integrations, and revoke it at any time if it's no longer needed.

With API Keys, you can:

- Generate keys directly from the UI.
- Use them to authenticate Admin API and MCP requests.
- Update a key's name or expiry date while it's active.
- Revoke a key instantly when it's no longer needed.
- Track and audit all key activity from one place.

> **Good to know:** API Keys are an *additional* way to authenticate — they don't replace or affect your existing Basic Authentication setup. After an upgrade, everything works exactly as before, and no migration is needed.

---

## Why Use API Keys?

Previously, automating Admin API calls meant embedding a user's username and password in scripts. That comes with some real risks:

- Credentials can be accidentally exposed in code or logs.
- Rotating passwords is disruptive and error-prone.
- Long-lived passwords create ongoing security exposure.

API Keys are purpose-built for automation: they're separate from user credentials, easy to revoke, and scoped to the user who created them.

---

## Before You Begin

- **Edition requirement:** API Keys are available on the **Professional** and **Ultimate** editions only.

---

## Finding the API Key Section

1. Go to **Administration**.
2. Select **API key** from the menu.

You'll land on the **API key list view**, which shows all keys you've created along with the following details:

| Column | What it shows                                               |
|--------|-------------------------------------------------------------|
| **Name** | The name you gave the key when creating it.                 |
| **Created on** | When the key was created.                                   |
| **Expires on** | When the key is set to expire.                              |
| **Last accessed** | The last time the key was used successfully.                |
| **Status** | Whether the key is **Active**, **Expired**, or **Revoked**. |
| **Action** | Option to revoke the key.                                   |

<p align="center">
  <img src="../../assets/APIKey_List_View.png" width="1000"/>
</p>

> **Note:** The actual key value is never shown here — only its metadata. This is by design to keep your keys secure.

---

## Generating an API Key

1. Go to **Administration → API key**.
2. Click the **+** button in the top right corner to open the **Create API Key** form.
3. Fill in the following fields:
    - **Name** *(required)* — Give the key a clear, meaningful name so you can identify it later.
    - **Expires on** *(required)* — Set a future expiry date. The date must be in the future and no more than **1 year** from today.

<p align="center">
  <img src="../../assets/APIKey_Create_Form.png" width="1000"/>
</p>

4. Click **Save**. The system generates a cryptographically secure key.
5. Your new key is displayed **one time only** in a pop-up. Click **Copy** to copy it, then store it somewhere safe (a secrets manager or password vault works great).

<p align="center">
  <img src="../../assets/APIKey_Copy_Modal.png" width="600"/>
</p>

6. Click **Close** to go back to the key list. The new key appears there, but the key value itself is no longer visible.

> **Important:** Once you close this pop-up, the key value cannot be retrieved again. If you lose it, you'll need to generate a new one.

---

## Using an API Key

Once generated, your API Key can authenticate requests to both the **Admin API** and **MCP** endpoints.

### How to Pass the Key

Include the key in **one** of the following request headers:

```
x-api-key: <api-key>
```

or

```
Authorization: ApiKey <api-key>
```

### How Authentication Works

1. Your client sends a request with the API Key in the header.
2. The system checks that the key exists, is active, and hasn't expired.
3. If everything checks out, the request goes through — and the **Last accessed** timestamp updates automatically.
4. If the key is invalid, expired, or revoked, you'll get a **401 Unauthorized** response:

```json
{
  "errorMessage": "Authentication failed. Valid credentials are required to access this resource.",
  "stackTrace": null
}
```

> **Permissions note:** An API Key carries the same permissions as the user who created it. It can't be used to do anything beyond what that user is allowed to do.

---

## Editing an API Key

You can update the name or expiry date of any **active** key.

1. Go to **Administration → API key**.
2. Click on an active key to open its details.
3. Click the edit button in the top right.
4. Update the **Name** and/or **Expires on** fields. The same validation rules apply as when creating a key.
5. Click **Save**.

<p align="center">
  <img src="../../assets/APIKey_Edit_Form.png" width="1000"/>
</p>

> **Note:** Expired or revoked keys cannot be edited. The edit option will be disabled for those keys.

---

## Revoking an API Key

Revoke a key any time it's no longer needed.

1. Go to **Administration → API key**.
2. Click the **✕** button next to the key you want to revoke in the **Action** column.
3. A confirmation prompt will appear: *"API key with name \<api-key-name\> will be permanently revoked. This action is irreversible."*
4. Click **Yes, revoke it!** to confirm.

<p align="center">
  <img src="../../assets/APIKey_Revoke_Confirmation.png" width="600"/>
</p>

After revoking:

- The key remains visible in the list with a **Revoked** status — it's not deleted.
- Any requests using that key will immediately start returning **401 Unauthorized**.
- The key cannot be reactivated. If you need access again, generate a new key.

---

## API Key Statuses

| Status | What it means |
|--------|---------------|
| **Active** | The key is valid and working. |
| **Expired** | The expiry date has passed. The key no longer works. This happens automatically. |
| **Revoked** | You (or an admin) manually revoked the key. It can't be restored or reused. |

---

## Auditing API Key Activity

All API Key actions are logged and viewable from the **API key audits** screen. Each entry captures the **Name**, **Author**, **Change Time**, **Revision Type**, and any changed field values (old and new).

Three types of events are tracked:

- **Create** — logs the key name and expiry date at time of creation.
- **Update** — logs what changed (name and/or expiry date).
- **Revoke** — logs the status change from Active to Revoked.

---

## Access and Permissions

- Any authenticated user can create and manage their own API Keys, regardless of role.
- You can only see and manage keys you created — not keys belonging to other users.
- A key inherits your permissions; it can't be used for anything you couldn't do yourself.
- By default, **Super Admins** can view and manage all users' API Keys and audit logs. Users with the **User Management – Write** permission in a custom role can also do this. See [User Access Control](user-access-control.md) for details.

---

## Things to Keep in Mind

| Behavior | Details |
|----------|---------|
| **Key is shown only once** | Copy and save it immediately after creation — it can't be retrieved again. |
| **Revocation is instant and permanent** | Once revoked, the key stops working immediately and cannot be restored. Generate a new one if needed. |
| **No in-place key rotation** | To rotate a key, generate a new one and revoke the old one manually. |
| **No per-key permission scoping** | Keys always inherit the full permissions of the user who created them. |
| **Keys are revoked when a user is deleted** | If a user account is deleted, all their API Keys are automatically revoked and cannot be reactivated. |