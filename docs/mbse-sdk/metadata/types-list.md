---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# Overview

Retrieves the list of UML and SysML types supported by the end system for a given project, such as UML Class, UML Property, or SysML Requirement.

The supported types are categorized into three groups:

- **Container types**: Types that represent containers for model data, such as Project, Branch, etc.
- **Packageable types**: Types that can organize and group model elements. They can contain child elements of any type, including both packageable and non-packageable types.
- **Non-packageable types**: Types that can contain only specific or restricted types of child elements.

# API URI

OpsHub invokes this API using the following URI:

```http
GET /mbse/api/1.0/types?projectId=<projectId>
```

# URI Parameters

| Name | In | Required | Type | Description |
|------|----|----------|------|-------------|
| projectId | Query | Yes | String | ID of the project for which the supported types must be retrieved. This will be the same ID returned in the response of the [`/projects`](projects-list.md) API. |

# Response Payload

```json
{
  "containerTypes": [
    "Project"
  ],
  "packageableTypes": [
    "uml:Package",
    "uml:Class"
  ],
  "nonPackageableTypes": [
    "uml:Property",
    "sysml:Requirement"
  ]
}
```

# Response Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| containerTypes | List<String> | Yes | List of container types supported by the end system. |
| packageableTypes | List<String> | Yes | List of packageable types supported by the end system. |
| nonPackageableTypes | List<String> | Yes | List of non-packageable types supported by the end system. |

Each string in the above lists represents the unique identifier of a type.