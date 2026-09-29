---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# API Name

API Name: Revision – Get Elements at Revision

---

# Overview

This API returns the state of given elements at a specific revision.

It provides a snapshot of elements as they existed at `revisionId`.

MBSE Core uses this API when:

- Field-level diff is not provided by the Revision – Diff API.
- Full element reconstruction is required.
- Snapshot-based synchronization is implemented.

Connector responsibility:

- This API is **not mandatory** if detailed property/tag diff is already provided in the Revision – Diff API.
- If detailed diff is not provided, connector must implement this API.
- Connector must return element state exactly as it existed at the specified revision.

---

## API URI

```bash
POST: /mbse/api/1.0/revisions/{revisionId}/elements
    ?projectId={projectId}
    &elementTypeIds={elementTypeIds}
    &branchId={branchId}
    &expand=PROPERTIES,TAGS,FILES,RELATIONS
    &tags={tags}
    &properties={properties}
```

---

## Path Parameters

| Name        | Mandatory | Type   | Description |
|------------|-----------|--------|-------------|
| revisionId | True      | String | ID of the revision at which element state must be retrieved. |

---

## URI Parameters

| Name           | Mandatory | Type          | Description                                                                                                                            |
|----------------|-----------|--------------|----------------------------------------------------------------------------------------------------------------------------------------|
| projectId      | True      | String       | ID of the project.                                                                                                                     |
| elementTypeIds | True      | List<String> | List of element Type Ids defined in `element-types` JSON configuration. Only changes related to these element types must be returned.  |
| branchId       | False     | String       | ID of the branch. If omitted, default branch behavior of the end system should apply.                                                  |
| expand         | False     | List<String> | Controls which additional information should be included in the response. Possible values: `PROPERTIES`, `TAGS`, `FILES`, `RELATIONS`. |
| tags           | False     | List<String> | List of tag IDs to be included in the response. Applicable only if `TAGS` is included in `expand`.                                     |
| properties     | False     | List<String> | List of property IDs to be included in the response. Applicable only if `PROPERTIES` is included in `expand`.                          |

---

## Request Body
```json
[
  {
    "elementId": "block_101",
    "changeType": "ADD"
  },
  {
    "elementId": "requirement_55",
    "changeType": "UPDATE"
  }
]
```
---

## Expand Parameter Behavior

The `expand` parameter determines which additional fields are included:

- `PROPERTIES`
    - Include element properties.
    - If `properties` parameter is provided, return only those properties.
    - If not provided, return all properties.

- `TAGS`
    - Include tagged values.
    - If `tags` parameter is provided, return only those tags.
    - If not provided, return all tags.

- `FILES`
    - Include files attached to the element.

- `RELATIONS`
    - Include relations of the element.

If `expand` is omitted, only base element metadata must be returned.

---

## Behavior Rules

1. Element state must reflect the exact state at `revisionId`.
2. Only elements specified in `elementIds` must be returned.
3. If an element does not exist at the specified revision, it must not be returned.
4. Filtering by `properties` and `tags` must be respected when provided.
5. If `expand` is not specified, properties, tags, files, and relations must not be returned.
6. Response must not include data beyond what is requested.

---

## Response Payload

The API returns a list of element objects.

### Sample Response

```json
[
  {
    "sourceElementId" : "block_101",
    "mbseElement" : {
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
  }
]
```

---

## Response Object Structure
| Name              | Required | Type              | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|-------------------|----------|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| sourceElementId | True     | String            | Identifier used to resolve the corresponding mbseElement. In the usual case, this is the ID of the MBSE element itself. For connectors where the MBSE element is resolved through an associated tag, comment, property, or other object, this contains the ID of that object, while mbseElement.elementId contains the ID of the actual MBSE element.                                                                                                                                                             |
| mbseElement       | True     | Object            | The MBSE element associated with the resolved identifier. This object represents the actual MBSE model element discovered by the connector, regardless of whether the element was resolved directly using its own ID or indirectly through an associated object such as a tag, comment, property, or other metadata. The object contains the element's details such as element type, properties, tags, relations, attached files etc, depending on the requested expansion and the capabilities of the connector. |

### Connector Behaviors and `sourceElementId` Examples

The value of `sourceElementId` depends on how the connector discovers and tracks changes. The connector may receive an ID for the actual MBSE model element or an ID for a related object that helps identify the model element.

#### Case 1. Change directly on the model element

- **Behavior**: The connector directly tracks changes against the MBSE model elements. The `elementId` passed in the request body identifies the MBSE element itself.

- **Example**: A Block named **"System Block"** is updated.
    - The connector detects a change directly on the Block.
    - The connector receives the Block ID.
    - The connector returns the same Block as the affected MBSE model element.

- **Value of `sourceElementId`**: Matches the element's own `elementId` (`sourceElementId == mbseElement.elementId`).

- **Example of Request-Response**:
    - **Request Body Item**:
      ```json
      {
        "elementId": "block_101",
        "changeType": "UPDATE"
      }
      ```

    - **Response Object**:
      ```json
      {
        "sourceElementId": "block_101",
        "mbseElement": {
          "elementId": "block_101",
          "name": "System Block",
          "elementTypeId": "Block",
          "projectId": "123"
        }
      }
      ```

    - **Result**:
        - `sourceElementId` = `"block_101"`
        - `mbseElement.elementId` = `"block_101"`
        - Both values are the same because the change occurred directly on the MBSE model element.

---

#### Case 2. Change on something related to the model element

- **Behavior**: The connector tracks changes related to an MBSE model element, such as comments, properties, stereotypes, tagged values, or linked diagrams. When a change occurs, the Revision Diff API provides the ID of the affected related item.

- **Case**: A comment attached to **"System Block"** is updated.
    - The connector detects the change on the comment.
    - The connector receives the Comment ID.
    - The connector identifies that the comment belongs to `"block_101"`.
    - The connector returns `"block_101"` as the actual MBSE model element.

- **Value of `sourceElementId`**: Contains the ID of the associated object received in the request body, while `mbseElement.elementId` contains the ID of the actual resolved MBSE model element (`sourceElementId != mbseElement.elementId`).

- **Example**:
    - **Request Body Item**:
      ```json
      {
        "elementId": "comment_901",
        "changeType": "UPDATE"
      }
      ```
      *(where `comment_901` is a comment or annotation associated with `block_101`)*

    - **Response Object**:
      ```json
      {
        "sourceElementId": "comment_901",
        "mbseElement": {
          "elementId": "block_101",
          "name": "System Block",
          "elementTypeId": "Block",
          "projectId": "123"
        }
      }
      ```

    - **Result**:
        - `sourceElementId` = `"comment_901"`
        - `mbseElement.elementId` = `"block_101"`
        - The values are different because the connector used the Comment to identify the actual MBSE model element.

### In Simple Terms

Think of `sourceElementId` as:

> **The ID of the item that led the connector to identify the MBSE model element.**

And `mbseElement.elementId` as:

> **The ID of the actual MBSE model element identified by the connector.**

Therefore:

- **Direct change**: The change occurs directly on the model element, so both IDs are the same.
    - `sourceElementId = elementId`

- **Indirect change**: The change occurs on a related object, such as a comment, property, stereotype, tagged value, or diagram element. The related object's ID is used to identify the actual model element, so the IDs are different.
    - `sourceElementId != elementId`
---

## Element Object Structure

| Name            | Required | Type              | Description |
|----------------|----------|-------------------|-------------|
| elementId      | True     | String            | Unique identifier of the element. |
| name           | False    | String            | Name of the element. |
| elementTypeId  | True     | String            | ID of the element type. |
| qualifiedName  | False    | String            | Fully qualified name of the element. |
| projectId      | True     | String            | Project ID. |
| createdBy      | False    | String            | User who created the element. |
| updatedBy      | False    | String            | User who last updated the element. |
| createdDate    | False    | String (ISO-8601) | Creation timestamp. |
| updatedDate    | False    | String (ISO-8601) | Last modification timestamp. |
| parentElementId| False    | String            | Parent element ID. |
| properties     | False    | Map<String,Object>| Element properties (if expanded). |
| tags           | False    | Map<String,Object>| Tagged values (if expanded). |
| relations      | False    | List<Relation>    | Element relations (if expanded). |
| files          | False    | List<File>        | Files attached to element (if expanded). |

---

## Relation Object Structure

| Name               | Required | Type   | Description |
|--------------------|----------|--------|-------------|
| relationType       | True     | String | Type of relation (association, dependency, realization, etc.). |
| targetElementId    | True     | String | Target element ID. |
| targetElementTypeId| True     | String | Target element type ID. |
| projectId          | True     | String | Project ID. |
| author             | False    | String | Creator of the relation. |
| createdDate        | False    | String | Relation creation timestamp (ISO-8601). |

---

## File Object Structure

| Name             | Required | Type   | Description |
|------------------|----------|--------|-------------|
| fileId           | True     | String | Unique file identifier. |
| fileName         | True     | String | Name of the file. |
| filePath         | False    | String | Path of the file. |
| downloadUrl      | False    | String | URL to download the file. |
| label            | False    | String | File label. |
| contentType      | False    | String | MIME type. |
| contentLength    | False    | Long   | File size in bytes. |
| author           | False    | String | User who uploaded the file. |
| fileType         | False    | String | Type/category of the file. |
| lastModifiedDate | False    | String | Last modification timestamp (ISO-8601). |

---

## Example Use Case

### Get Elements at Specific Revision with Properties and Tags

```bash
POST /mbse/api/1.0/revisions/rev_20260214_002/elements?
projectId=123
&elementTypeIds=block,requirement
&expand=PROPERTIES,TAGS
```

**Request Body:**
```json
[
  {
    "elementId": "block_101",
    "changeType": "ADD"
  },
  {
    "elementId": "requirement_55",
    "changeType": "UPDATE"
  }
]
```

---

## Implementation Guidelines

1. If detailed property/tag diff is already provided in Revision – Diff API, this API does not need to be implemented.
2. If diff is not provided, connector must:
    - Retrieve full element state at revision.
    - Return only requested elements, whose elementType falls in the provided list of elementTypeIds.
3. Connector must ensure:
    - Revision-consistent state.
    - Filtering the response based on the elementTypeIds list.
    - No mixing of data from other revisions.
    - Accurate filtering of properties and tags.

---

## Design Rationale

This API enables snapshot-based synchronization when:

- Field-level diff is unavailable.
- File-based systems do not support granular diff.
- Full element reconstruction is required.

This keeps the revision layer clean and separates:

- Revision metadata retrieval
- Element-level change detection
- Element snapshot reconstruction
