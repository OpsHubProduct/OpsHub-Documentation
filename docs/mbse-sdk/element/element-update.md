---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# API Name

API Name: Element – Update

---

# Overview

This API updates an existing [element](../getting-started/mbse-sdk-connector-apis.md#glossary) in the specified project (and optional branch).

MBSE Core uses this API to:

- Modify element metadata
- Update properties
- Update tagged values
- Update parent hierarchy
- Establish required relations during update

Connector responsibility:

- Retrieve the element within the provided context.
- Prepare the update request according to end system requirements.
- Update only the fields provided in the request body.
- Create or update supplied tags using connector-supported tag APIs.
- Create required relations if provided.
- Convert the updated element into `MbseElement` format and return it.

---

## API URI

```bash
PUT: /mbse/api/1.0/elements/{elementId}
    ?projectId={projectId}
    &elementTypeId={elementTypeId}
    &branchId={branchId}
```

---

## Path Parameters

| Name       | Mandatory | Type   | Description |
|------------|-----------|--------|-------------|
| elementId  | True      | String | ID of the element to update. |

---

## URI Parameters

| Name          | Mandatory | Type   | Description |
|---------------|-----------|--------|-------------|
| projectId     | True      | String | ID of the project in which the element exists. |
| elementTypeId | True      | String | ID of the element type. |
| branchId      | False     | String | ID of the branch. If omitted, default branch behavior applies. |

---

## Request Body

```json
{
  "name": "Updated System Block",
  "parentElementId": "package_2",
  "properties": {
    "status": "Approved"
  },
  "tags": {
    "criticality": "Medium"
  },
  "requiredRelations": [
    {
      "relationType": "realization",
      "targetElementId": "requirement_60",
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
| name              | False     | String                 | Updated name of the element. |
| parentElementId   | False     | String                 | Updated parent element ID. |
| properties        | False     | Map<String,Object>     | Properties to update. |
| tags              | False     | Map<String,Object>     | Tagged values to update. |
| requiredRelations | False     | List<Relation>         | Relations to establish during update. |

---

## Behavior Rules

1. The element must exist within the context of:
    - `projectId`
    - `elementTypeId`
    - Optional `branchId`
2. Only fields provided in the request body must be updated.
3. Fields not present in the request body must not be modified.
4. Parent update:
    - If `parentElementId` is provided, update hierarchy accordingly.
5. Properties:
    - Update only provided properties.
    - Do not remove unspecified properties unless explicitly required by system logic.
6. Tags:
    - If tag exists → update it.
    - If tag does not exist → create it.
    - MBSE Core may provide utilities for tag lifecycle handling.
7. Required relations:
    - Must be created if provided.
    - Must not remove existing relations unless explicitly supported.
8. If element does not exist:
    - Return HTTP `404 Not Found`.

---

## Response Payload

The response must return the fully updated element in `MbseElement` format.

### Sample Response

```json
{
  "elementId": "block_200",
  "name": "Updated System Block",
  "elementTypeId": "Block",
  "qualifiedName": "Model::System::UpdatedBlock",
  "projectId": "123",
  "createdBy": "john.doe",
  "updatedBy": "jane.smith",
  "createdDate": "2026-02-14T12:00:00.000Z",
  "updatedDate": "2026-02-14T13:00:00.000Z",
  "parentElementId": "package_2",
  "properties": {
    "status": "Approved"
  },
  "tags": {
    "criticality": "Medium"
  }
}
```

---

## Response Parameters

The response must conform to the `MbseElement` structure defined in the Element – Get API.

| Name            | Required | Type              | Description |
|----------------|----------|-------------------|-------------|
| elementId      | True     | String            | Unique element identifier. |
| elementTypeId  | True     | String            | ID of the element type. |
| projectId      | True     | String            | Project ID. |
| updatedBy      | False    | String            | User who performed the update. |
| updatedDate    | False    | String (ISO-8601) | Last modification timestamp. |
| properties     | False    | Map<String,Object>| Updated properties. |
| tags           | False    | Map<String,Object>| Updated tagged values. |

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
| 400        | Invalid request parameters. |
| 404        | Element not found in the specified project. |
| 409        | Update conflict or constraint violation. |
| 500        | Internal server error during element update. |

---

## Implementation Guidelines

- Validate element existence before update.
- Avoid full overwrite unless required by end system.
- Do not silently ignore invalid fields.
- Ensure updates are atomic where supported.
- Maintain ISO-8601 timestamp format.
- Return the updated element state.

---

## Design Rationale

This API enforces controlled partial updates.

By:

- Updating only provided fields
- Supporting tag lifecycle management
- Maintaining strict scoping
- Avoiding unintended data removal

The MBSE integration layer remains predictable, safe, and system-agnostic.
