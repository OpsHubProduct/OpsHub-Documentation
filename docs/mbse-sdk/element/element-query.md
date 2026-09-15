---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# API Name

API Name: Elements – Query

---

# Overview

This API searches and retrieves [elements](../getting-started/mbse-sdk-connector-apis.md#glossary) based on filtering, hierarchy scope, time range, and pagination.

MBSE Core uses this API for:

- Incremental synchronization
- Target lookup
- Criteria-based filtering
- Package-based browsing
- Bulk element retrieval

Connector responsibility:

- Apply hierarchy filters (parent + recursion).
- Apply time filters (`afterTime`, `beforeTime`) if supported.
- Apply structured filters and/or native query.
- Apply pagination.
- Respect expand options.
- Convert results into `MbseElement` objects.
- Return results in `MbseElementListResponse`.

---

## API URI

```bash
POST: /mbse/api/1.0/elements/query
    ?projectIds={projectIds}
    &elementTypeIds={elementTypeIds}
    &branchId={branchId}
    &expand=PROPERTIES,TAGS,FILES,RELATIONS
    &properties={properties}
    &tags={tags}
    &pageNumber={pageNumber}
    &pageSize={pageSize}
```

---

## URI Parameters

| Name | Mandatory | Type | Description |
|------|-----------|------|-------------|
| projectIds | Yes | List<String> | List of project IDs (comma-separated). |
| elementTypeIds | Yes | List<String> | List of element type IDs. |
| branchId | No | String | Branch ID. |
| expand | No | List<String> | Controls additional data fetch. Values: `PROPERTIES`, `TAGS`, `FILES`, `RELATIONS`. |
| properties | No | List<String> | List of property IDs to include (if PROPERTIES expanded). |
| tags | No | List<String> | List of tag IDs to include (if TAGS expanded). |
| pageNumber | Yes | Integer | 0-based page index. |
| pageSize | Yes | Integer | Number of elements per page. |

---

## Request Body

```json
{
  "parentElementIds": ["pkg_1"],
  "recursiveChildSearch": true,
  "afterTime": "2026-02-14T08:00:00Z",
  "beforeTime": "2026-02-15T08:00:00Z",
  "elementIds": ["el_1", "el_2"],
  "qualifiedNames": ["Model::System::Block"],
  "createdBy": "john.doe",
  "filters": {
    "status": "Approved"
  },
  "nativeQuery": "status = 'Approved'",
  "orderBy": [
    { "name": "updatedDate", "direction": "ASC" }
  ]
}
```

---

## Request Body Parameters

| Name | Required | Type | Description |
|------|----------|------|-------------|
| parentElementIds | No | List<String> | Restrict search to child hierarchy of given parents. |
| recursiveChildSearch | No | Boolean | If true, search recursively under parent hierarchy. |
| afterTime | No | ZonedDateTime | Return elements updated after this time. |
| beforeTime | No | ZonedDateTime | Return elements updated before this time. |
| elementIds | No | List<String> | Restrict search to specific element IDs. |
| qualifiedNames | No | List<String> | Search by qualified names. |
| createdBy | No | String | Filter by creator. |
| filters | No | Map<String,Object> | Structured filter criteria. |
| nativeQuery | No | String | Native query string (if supported). |
| orderBy | No | List<OrderBy> | Sorting rules. |

---

## Behavior Rules

### 1. Parent Filtering

- If `parentElementIds` provided:
    - Return elements under these parents.
- If not provided:
    - Return root-level elements or full project search.
- If `recursiveChildSearch = true`:
    - Search entire hierarchy under parent.
- If false:
    - Search direct children only.

---

### 2. Time Filtering

- Apply `afterTime` and `beforeTime` if supported.
- If not supported:
    - Ignore at connector level.
    - MBSE Core may filter.

---

### 3. Element ID Filtering

- If `elementIds` provided:
    - Restrict results strictly to these IDs.

---

### 4. Filters & Native Query

- If `filters` provided:
    - Apply structured criteria.
- If `nativeQuery` provided:
    - Execute directly in end system.
- If both provided:
    - Combine logically if supported.

---

### 5. Pagination

- Pagination is mandatory.
- Implement using:
    - `pageNumber`
    - `pageSize`
- Must return only requested page.

---

### 6. Expand Behavior

| Expand Value | Behavior |
|--------------|----------|
| PROPERTIES | Include properties. Filter if `properties` provided. |
| TAGS | Include tags. Filter if `tags` provided. |
| FILES | Include attached files. |
| RELATIONS | Include relations. |

If `expand` not provided:
- Return only base element metadata.

---

## Response Payload

```json
{
  "elements": [
    {
      "elementId": "block_101",
      "name": "System Block",
      "elementTypeId": "Block",
      "qualifiedName": "Model::System::Block",
      "projectId": "123",
      "createdBy": "john.doe",
      "updatedBy": "jane.smith",
      "createdDate": "2026-02-14T08:00:00Z",
      "updatedDate": "2026-02-14T09:00:00Z",
      "parentElementId": "pkg_1",
      "properties": {
        "status": "Approved"
      },
      "tags": {
        "criticality": "High"
      }
    }
  ]
}
```

---

## Response Structure

### MbseElementListResponse

| Name | Required | Type |
|------|----------|------|
| elements | Yes | List<MbseElement> |

---

## Ordering

- Respect `orderBy` rules.
- Each rule:
    - `name`
    - `direction` (`ASC`, `DESC`)
- Default ordering: system-defined if not provided.

---

## Error Handling

| HTTP Status | Description |
|------------|-------------|
| 400 | Invalid input parameters |
| 404 | Project or element type not found |
| 500 | Internal server error |

---

## Implementation Guidelines

- Avoid full-table scans where possible.
- Use native system query capabilities.
- Apply pagination at source system level.
- Avoid fetching properties/tags/files unless requested.
- Ensure ISO-8601 date format.
- Return deterministic results.

---

## Design Rationale

This API enables:

- Scalable element retrieval
- Hierarchical search
- Time-based polling
- Target lookup
- Criteria-based filtering

It is the backbone of MBSE synchronization and search functionality.
