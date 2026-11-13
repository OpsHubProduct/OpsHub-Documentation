---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# Overview

Retrieves the list of UML and SysML element types supported by the end system for a given project. Examples of these types include UML Class, UML Property, SysML Requirement, etc.

The supported types are classified into the following three categories based on how they are used to organize model elements in the end system:

- **Container types**: Types such as Project or Branch represent containers within which model elements are created and managed. These types serve as top-level containers for model elements and must be classified under `containerTypes`.

- **Packageable types**: Model element types such as Package, Profile, and Namespace are used to organize and group other model elements. They can contain child elements of any type, including both packageable and non-packageable types. Such model element types must be classified under `packageableTypes`.

- **Non-packageable types**: Model element types such as Class, Property, UseCase, Activity, Artifact, and Operation can contain only specific types of child elements, as defined by the end system. For example, a Class can contain Properties and Operations but may not support all types of model elements as children. Such model element types must be classified under `nonPackageableTypes`.

OpsHub uses this information to identify the types of elements supported by the end system and build the corresponding element hierarchy when synchronizing model elements.

# API URI

OpsHub invokes this API using the following URI:

```http
GET /mbse/api/1.0/types?projectId=<projectId>
```

# URI Parameters

| Name | In | Required | Type | Description |
|------|----|----------|------|-------------|
| projectId | Query | Yes | String | ID of the project for which the supported element types must be retrieved. This is the same ID returned in the response of the [`/projects`](projects-list.md) API. |

# Response Payload

```json
{
  "containerTypes": [
    "Project"
  ],
  "packageableTypes": [
    "uml:Package",
    "uml:Profile"
  ],
  "nonPackageableTypes": [
    "uml:Class",
    "uml:Property",
    "sysml:Requirement"
  ]
}
```

# Response Parameters

| Name | Type | Required | Description                                                                                         |
|------|------|----------|-----------------------------------------------------------------------------------------------------|
| containerTypes | List<String> | No | List of types that represent containers for model elements in the end system.                       |
| packageableTypes | List<String> | Yes | List of types that can be used to group child elements without restricting their types.             |
| nonPackageableTypes | List<String> | Yes | List of types that can contain only specific types of child elements, as defined by the end system. |

Each value in these lists represents the unique identifier of an element type supported by the end system.