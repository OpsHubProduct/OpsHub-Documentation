---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# MBSE SDK Server Bootstrap Package v/s OIM version compatibility matrix

| SDK Server                                                                                                                                | OIM                 | Remarks                                                                                                                                                                                                                                                                                                                                 |
|-------------------------------------------------------------------------------------------------------------------------------------------|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [1.6.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/IgDQ5-eZor_WSZ_OMD0AnpgNAct9hePsCUCzYrbrjoP5VMs?e=hsfMV0) | \>=7.238            | To enhance the Sync Performance: <br><ul><li>Made elementTypeIds parameter optional in [Get Elements Changed In Revision API](revision/get-elements-changed-in-revision.md).</li><li>Updated [Get Elements at Revision](revision/get-elements-at-revision.md) to POST method with request body and updated response structure</li></ul> |
| [1.5.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/IgDVoYanXCKIR53wkZIGrnwyAb4YFw7Ub6LTzjd5ug1Zcm0?e=zbjYb1) | \>=7.237 and <7.238 | <ul><li>Added support for Project as an entity type</li></ul>                                                                                                                                                                                                                                                                           |
| [1.4.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/IgAmBLUYkxc7TLy8PeyTr4dnARHu0hXkm4wA7lggMZ6JMkg?e=dD3QZy) | \>=7.226 and <7.237 | <ul><li>Added rich text support for Documentation Field</li><li>Added filtering based on MetaType and identifiedStereotypes in the Owning Package field</li></ul>                                                                                                                                                                       |
| [1.3.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/IgCsdqhXFbV6TLPomLgyftNRAQp_GlC1o0Ip-wQET79hxJU?e=UdySEM) | \>=7.224 and <7.226 | <ul><li>Added support for query-based filtering using name and GUID.</li><li>Redesigned the Element Types JSON configuration for improved structure and flexibility.</li><li>Enabled support for polling entities from the first revision.</li><li>Added support for Item Flow and reference fields.</li></ul>                          |
| [1.2.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/IgA_ObXHl2RjS5Yq_8K0A5HFAeEH1uGYq2-r-cZ0vAdsl40?e=OHy4aE) | \>=7.218 and <7.224 | Support for Generalization and Usage relationship, along with renaming of realization relationship                                                                                                                                                                                                                                      |
| [1.1.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/IgASwZ7wO5lsQZXpQozVIq6kAUcbJWqBEpV5QEZxTJ4NlYk?e=p0Brbr) | \>=7.218 and <7.224 | Batching and parallel processing implemented for getting list of elements on latest state and at given revision.                                                                                                                                                                                                                        
| [1.0.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/IgB2GwvZGsFzTb8G8eOLDsoHAVGOfcyUg0Z-XDYSNM-6ZdY?e=YQ7PWC) | \>=7.218 and <7.224 | Initial Version.<br><br>OIM supports MBSE SDK connector registration from 7.218 onwards.                                                                                                                                                                                                                                                |
---

# Developer Notes
## MBSE SDK Release 1.6.0
**Breaking API changes**
- **Updated the `Get Elements at Revision` API**
    - **Changes** 
        - The API now uses `POST` instead of `GET`:
            `/mbse/api/1.0/revisions/{revisionId}/elements`
        - `elementTypeIds` is now a mandatory query parameter.
        - The list of elements whose state needs to be retrieved is now provided in the request body. Each item contains the `elementId` and `changeType`.
        - The response structure has also been updated. Each response item now contains:
            - `sourceElementId` — the ID used by the connector to identify the MBSE element.
            - `mbseElement` — the corresponding MBSE element.
    - **Purpose**
        - Moving the element list from the URL to the request body allows a large number of elements to be provided without being limited by URL length restrictions.
        - To improve the performance of synchronization and recovery operations.
    - **Reference**
        - [Get Elements at Revision](revision/get-elements-at-revision.md).


**Backward Compatible Changes**
- **Updated the `Get Elements Changed In Revision` API**
  - **Changes**
      - In the [Get Elements Changed In Revision API](revision/get-elements-changed-in-revision.md) (`/mbse/api/1.0/revisions/diff`), the `elementTypeIds` parameter is now optional.
      - If the end system supports filtering changes by element type, you can provide `elementTypeIds` in the request to have the end system perform the filtering.
      - If the end system does not support element-type filtering, you can omit `elementTypeIds`, and OIM will perform the filtering.
  - **Purpose**
    - This allows the API to work with both types of end systems without losing applicable changes.
  - **Reference**
    - [Get Elements Changed In Revision API](revision/get-elements-changed-in-revision.md)
## MBSE SDK Release 1.5.0
**Backward Compatible Changes**
- Added support for Project as an entity type

## MBSE SDK Release 1.4.0
**Backward Compatible Changes**
- Added Rich Text Support in 'Documentation' Field
- Added filtering based on MetaType and identifiedStereotypes in the 'Owning Package' field

## MBSE SDK Release 1.3.0
**Backward Compatible Changes**
- Added support for query-based filtering using name and GUID.
- Redesigned the element types json configuration for improved structure and flexibily.
- Enabled support for polling entities from first revision.
- Added support for item flow and reference fields.

**Breaking API changes**
- Added parameters for the branchName and branchDescription in the EmfBranchClient.
- Added deleteElements and bulkUpsertElements method in the EmfElementClient.![img.png](img.png)

## MBSE SDK Release 1.2.0
**Backward Compatible Changes**
- Added support for Generalization and Usage Relationship.
- Renaming for the realization link


## MBSE SDK Release 1.1.0
**Backward Compatible Changes**
- Added support for Java 25.
- Batching and parallel processing implemented for 'Get elements at revision' and 'Get elements' methods.

## MBSE SDK Release 1.0.0
### First Release of MBSE SDK Server Bootstrap Package
