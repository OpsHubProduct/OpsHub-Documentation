---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# API Name

API Name: Element – Create

---

# Overview

This API creates a new [element](../getting-started/mbse-sdk-connector-apis.md#glossary) in the specified project (and optional branch).

MBSE Core uses this API to:

- Create new model elements
- Establish parent-child hierarchy
- Set initial properties and tags
- Establish mandatory relations during creation

Connector responsibility:

- Prepare the create request according to end system requirements.
- Create the element in the specified project and branch.
- Apply provided properties.
- Create or update supplied tags using connector-supported tag APIs.
- Create required relations as part of element creation.
- Convert the final created element into `MbseElement` format and return it.

---

## API URI

```bash
POST: /mbse/api/1.0/elements
    ?projectId={projectId}
    &elementTypeId={elementTypeId}
    &branchId={branchId}
```

---

## URI Parameters

| Name          | Mandatory | Type   | Description |
|---------------|-----------|--------|-------------|
| projectId     | True      | String | ID of the project where the element will be created. |
| elementTypeId | True      | String | ID of the element type to be created. |
| branchId      | False     | String | ID of the branch. If omitted, default branch behavior applies. |

---

## Request Body

```json
{
  "name": "System Block",
  "parentElementId": "package_1",
  "properties": {
    "status": "Draft"
  },
  "tags": {
    "criticality": "High"
  },
  "requiredRelations": [
    {
      "relationType": "dependency",
      "targetElementId": "requirement_55",
      "targetElementTypeId": "Requirement",
      "projectId": "123"
    }
  ]
}
```

---

## Request Body Parameters

| Name              | Mandatory | Type                   | Description |
|-------------------|-----------|------------------------|-------------|
| name              | True      | String                 | Name of the element. |
| parentElementId   | False     | String                 | ID of the parent element. |
| properties        | False     | Map<String,Object>     | Properties to set during creation. |
| tags              | False     | Map<String,Object>     | Tagged values to set during creation. |
| requiredRelations | False     | List<Relation>         | List of mandatory relations to establish during creation. |

---

## Behavior Rules

1. Element must be created within the scope of:
    - `projectId`
    - `elementTypeId`
    - Optional `branchId`
2. Only properties provided in the request must be set.
3. Connector must not modify or inject additional fields unless required by the end system.
4. Tags:
    - If tag exists → update it.
    - If tag does not exist → create it.
    - MBSE Core may provide utilities to support tag lifecycle management.
5. Required relations must be created during element creation if supported by the end system.
6. If creation fails:
    - Return appropriate HTTP error code.
7. The response must return the fully created element in `MbseElement` format.

---

## Response Payload

### Sample Response

```json
{
  "elementId": "block_200",
  "name": "System Block",
  "elementTypeId": "Block",
  "qualifiedName": "Model::System::Block",
  "projectId": "123",
  "createdBy": "john.doe",
  "updatedBy": "john.doe",
  "createdDate": "2026-02-14T12:00:00.000Z",
  "updatedDate": "2026-02-14T12:00:00.000Z",
  "parentElementId": "package_1",
  "properties": {
    "status": "Draft"
  },
  "tags": {
    "criticality": "High"
  },
  "relations": [
    {
      "relationType": "dependency",
      "targetElementId": "requirement_55",
      "targetElementTypeId": "Requirement",
      "projectId": "123"
    }
  ]
}
```

---

## Response Parameters

The response must conform to the `MbseElement` structure defined in the Element – Get API.

| Name            | Required | Type              | Description |
|----------------|----------|-------------------|-------------|
| elementId      | True     | String            | Unique identifier of the created element. |
| name           | True     | String            | Name of the element. |
| elementTypeId  | True     | String            | ID of the element type. |
| projectId      | True     | String            | Project ID. |
| createdBy      | False    | String            | User who created the element. |
| createdDate    | False    | String (ISO-8601) | Creation timestamp. |
| properties     | False    | Map<String,Object>| Properties set during creation. |
| tags           | False    | Map<String,Object>| Tags set during creation. |
| relations      | False    | List<Relation>    | Relations created during creation. |

## Relation Object

| Name               | Required | Type   | Description |
|--------------------|----------|--------|-------------|
| relationType       | True     | String | Type of relation (association, dependency, etc.). |
| targetElementId    | True     | String | Target element ID. |
| targetElementTypeId| True     | String | Target element type ID. |
| projectId          | True     | String | Project ID of the target element. |
| author             | False    | String | Creator of relation. |
| createdDate        | False    | String | Relation creation timestamp. |

---

## Error Handling

| HTTP Status | Description |
|------------|-------------|
| 400        | Invalid input parameters. |
| 404        | Project or parent element not found. |
| 409        | Conflict during creation (duplicate element, constraint violation). |
| 500        | Internal server error during element creation. |

---

## Implementation Guidelines

- Validate `elementTypeId` before creation.
- Validate parent element existence if `parentElementId` is provided.
- Avoid partial creation:
    - If property or tag creation fails, roll back if supported by the end system.
- Ensure timestamp format follows ISO-8601.
- Return consistent `MbseElement` structure.

---

## Design Rationale

This API enables controlled element creation with:

- Hierarchical support
- Property initialization
- Tag lifecycle management
- Mandatory relation establishment

By separating creation from update and enforcing structured expansion rules, the MBSE integration layer remains deterministic and system-agnostic.
