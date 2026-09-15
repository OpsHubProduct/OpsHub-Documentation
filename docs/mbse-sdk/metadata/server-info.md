---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# API Name

API Name: Server Info – Get

---

# Overview

This API returns server-level configuration information required by MBSE Core to interact correctly with the end system.

MBSE Core uses this API to:

- Understand system time zone behavior
- Determine maximum supported page size
- Identify integration user configuration
- Identify if Project should also be treated as an element

Connector responsibility:

- Provide accurate server configuration details.
- Return pagination limits supported by the system.
- Return integration user configuration metadata.
- Return whether Project should be treated as an element.
---

## API URI

```bash
GET: /mbse/api/1.0/server-info
```

---

# Response Parameters

## Root Level Parameters

| Name                | Required | Type    | Description                                                                                                                                                                                                                                    |
|---------------------|----------|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| timeZone            | No       | String  | Time zone of the end system. Examples: `"America/Los_Angeles"`, `"GMT-8:00"`, `"UTC"`. Return blank if timezone is embedded in date values returned by the system.                                                                             |
| maxResults          | Yes      | Integer | Maximum number of records that can be returned in a single paginated API response. If the end system does not support pagination natively, the connector must implement in-memory pagination and provide the maximum supported page size here. |
| supportsProjectAsElement | No       | Boolean | Send `true` if Project should also be treated as an element. Send `false` (or nothing) if not. Default is `false`. See [Element](../getting-started/mbse-sdk-connector-apis.md#glossary).  |
| integrationUserInfo | Yes      | Object  | Information about the integration user configuration.                                                                                                                                                                                          |

---

## integrationUserInfo Object

| Name              | Required | Type   | Description |
|-------------------|----------|--------|-------------|
| fieldInternalName | Yes      | String | Internal name of the field used in the system configuration screen to capture the integration username or email. This must match the corresponding field defined in the Connector Metadata API. |
| userDataType      | Yes      | Enum   | Data type of the integration user field. Valid values:<br>- `EMAIL_AS_USER`<br>- `USERNAME_AS_USER` |

---

# Response Payload

```json
{
  "timeZone": "UTC",
  "maxResults": 50,
  "supportsProjectAsElement": true,
  "integrationUserInfo": {
    "userDataType": "USERNAME_AS_USER",
    "fieldInternalName": "userName"
  }
}
```

---

# Behavior Rules

1. `maxResults` must always be provided.
2. If the end system does not support pagination:
    - The connector must implement pagination internally.
    - `maxResults` must reflect the enforced page size.
3. `timeZone` must be provided if timestamps do not contain timezone information.
4. `fieldInternalName` must match a field defined in the Connector Metadata API.
5. Send `supportsProjectAsElement` as `true` only when the connector's Element APIs (Get, Query, Create, Update) also work for Project. If you send `false`, or send nothing, Project will not be treated as an element.

---

# Design Rationale

This API ensures MBSE Core can:

- Interpret timestamps correctly.
- Enforce safe pagination limits.
- Identify integration user context consistently.
- Identify whether Project should be treated as an element.

Accurate server configuration is critical for reliable synchronization and data integrity.
