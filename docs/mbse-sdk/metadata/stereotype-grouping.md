---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# Overview

# Overview

Discovers how elements in a given project are grouped based on the combinations of stereotypes (metadata definition) and their corresponding UML or SysML types in the end system.

The response contains a list of stereotype groupings, where each grouping includes the list of stereotypes applied together to the elements and the corresponding UML or SysML type.

This API enables OpsHub to derive the element types supported by the end system based on the combinations of UML or SysML types and stereotypes applied to its elements.

# API URI

OpsHub invokes this API using the following URI:

```http
GET /mbse/api/1.0/stereotype-grouping?projectId=<projectId>
```

# URI Parameters

| Name | In | Required | Type | Description |
|------|----|----------|------|-------------|
| projectId | Query | Yes | String | ID of the project for which stereotype grouping needs to be discovered. This will be the same ID returned in the response of the [`/projects`](projects-list.md) API response |

# Response Payload

```json
[
  {
    "id": "f8991547-839e-3ec3-8c97-6855138e97a0",
    "name": "Activity",
    "type": "uml:Activity",
    "identifyingStereotypes": []
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

| Name | Type | Required | Description                                                                                                                                                                                                            |
|------|------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id | String | Yes | Unique identifier of the grouping.                                                                                                                                                                                     |
| name | String | Yes | Display name of the grouping.                                                                                                                                                                                          |
| type | String | Yes | UML or SysML type associated with the grouping (e.g., `uml:Activity`). The value will be the same type returned in the [/types](types-list.md) API.                                                                    |
| identifyingStereotypes | List<String> | Yes | List of stereotypes applied together to elements belonging to this grouping. An empty list indicates that the grouping applies to elements matching the specified type, regardless of the stereotypes applied to them. |