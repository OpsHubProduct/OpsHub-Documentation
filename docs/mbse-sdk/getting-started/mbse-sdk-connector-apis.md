---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# Build Your Own Connector

The following table describes:

- The list of MBSE Connector SDK APIs.
- Which APIs are mandatory.
- Recommended order of implementation.
- A brief overview of how MBSE Core calls each API and the expected behavior.

Empty cells in the "Order of Implementation" column indicate optional APIs.

---

## MBSE Connector SDK APIs

| Section                         | API Name                                                                            | Required (Yes/No) | Order of Implementation | Overview                                                                                                                             |
|---------------------------------|-------------------------------------------------------------------------------------|------------------|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| **Registration APIs**           |                                                                                     | Yes | 1                       | APIs required to register and identify the connector to MBSE Core.                                                                   |
|                                 | [Connector Metadata](../registration/connector-metadata-get.md)                     | Yes |                         | Returns connector metadata and supported capabilities.                                                                               |
|                                 | [Discover SDK](../registration/discovery-api-get.md)                                | Yes |                         | Returns discovery information and SDK capabilities.                                                                                  |
| **Authentication APIs**         |                                                                                     | Yes | 2                       | APIs required to initialize and cleanup connector sessions.                                                                          |
|                                 | [Initialize](../authentication/session-initialize.md)                               | Yes |                         | Initializes connection with end system, loads cache, validates credentials.                                                          |
|                                 | [Cleanup](../authentication/session-logout.md)                                      | Yes |                         | Cleans up session resources and logs out from end system.                                                                            |
| **Metadata APIs**               |                                                                                     | Yes | 3                       | APIs required for configuration, metadata discovery, and system understanding.                                                       |
|                                 | [Get Server Info](../metadata/server-info.md)                                       | Yes |                         | Returns server-level configuration such as max page size and timezone.                                                               |
|                                 | [Get All Projects](../metadata/projects-list.md)                                    | Yes |                         | Returns all projects available in the end system.                                                                                    |
|                                 | [Get All Workspaces](../metadata/workspaces-list.md)                                | Optional |                         | Returns available workspaces if supported by the system.                                                                             |
|                                 | [Get Element Type](../metadata/element-type-get.md)                                 | Yes |                         | Returns configuration details for a given element type.                                                                              |
|                                 | [Get Stereotypes](../metadata/stereotype-details.md)                                | Yes |                         | Returns stereotype metadata definitions.                                                                                             |
|                                 | [Get Properties](../metadata/properties-list.md)                                    | Yes |                         | Returns property metadata for a given element type and stereotype.                                                                   |
|                                 | [Get Enumeration Literals](../metadata/enumeration-literals.md)                     | Yes |                         | Returns enumeration values for a property or tag.                                                                                    |
| **Multi Element Revision APIs** |                                                                                     | Yes | 4                       | APIs used for revision-based synchronization.                                                                                        |
|                                 | [Get Revisions](../revision/get-revisions.md)                                       | Yes |                         | Returns list of revisions for a project.                                                                                             |
|                                 | [Get Elements Changed In Revision](../revision/get-elements-changed-in-revision.md) | Yes |                         | Returns elements changed between two revisions.                                                                                      |
|                                 | [Get Elements At Revision](../revision/get-elements-at-revision.md)                 | Optional |                         | Returns element snapshot at a given revision. Required if diff details are not provided in the Get Elements Changed In Revision API. |
| **Element APIs**                |                                                                                     | Yes | 5                       | Core CRUD APIs for elements.                                                                                                         |
|                                 | [Get Element](../element/element-get.md)                                            | Yes |                         | Retrieves element details based on ID.                                                                                               |
|                                 | [Add Element](../element/element-add.md)                                            | Yes |                         | Creates a new element.                                                                                                               |
|                                 | [Update Element](../element/element-update.md)                                      | Yes |                         | Updates an existing element.                                                                                                         |
|                                 | [Query Elements](../element/element-query.md)                                       | Yes |                         | Searches elements based on criteria and pagination.                                                                                  |
| **Relation APIs**               |                                                                                     | Yes | 6                       | APIs to manage relationships between elements.                                                                                       |
|                                 | [Add Relation](../relation/create-relation.md)                                      | Yes |                         | Creates a relation between elements.                                                                                                 |
|                                 | [Delete Relation](../relation/delete-relation.md)                                   | Yes |                         | Deletes an existing relation.                                                                                                        |
| **File APIs**                   |                                                                                     | Yes | 7                       | APIs to manage files between elements.                                                                                               |
|                                 | [Get File Content](../file/file-get.md)                                             | Yes |                         | Reterives the File Content.                                                                                                          |
| **Branch APIs** |                                                                                     | Optional* | 8                       | Required only if branch-based synchronization is enabled.                                                                            |
| | [Get Branch](../branch/get-branch.md)                                               | Optional |                         | Retrieves branch details.                                                                                                            |
| | [Create Branch](../branch/create-branch.md)                                         | Optional |                         | Creates a new branch.                                                                                                                |
| | [Delete Branch](../branch/delete-branch.md)                                         | Optional |                         | Deletes a branch.                                                                                                                    |
| | [Merge Branch](../branch/merge-branch.md)                                           | Optional |                         | Merges a branch into the main/master/trunk branch.                                                                                   |

---


## Recommended Order of Implementation

1. Registration APIs
2. Authentication APIs
3. Metadata APIs
4. Revision APIs
5. Element CRUD APIs
6. Relation APIs
7. File APIs
8. Branch APIs (if applicable)


This order ensures:

- Connector registration is validated first.
- Session handling works properly.
- Metadata configuration is accurate.
- Revision synchronization is stable.
- Element-level operations are reliable.
- Relation handling is consistent.
- Branch lifecycle is managed safely.

---

## Mandatory vs Optional APIs

### Mandatory APIs

These APIs are required for:

- Revision-based synchronization
- Element CRUD operations
- Metadata configuration
- Connector registration

Without these, the connector cannot function.

### Optional APIs

These APIs are required only if:

- Branch-based synchronization is enabled.
- Workspace concept exists in the system.

---

## Important Notes

- All APIs must follow MBSE SDK URI structure.
- All APIs must implement standardized error handling.
- Pagination must be implemented where required.
- ISO-8601 date format must be used for timestamps.
- Expand behavior must be respected for performance optimization.
- Connector must convert all responses into MBSE DTO structures.

---

## Related Pages

- [SDK API URI Structure](mbse-sdk-api-uri-structure.md)
- [MBSE SDK Best Practices](mbse-sdk-best-practices.md)
- [APIs Required for Each Feature](mbse-apis-required-for-each-feature.md)
- [Error Handling](error-handling.md)
- [Pagination](pagination.md)
- [Passing Configuration Parameters](passing-the-configuration-parameters-to-mbse-sdk-apis.md)

---

This page serves as the master checklist for building an MBSE connector.

Implement APIs in the recommended order to ensure stable and predictable integration behavior.
