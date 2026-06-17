
## Overview

API Keys provide a secure, dedicated credential for programmatic access to the [Admin APIs](../api/getting-started-with-api.md) and [MCP integrations](../mcp/getting-started-with-mcp.md) — without sharing a user's username and password.

> **Note:** API Key authentication is an additional mechanism and does not replace existing Basic Authentication.

* **License** 
  * API Keys are available on the **Professional** and **Ultimate** editions only. To verify your edition, refer to the value shown in the footer of <code class="expression">space.vars.OIM</code>.
* **API Key Permissions**
  * An API Key inherits the permissions of the user who created it — it cannot be used to perform any action beyond what that user is authorized to do.
* **Where to Generate**
  * API Keys are generated and managed from the <code class="expression">space.vars.OIM</code> UI under **Administration → API key**, and can be revoked at any time. Refer to [Generating an API Key](#generating-an-api-key) for the steps.

---

## Accessing API Key Management

1. Click **Administration**.
2. Select **API key** from the options in the left pane. The **API key** list view opens, showing all keys you have created.

<p align="center">
  <img src="../../assets/APIKey_List_View.png" width="1000"/>
</p>

The list displays the following details for each key:

| Column            | Description                                                            |
|-------------------|------------------------------------------------------------------------|
| **Name**          | The unique label provided when creating the key.                       |
| **Created By**    | The user who created the key.                                          |
| **Created on**    | The timestamp when the key was created.                                |
| **Expires on**    | The configured expiry datetime of the key.                             |
| **Last accessed** | The timestamp of the last successful use of the key.                   |
| **Status**        | The current state of the key: **Active**, **Expired**, or **Revoked**. |
| **Action**        | Option to revoke the key.                                              |

> **Note:** For security reasons, the actual API Key value is shown only once at the time of generation and is never displayed again. This list shows only the key's details, not the key value itself.

---

## Generating an API Key

1. Navigate to **Administration → API key**.
2. Click the **+** button on the top right corner of the screen.

3. The **Create API Key** form opens. Fill in the following details:
   - **Name** *(required)* — A unique name to identify the key.
   - **Expires on** *(required)* — A future expiry datetime, no more than **1 year** from the current date. 
   - Refer to [Field Validations](#field-validations) for the rules and warning messages.

<p align="center">
  <img src="../../assets/APIKey_Create_Form.png" width="1000"/>
</p>

4. Click **Save**. The system generates a cryptographically secure API Key.

5. The generated key is displayed **one time only** in a pop-up. Click **Copy** to copy the key and store it securely.

<p align="center">
  <img src="../../assets/APIKey_Copy_Modal.png" width="600"/>
</p>

6. Click **Close** to dismiss the pop-up. You are redirected back to the API key list view where the newly created key is visible.

{% hint style="warning" %}
**Important:** For security reasons, the API Key value is shown **only once**. After the pop-up is dismissed, the key value cannot be retrieved again. Be sure to copy and store it in a secure location. If the key is lost, you must generate a new key.
{% endhint %}

### Field Validations

The same validations apply while creating or editing a key. If an entered value does not meet a rule, a warning message is shown and the key is not saved:

| Field          | Rule                                   | Warning message shown on violation                     |
|----------------|----------------------------------------|--------------------------------------------------------|
| **Name**       | Must be unique.                        | API key name must be unique.                           |
| **Expires on** | Must be a future date and time.        | Expiry date must be a future datetime.                 |
| **Expires on** | Cannot be more than 1 year from today. | API key expiry cannot be set beyond 1 year from today. |

---

## Using an API Key

Once generated, an API Key can authenticate requests to the **Admin API** and **MCP** endpoints. Pass the key in one of the following request headers:

```
x-api-key: <api-key>
```

or

```
Authorization: ApiKey <api-key>
```

On a successful request, the **Last accessed** timestamp of the key is updated automatically. If the key is invalid, expired, or revoked, a **401 Unauthorized** response is returned:

```json
{
  "errorMessage": "Authentication failed. Valid credentials are required to access this resource.",
  "stackTrace": null
}
```

---

## Editing an API Key

An API Key can be edited only while it is in the **Active** state.

1. Navigate to **Administration → API key**.
2. Click on an active key to open its details.
3. Click the edit button on the top right corner.
4. Update the **Name** and/or **Expires on** fields. The same field validations apply as when creating a key.
5. Click **Save**.

<p align="center">
  <img src="../../assets/APIKey_Edit_Form.png" width="1000"/>
</p>

> **Note:** Editing is not available for expired or revoked keys — the edit option will be disabled for those keys.

---

## Revoking an API Key

You can revoke a key from the **API key** list view by clicking the **✕** button in the **Action** column against that key.

<p align="center">
  <img src="../../assets/APIKey_List_Revoke_Action.png" width="1000"/>
</p>

1. Navigate to **Administration → API key**.
2. Click the **✕** button against the key you want to revoke in the **Action** column.
3. A confirmation prompt appears: *"API key with name &lt;api-key-name&gt; will be permanently revoked. This action is irreversible."*
4. Click **Yes, revoke it!** to confirm.

<p align="center">
  <img src="../../assets/APIKey_Revoke_Confirmation.png" width="600"/>
</p>

After revocation:

- The key remains visible in the list with a **Revoked** status — it is not deleted.
- Any subsequent request using that key returns a **401 Unauthorized** response.
- A revoked key cannot be reactivated. If access is required again, a new key must be generated.

---

## API Key Statuses

Every API Key has one of the following statuses:

| Status      | Description                                                                     |
|-------------|---------------------------------------------------------------------------------|
| **Active**  | The key is valid and can be used to authenticate requests.                      |
| **Expired** | The configured expiry datetime has been reached. The key can no longer be used. |
| **Revoked** | The key has been revoked. It cannot be used, restored, or reused.               |

A newly created key starts in the **Active** state. **Expired** and **Revoked** are terminal states — a key in either state cannot be restored or reused.

---

## Audits

All actions performed on API Keys are logged and can be viewed from the **API key audits** screen. Each audit entry captures the **Name**, **Author**, **Change Time**, **Revision Type**, and changed field values.

<p align="center">
  <img src="../../assets/APIKey_Audits.png" width="1000"/>
</p>

The following actions are recorded:

- **Create** — logged when a new key is created, along with its name and expiry date.
- **Update** — logged when the name or expiry date of a key is changed.
- **Revoke** — logged when a key is revoked, along with the change in its status.

---

## User Access Control

- Any authenticated user, irrespective of role, can generate and manage their own API Keys.
- A user can only view and manage their own keys — they cannot view, modify, or revoke keys created by another user.
- By default, only the **Super Admin** can manage API Keys across all users. Users with the **User Management – Write** permission in a custom role can also view and manage API Keys of other users. Refer to [User Access Control](user-access-control.md) for more details.


{% hint style="info" %}
**My keys vs. all keys:** A regular user always sees only their own keys. Users who are allowed to manage other users' keys (the **Super Admin**, or a custom role with **User Management – Write** permission) get a toggle on the **API key** list view to switch between **My API keys** (only the keys they created) and **All API keys** (keys across all users). This toggle is visible only to these privileged users — a regular user does not see it.
{% endhint %}

<p align="center">
  <img src="../../assets/APIKey_MyKeys_AllKeys_Toggle.png" width="1000"/>
</p>

---

## Known Behaviors

| Behavior                          | Detail                                                                                             |
|-----------------------------------|----------------------------------------------------------------------------------------------------|
| **Key shown once**                | After generation, the key value cannot be retrieved. A new key must be generated if it is lost.    |
| **Revocation is immediate**       | Once revoked, a key cannot be restored. A new key must be generated if needed.                     |
| **No key rotation**               | In-place key rotation is not supported. Generate a new key and revoke the old one.                 |
| **No per-key permission scoping** | API Keys inherit the generating user's full permissions — granular scope control is not supported. |
| **Deleted user keys**             | All API Keys of a deleted user are revoked automatically and cannot be reactivated.                |