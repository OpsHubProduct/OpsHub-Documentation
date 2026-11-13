---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# Overview

Fetches a list of stereotype groupings for the specified project. Each grouping represents a unique combination of stereotypes (such as `SysML::Requirements::Requirement`, `SysML::Blocks::Block`, etc.)  applied together to elements of a particular UML or SysML type (such as `uml:Class`, `uml:Artifact`, `uml:Property`, etc.).

Each grouping corresponds to an element type in OIM. Elements matching this type and stereotype combination are identified as the corresponding entity type in OIM.

This API enables OpsHub to automatically derive the element types supported by the end system for the specified project, based on the UML or SysML types and stereotype combinations applied to its elements.

# API URI

OpsHub invokes this API using the following URI:

```http
GET /mbse/api/1.0/stereotype-grouping?projectId=<projectId>
```

# URI Parameters

| Name | In | Required | Type | Description |
|------|----|----------|------|-------------|
| projectId | Query | Yes | String | ID of the project for which stereotype groupings are to be discovered. This is the same project ID returned in the response of the [`/projects`](projects-list.md) API. |

# Response Payload

```json
[
  {
    "id": "f8991547-839e-3ec3-8c97-6855138e97a0",
    "name": "Activity",
    "type": "uml:Activity",
    "identifyingStereotypes": ["Profile::CustomActivity::Custom"]
  },
  {
    "id": "9876ae67-a44a-36c3-bec3-a59bb7e77243",
    "name": "Requirement",
    "type": "uml:Class",
    "identifyingStereotypes": ["SysML::Requirements::Requirement"]
  }
]
```

# Response Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| id | String | Yes | Unique identifier of the stereotype grouping. |
| name | String | Yes | Display name of the stereotype grouping. |
| type | String | Yes | UML or SysML type associated with the grouping (e.g., `uml:Activity`). The value must match a type returned by the [`/types`](types-list.md) API. |
| identifyingStereotypes | List<String> | Yes | List of stereotypes applied together to elements of the specified UML or SysML type.  |