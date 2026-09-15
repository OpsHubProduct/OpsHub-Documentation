---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# API Name

API Name: Element – Get

---

# Overview

This API retrieves a single [element](../getting-started/mbse-sdk-connector-apis.md#glossary) from the end system.

MBSE Core uses this API to:

- Fetch element details
- Perform on-demand synchronization
- Retrieve full element state
- Support relation and file expansion

Connector responsibility:

- Retrieve the element using the end system API with the given `elementId`.
- Respect project and branch scoping.
- Based on `expand` options:
    - Load properties
    - Load tags
    - Load relations
    - Load files
- For tags, connector may need to:
    - Extract tag GUIDs from element metadata
    - Fetch tag details separately
- Fetch relations and files if requested.
- Convert all retrieved data into `MbseElement` format.

---

## API URI

```bash
GET: /mbse/api/1.0/elements/{elementId}
    ?projectId={projectId}
    &elementTypeId={elementTypeId}
    &branchId={branchId}
    &expand=PROPERTIES,TAGS,FILES,RELATIONS
    &properties={properties}
    &tags={tags}
```

---

## Path Parameters

| Name       | Mandatory | Type   | Description |
|------------|-----------|--------|-------------|
| elementId  | True      | String | ID of the element to retrieve. |

---

## URI Parameters

| Name           | Mandatory | Type          | Description |
|----------------|-----------|--------------|-------------|
| projectId      | True      | String       | ID of the project. |
| elementTypeId  | True      | String       | ID of the element type. |
| branchId       | False     | String       | ID of the branch. If omitted, default branch behavior applies. |
| expand         | False     | List<String> | Controls which additional information is included. Possible values: `PROPERTIES`, `TAGS`, `FILES`, `RELATIONS`. |
| properties     | False     | List<String> | List of property IDs to include. Applicable only if `PROPERTIES` is included in `expand`. |
| tags           | False     | List<String> | List of tag IDs to include. Applicable only if `TAGS` is included in `expand`. |

---

## Expand Parameter Behavior

The `expand` parameter controls what additional data is returned:

### PROPERTIES
- Include element properties.
- If `properties` is provided, return only those properties.
- If omitted, return all properties.

### TAGS
- Include tagged values.
- If `tags` is provided, return only those tags.
- If omitted, return all tags.

### FILES
- Include files attached to the element.

### RELATIONS
- Include element relations.

If `expand` is omitted, only base element metadata must be returned.

---

## Behavior Rules

1. The element must be retrieved within the scope of:
    - `projectId`
    - `elementTypeId`
    - Optional `branchId`
2. If element does not exist:
    - Return HTTP `404 Not Found`.
3. If `expand` is not provided:
    - Do not return properties, tags, files, or relations.
4. Respect filtering parameters (`properties`, `tags`).
5. Do not return unrelated data.
6. Response must strictly follow `MbseElement` structure.

---

## Response Payload

### Sample Response

```json
{
  "elementId": "block_101",
  "name": "System Block",
  "elementTypeId": "Block",
  "qualifiedName": "Model::System::Block",
  "projectId": "123",
  "createdBy": "john.doe",
  "updatedBy": "jane.smith",
  "createdDate": "2026-02-14T08:15:30.000Z",
  "updatedDate": "2026-02-14T10:10:15.000Z",
  "parentElementId": "package_1",
  "properties": {
    "status": "Approved",
    "version": "1.2"
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
  ],
  "files": [
    {
      "fileId": "file_001",
      "fileName": "block-diagram.png",
      "filePath": "/attachments/block-diagram.png",
      "downloadUrl": "https://example.com/download/file_001",
      "label": "Diagram",
      "contentType": "image/png",
      "contentLength": 204800,
      "author": "john.doe",
      "fileType": "IMAGE",
      "lastModifiedDate": "2026-02-14T09:00:00.000Z"
    }
  ]
}
```

---

## Response Parameters

### Element Object

| Name            | Required | Type              | Description |
|----------------|----------|-------------------|-------------|
| elementId      | True     | String            | Unique element identifier. |
| name           | False    | String            | Name of the element. |
| elementTypeId  | True     | String            | ID of the element type. |
| qualifiedName  | False    | String            | Fully qualified name. |
| projectId      | True     | String            | Project ID. |
| createdBy      | False    | String            | User who created the element. |
| updatedBy      | False    | String            | User who last updated the element. |
| createdDate    | False    | String (ISO-8601) | Creation timestamp. |
| updatedDate    | False    | String (ISO-8601) | Last update timestamp. |
| parentElementId| False    | String            | Parent element ID. |
| properties     | False    | Map<String,Object>| Element properties (if expanded). |
| tags           | False    | Map<String,Object>| Tagged values (if expanded). |
| relations      | False    | List<Relation>    | Element relations (if expanded). |
| files          | False    | List<File>        | Attached files (if expanded). |

---

## Relation Object

| Name               | Required | Type   | Description |
|--------------------|----------|--------|-------------|
| relationType       | True     | String | Type of relation (association, dependency, etc.). |
| targetElementId    | True     | String | Target element ID. |
| targetElementTypeId| True     | String | Target element type ID. |
| projectId          | True     | String | Project ID. |
| author             | False    | String | Creator of relation. |
| createdDate        | False    | String | Relation creation timestamp (ISO-8601). |

---

## File Object

| Name             | Required | Type   | Description |
|------------------|----------|--------|-------------|
| fileId           | True     | String | Unique file identifier. |
| fileName         | True     | String | File name. |
| filePath         | False    | String | File path. |
| downloadUrl      | False    | String | File download URL. |
| label            | False    | String | File label. |
| contentType      | False    | String | MIME type. |
| contentLength    | False    | Long   | File size in bytes. |
| author           | False    | String | File uploader. |
| fileType         | False    | String | File category/type. |
| lastModifiedDate | False    | String | Last modified timestamp (ISO-8601). |

---

## Example Use Case

### Get Element with Properties and Tags

```bash
GET /mbse/api/1.0/elements/block_101?
projectId=123
&elementTypeId=Block
&expand=PROPERTIES,TAGS
```

---

## Implementation Guidelines

- Always scope element retrieval to project and branch.
- Validate element type consistency.
- Fetch tags separately if end system stores them independently.
- Do not over-fetch data if `expand` is not specified.
- Convert all data strictly into `MbseElement` format.
- Ensure consistent timestamp formatting (ISO-8601).

---

## Design Rationale

This API provides controlled and expandable element retrieval.

By:

- Supporting selective expansion
- Supporting property/tag filtering
- Maintaining strict scoping

The API ensures performance efficiency and predictable synchronization behavior across heterogeneous MBSE systems.
