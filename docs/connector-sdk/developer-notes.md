---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# SDK Server Bootstrap Package v/s OIM version compatibility matrix


| SDK Server                                                                                                                                 | OIM                 | Remarks                                                                                                                                                                     |
|--------------------------------------------------------------------------------------------------------------------------------------------|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
 | [1.20.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/IgA5dDSkzZ6JS518k8LyTCtuAaqNkHD9amjtAaVKbXzpCCY?e=L4zR15) | \>=7.225              | Added support to wait before processing history updates to ensure that only mature and stable revisions are synchronized.                                          | 
| [1.19.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/IgCzYZnd_ofPRaW3N-z45vl5Ab68ZhIfC4P7mjRJ3PtPt0o?e=QxxBbI) | \>=7.224 and <7.225 | Added bidirectional support for attachments in complex field with multiple rows, for example, the test step field.                                                          |
| [1.18.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/IgAEkBpLrfOzSaJpQ-z0_dEMATNOApeDs0SQHvszRfNQye8?e=wKOqGa) | \>=7.217 and <7.224 | Enhanced link support to include link internal name and link direction.<br> Enhanced Test Step field synchronization with attachment & inline image/ file.                  |
| [1.17.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/EkEI6J-uYJFKv7_ePKrgqlEB9J9-oPTIo7D6r73Y2WG2oA?e=lROoA9)  | \>=7.198 and <7.217 | Added support for bulk linking and link ordering                                                                                                                            |
| [1.16.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/EvOnIixsygdIjhvfCa7vWS0BVG2vyovUYG4lzaRL1bN2UA?e=kIBnIn)  | 7.197               | Added support for systemId to store system-specific cache and cleanupGlobalCache flag to control cache cleanup.<br><br>Added support for adding multiple inline url prefix. |
| [1.15.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/EvvyUofLAjxHk-N5W0YnH_sBD6JEYO2grFg9FjWcycR0qg?e=a3RdTs)  | \>=7.189 and <7.197 | Added support for Rank synchronization                                                                                                                                      |
| [1.14.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/EpAJjYhkvjlMqInjTb8nnzsBvaBfdz935gW6Bbk-6snAkQ?e=AUW9cC)  | 7.188               | Added support for attachment file comment.                                                                                                                                  |
| [1.13.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/EhjGCtTDvpZBnqQ5Q1o-0DwBIhd_SH4YQyPgv6_g_NRKLg?e=QRWLbV)  | \>=7.184 and <7.188 | Added support for forming Remote Link using different base URL.                                                                                                             |
| [1.12.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/Eifg-bj_zBZJu0bDMeSeEmwBOzQGivZn7uSiMnlkgT4-MQ?e=r8KcUC)  | \>=7.182 and <7.184 | Added support for 'fetch mapped data only' feature.                                                                                                                         |
| [1.11.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/Elb-oBAzBfZFlQlx0vyP3pQBe3vJkKSxzPg3mm-kSu5CGQ?e=yl98Sy)  | \>=7.179 and <7.182 | Added Support for entity type and project movement.<br><br>Added provision for filtering comments after specified time.                                                     |
| [1.10.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/EviqliwYNMhFssMKncO0cfgBiHnM0VmWCKMigMttta5xxw?e=fuysA4)  | \>=7.177 and <7.179 | Optimized Entity-List API                                                                                                                                                   |
| [1.9.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/Ev8AGbZNxfNCp-fFrXE1sdYB66pZBJ8si3kZ2fdfpkNoNg?e=km0rN0)   | \>=7.174 and <7.177 | Added support for UserMention and EntityMention for MarkDown datatype and introduced support for subStepNumber in updateEntity.                                             |
| [1.8.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/EkZXYx2GibtIifkfi-1UXqYBVUSTNPIlhqKKZGDqBbT6gA?e=a9PlEw)   | \>=7.168 and <7.174 | Added support for Dynamic Retrieval of lookup fields in integration advance setting screens.                                                                                |
| [1.7.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/EtK34ZC39XVLjP9qGJXZXaYBmEKYi86_tgc011M-vSjfQA?e=a9PlEw)   | \>=7.165 and <7.168 | Added support for searching Entity Mention and User Mention in field or comment of HTML type using regex.                                                                   |
| [1.6.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/EjkO9ZHLFu1MifQbGzQ_gckBZbGKXIHWVQi_HBwIP64Rgg?e=k7zk6F)   | \>=7.162 and <7.165 | Added support for reference fields and upgraded spring boot version to 3.2.3                                                                                                |
| [1.5.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/ErdGKjtXHFJLmbQepsO9JoMB5_mYwWDexyqnsuYj8tD6YA?e=h0LjHw)   | \>=7.158 and <7.162 | Project Structure Change with respect to code organization                                                                                                                  |
| [1.4.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/ErlFZKgz_HlGl3yyeN1w3HEBjoX0X0nxV0ge6Mvl5nQGyw?e=G39xkC)   | \>=7.156 and <7.158 | Added support for Comment Author Impersonation                                                                                                                              |
| [1.3.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/Ej_3PQP_CrNHqZkXSGlOLXsBIke4XoXhp0T6e5vFfZT38g?e=WedC61)   | \>=7.153 and <7.156 | Added support for Next Page based Pagination                                                                                                                                |
| [1.2.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/Eub-SAMZhS9Brl_sppkIlN4BsNmN-zh1Ligf7q5s1yUucQ?e=ZlzvBf)   | \>=7.147 and <7.153 | Added support for Non Time-Stamp based poller and Entity-Mention synchronization                                                                                            |
| [1.1.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/EpQXywvHUFtMqzUgo-9v4R4Bxrz0G9xk90q0Y3QwIvN7fA?e=aaoX9M)   | \>=7.140 and <7.147 | Added support for delete sync                                                                                                                                               |
| [1.0.0](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/EvJdBwrcg49MmUBujzlJsN8BTQfy-ZwVjwQz-S0vP8PvcQ?e=7dg12z)   | \>=7.129 and <7.140 | Initial Version.<br><br>OIM supports SDK connector registration from 7.129 onwards.                                                                                         |

---

**Developer Notes**

> 💡 **Looking for older developer notes?**  
> Check out the [Developer Notes](https://docs.myopshub.com/oim/index.php/Developer_Notes) for versions prior to **1.6.0**.

# SDK Release 1.20.0
## Added support for wait duration before processing history updates

**Backward Compatible Changes**
- [Entity Type-Get API](entity-type-get.md#api-uri)
  - [Response payload](entity-type-get.md#response-payloaad):
  - In **history** attribute `readWaitTimeInMillis` is added.

# SDK Release 1.18.0
## Enhanced link support to include link internal name and link direction

**Backward Compatible Changes**
- [Entity Type-Get API](entity-type-get.md#api-uri)
  - [Response payload](entity-type-get.md#response-payload):
    - Within **links.linkTypes** attribute `linkTypeInternalName` and `linkTypeDirection` properties have been added.
    - In **links.fieldNameInfo** attribute `linkTypeDirectionFieldName` is added.

- [Link Create or Update API](link-create-or-update.md#api-uri) 
  - [Request payload](link-create-or-update.md#request-payload) and [Response payload](link-create-or-update.md#response-payload) 
    - The payloads have been extended to support the link direction property.
    - The `linkType` will contain the link internal name when `linkTypeInternalName` is configured in the [Entity Type-Get API](entity-type-get.md#response-payload).
    
- [Link Delete API](link-delete.md#api-uri)
  - [Request payload](link-delete.md#request-payload) and [Response payload](link-create-or-update.md#response-payload)
    - The payloads have been extended to support the link direction property.
    - The `linkType` will contain the link internal name when `linkTypeInternalName` is configured in the [Entity Type-Get API](entity-type-get.md#response-payload).


# SDK Release 1.17.0
## Added support for bulk linking and link ordering

**Breaking Changes**  
- [Link Create or Update API](link-create-or-update.md#api-uri)  
  - [Request payload](link-create-or-update.md#request-payload) has been enhanced to support adding multiple links for a given link type, and ordering in a single API call.  
- [Link Delete API](link-delete.md#api-uri)  
  - [Request payload](link-delete.md#request-payload) has been enhanced to support deleting multiple links for a given link type in a single API call.

**Backward Compatible Changes**  
- [Entity Type-Get API](entity-type-get.md#api-uri)  
  - In [Response Structure](entity-type-get.md#response-payload):  
    - In **links.linkTypes**, attribute `isBulkLinkingSupported` is added.  
    - In **links.rank.supportedRankOperations**, `MOVE_BULK_AFTER` is added.

---

# SDK Release 1.16.0
## Added support for systemId to store system-specific cache and cleanupGlobalCache flag to control cache cleanup.

**Backward Compatible Changes**  
- [Session Initialize API](session-initialize.md#api-uri)  
  - In [URI Parameters](session-initialize.md#uri-parameterss):  
    - Added query parameter of the `systemId`.  
- [Session Logout API](session-logout.md#api-uri)  
  - In [URI Parameters](session-logout.md#uri-parameterss):  
    - Added query parameter of the `systemId`.  
    - Added query parameter of the `cleanupGlobalCache`.

## Added support for adding multiple inline url prefix.

**Breaking Changes**  
- [Entity Type-Get API](entity-type-get.md#api-uri)  
  - In [Response Parameters](entity-type-get.md#response-parameters):  
    - Changed the datatype of `inlineFile.inlineFileUrlPrefix` from `String` to `List<String>`.

---

# SDK Release 1.15.0
## Added support for Rank synchronization

**Backward Compatible Changes**  
- [Entity Type-Get API](entity-type-get.md#api-uri)  
  - In [Response Structure](entity-type-get.md#response-payload):  
    - Field `rank` is added.

---

# SDK Release 1.14.0
## Added support for attachment file comment

**Backward Compatible Changes**  
- [Attachment Create API](attachment-create.md#request-body) and [Attachment Update API](attachment-update.md#request-body)  
  - In request body `fileComment` field, an optional attachment file comment is added.  
  - For example, if the attachment "Image.jpg" needs to add with the file comment "Sample trace image," we can use this file comment.

---

# SDK Release 1.13.0
## Added support for forming Remote Link using different base URL

**Breaking Changes**  
- [Entity Type-Get API](entity-type-get.md#api-uri)  
  - In [Response Structure](entity-type-get.md#response-payload):  
    - In **entityWebUrl** field, a new field `baseUrl` is added and `urlTemplate` attribute is renamed to `trailingTemplate`.  
    - These changes will be used to form a link.  
      - Example: if the original `urlTemplate` is `https://example.com/{0}/{1}/{2}`, it will now be split into:  
        - `baseUrl`: `https://example.com/`  
        - `trailingTemplate`: `{0}/{1}/{2}`.

---

# SDK Release 1.12.0
## Added support for fetch mapped data only feature

**Backward Compatible Changes**  
- [Entity–Get](entity-get.md#api-uri)  
  - In [URI Parameters](entity-get.md#uri-parameters):  
    - A new query parameter, `fieldList`, has been added.  
    - This parameter will have list of fields, and only the fields present in the `fieldList` need to be fetched.  
    - If an empty list is provided, all field values need to be returned.  
    - **Note:** No in-memory filtration is required if the endpoint API does not support field filtering. In that case, the connector can return all fields.

---

# SDK Release 1.11.0
## Added support for entity type and project movement

**Breaking Changes**  
- [Entity–Get](entity-get.md#api-uri)  
  - In [URI Parameters](entity-get.md#uri-parameters):  
    - The `entityTypeId` is changed from path parameter to query parameter.  
    - This will be used in return field values for a given entity id without filter on entityTypeId or projectId in case it is sent as null.

**Backward Compatible Changes**  
- [Entity Types-List API](entity-types-list.md#api-uri)  
  - In [Response Payload](entity-types-list.md#response-payload):  
    - New metadata for `belongsToCategories` and `projectMovementSupported` is introduced.  
    - These metadata will be used in entity type and project movement.  
      - `belongsToCategories` will help to determine in which category given entity Type belongs.  
      - `crossProjectMovementSupport` will help to determine if project movement is supported through API for the given entity Type or not.

## Added support for filtering comments after specified time

**Backward Compatible Changes**  
- [Get_Comments](get-comments.md#api-uri)  
  - In [URI Parameters](get-comments.md#uri-parameters):  
    - New parameter `afterTime` is introduced, which can be used when end system supports time based filtering on comments.

## Added archive support for entity

**Breaking Changes**  
- [Entity – Delete API](entity-delete.md#api-uri)  
  - In [URI Parameters](entity-delete.md#uri-parameters), added param `deletionType`.

**Backward Compatible Changes**  
- [Entity Types – List API](entity-types-list.md#api-uri)  
  - In [Response Payload](entity-types-list.md#response-payload), added field `isArchiveSupported`.  
- [Entity Type – Get API](entity-type-get.md#api-uri)  
  - In [Response Payload](entity-type-get.md#response-payload), added field `archiveMetadata`.

---

# SDK Release 1.10.0
## Optimized Entity-List API

**Backward Compatible Changes**  
- [Entity-List API](entity-list.md#overview)  
  - In [Response Payload](entity-list.md#response-payload):  
    - Fields provided in [fieldNameInfo in response payload for Entity Type-Get API](entity-type-get.md#response-payload) and any field which can be configured for end system storage should be part of response payload.

---

# SDK Release 1.9.0
## Added support for UserMention and EntityMention for MarkDown datatype and introduced support for subStepNumber in updateEntity

**Breaking Changes**  
- [Entity-Update API](entity-update.md#api-uri)  
  - In [URI Parameters](entity-update.md#uri-parameters):  
    - New parameter is introduced for `subStepNumber`.  
    - Only consider the `subStepNumber` change in the updateEntity if the `multiStepUpdate` field provided in the [multiStepUpdate](entity-type-get.md#response_parameters) is either `STATIC_SUB_STEPS` or `DYNAMIC_SUB_STEPS`.  
    - This parameter allows users to detect which API call to make based on Step number in which the field/fields came. Useful when there is separate API to transition Status from one state to another and all other fields can be updated in single update request to end system.

**Backward Compatible Changes**  
- [Connector_Metadata–Get](connector-metadata-get.md#api-uri)  
  - In [Response Payload](connector-metadata-get.md#response-payload):  
    - New metadata for `additionalMetadata` is introduced.  
    - This will be used to know if the connector supports user search based on `userName` and user search on `email`.

---

# SDK Release 1.8.0
## Added support for Dynamic Retrieval of lookup fields in integration advance setting screens.

**Breaking Changes**  
- [History-List API](history-list.md#api-uri), [Attachment_History-List](attachment-history-list.md#uri-parameters), [Comment_History-List](comment-history-list.md#uri-parameters), [Link_History-List](link-history-list.md#uri-parameters)  
  - In corresponding URI Parameters:  
    - New parameter `orderByDirection` is introduced.  
    - This parameter gives direction for sorting to all the fields listed in history metadata `sortableFields` set.  
- [Lookup_Field_Values-Get](lookup-field-value-get.md#api-uri)  
  - In [URI Parameters](lookup-field-value-get.md#uri-parameters):  
    - New parameter `fieldScope` is introduced.  
    - This parameter gives the Scope where Lookup values for a field are to be displayed.

---

# SDK Release 1.7.0
## Added support for searching mention in HTML data type using regex

**Backward Compatible Changes**  
- [Entity Type-Get API](entity-type-get.md#api-uri)  
  - In [Response Parameters](entity-type-get.md#response-parameters):  
    - New parameter introduced for `fieldDataType` field of `userMention` and `entityMention`.  
    - This parameter will allow user to detect mention from html data type using regex. This is useful when it's not possible to detect all the mention using html selector.

---

# SDK Release 1.6.0
## Added Support for Reference Fields

**Backward Compatible Changes**  
- [Entity Type-Get API](entity-type-get.md#api-uri)  
  - In [Response Structure](entity-type-get.md#response-payload):  
    - In `fields`, `referenceFieldMetadata` field is added.  
    - In `fieldNameInfo`, `entityNameFieldName` field is added.  

- Spring Boot version is upgraded from 2.7.8 to 3.2.3.
