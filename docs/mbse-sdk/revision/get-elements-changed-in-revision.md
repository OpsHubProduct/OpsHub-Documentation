---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# API Name

API Name: Revision – Diff (Get Elements Changed in Revision)

---

# Overview

This API returns the list of elements changed between two revisions.

It compares:

- `parentRevisionId` (source revision)
- `revisionId` (target revision)

and returns the elements that were added or updated between these two revisions.

MBSE Core uses this API for:

- Identifying element-level changes in a revision
- Performing incremental synchronization
- Detecting newly added or modified elements

Connector implementation must:

- Compare `parentRevisionId` and `revisionId`
- Return only elements that were changed between these two revisions
- Filter changes based on the provided `elementTypeIds` if the connector allows filtering; if not, OIM will handle the filtering.
- Return results in the expected MBSE change format

---

## API URI

```bash
GET: /mbse/api/1.0/revisions/diff
    ?projectId={projectId}
    &elementTypeIds={elementTypeIds}
    &branchId={branchId}
    &revisionId={revisionId}
    &parentRevisionId={parentRevisionId}
```

---

## URI Parameters

| Name              | Mandatory | Type          | Description |
|-------------------|-----------|--------------|-------------|
| projectId         | True      | String       | ID of the project. |
| elementTypeIds    | False     | List<String> | List of element type IDs defined in `element-types` JSON configuration. If the connector allows filtering, filter and return only changes related to these element types; otherwise, OIM will handle the filtering. |
| branchId          | False     | String       | ID of the branch. If omitted, default branch behavior of the end system should apply. |
| revisionId        | True      | String       | Target revision ID for which diff is required. |
| parentRevisionId  | True      | String       | Source (previous) revision ID from which the diff must be calculated. |

---

## Behavior Rules

1. The API must return elements changed between:
    - `parentRevisionId` → `revisionId`

2. If no changes are found, return an empty list.

3. The API must return only:
    - Added elements
    - Updated elements

4. If the underlying system supports deletion tracking and deletion needs to be supported, the connector may extend `changeType` accordingly.

5. This API must not return full element data. It only returns change metadata.

---

## Expected Response Structure

The API returns a list of element change objects.

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

## Response Parameters

| Name       | Required | Type   | Description |
|------------|----------|--------|-------------|
| elementId  | True     | String | Unique identifier of the element that changed. |
| changeType | True     | String | Type of change. Possible values: `ADD`, `UPDATE`. |

---

## Optional Detailed Change Format

If the connector or end system supports field-level diff, it may return detailed change information using the extended structure.

### Detailed Change Example

```json
[
  {
    "elementId": "block_101",
    "changeType": "UPDATE",
    "elementTypeId": "Block",
    "propertiesChangedInRevision": {
      "name": {
        "oldValue": "Old Block Name",
        "newValue": "New Block Name"
      }
    },
    "tagsChangedInRevision": {
      "criticality": {
        "oldValue": "Low",
        "newValue": "High"
      }
    }
  }
]
```

---

## Detailed Change Object Structure

| Name                         | Required | Type                      | Description |
|------------------------------|----------|---------------------------|-------------|
| elementId                    | True     | String                    | ID of the changed element. |
| changeType                   | True     | String                    | `ADD` or `UPDATE`. |
| elementTypeId                | False    | String                    | ID of the element type. |
| propertiesChangedInRevision  | False    | Map<String, ValueChange>  | Map of property name to value change. |
| tagsChangedInRevision        | False    | Map<String, ValueChange>  | Map of tag name to value change. |

### ValueChange Object

| Name     | Required | Type   | Description |
|----------|----------|--------|-------------|
| oldValue | False    | Object | Previous value of the field. |
| newValue | False    | Object | New value of the field. |

---

## Change Type Enumeration

Possible values for `changeType`:

- `ADD`
- `UPDATE`

If deletion tracking is required in future, this enumeration may be extended.

---

## Connector Implementation Guidelines

Connector implementor must follow one of the following approaches depending on end system capability:

### Case 1: End System Provides Direct Element Diff

- Call native revision comparison API.
- Convert response to:
    - `elementId`
    - `changeType`
    - (Optional) detailed diff structure.

### Case 2: End System Provides Only Element IDs

- Call revision diff API.
- Extract changed element IDs.
- Map changes to expected MBSE structure.

### Case 3: End System Maintains File-Based History

If history is maintained at file level and no element-level diff API exists:

1. Retrieve file-level diff.
2. Parse file changes.
3. Identify affected elements.
4. Construct response in required MBSE format:
    - `elementId`
    - `changeType`

Connector must ensure accuracy and avoid duplicate element entries.

---

## Example Use Case

### Get Elements Changed Between Two Revisions

```bash
GET /mbse/api/1.0/revisions/diff?
projectId=123
&elementTypeIds=Block,Requirement
&revisionId=rev_20260214_002
&parentRevisionId=rev_20260214_001
```

---

## Important Notes

- This API is revision comparison only.
- It must not return unchanged elements.
- It must not return complete element data.
- It must be deterministic and consistent for the same revision pair.
- Duplicate `elementId` entries must not be returned.

---

## Design Rationale

This API separates:

- Revision metadata retrieval (`Revisions – Get`)
- Element-level change detection (`Revision – Diff`)

This separation ensures:

- Efficient polling
- Controlled synchronization
- Scalable integration design
