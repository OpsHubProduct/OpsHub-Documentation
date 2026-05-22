---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

## Overview
This API describes the entity type in detail for OpsHub to be able to integrate various basic and complex data for a given entity type.  
>**Note**: It is important to return a correct response for this API as OpsHub relies heavily on these inputs to handle multiple connector tasks automatically.

## API URI
This is the URI OpsHub will execute to call this API:

```bash
GET: /entity-types/{entityTypeId}?projectId=<projectId>
```

## URI Parameters

| Name | In | Required | Type | Description |
|------|----|----------|------|-------------|
| entityTypeId | path | True | String | ‘id’ of entity type returned as response of Entity Type – List API |
| projectId | query | True | String | Project id for which entity type details need to be returned. ProjectId here will be the same as ‘id’ sent as part of `/projects` |

## Response Payload
```json

{

  "multiStepUpdate": "NO_SUB_STEPS, STATIC_SUB_STEPS, DYNAMIC_SUB_STEPS",

  "recovery": {

    "type": "FIELD_BASED, COMPARISON_BASED, HISTORY_BASED",

    "fieldName": "// If FIELD_BASED, then id of the field to store last update date"

  },

  "history": {

    "type": "FIELD_BASED, FULL_STATE_BASED",

    "revisionDateFormat": "dd/MM/YYYY’T’hh:mm:ss.SSSz",

    "isRevisionIdNumeric": "true/false | datatype: boolean",

    "revisionUserDataType": "USERNAME_AS_USER, EMAIL_AS_USER",

    "separateHistoryApis": "ATTACHMENTS, COMMENTS, LINKS",

    "sortableFields":"CREATED_UPDATED_TIME, ENTITY_ID, REVISION_ID",
    
    "readWaitTimeInMillis": "define how long OIM should wait before reading history updates to ensure only mature revisions are read | datatype: long"

  },

  "enitytScope": {

    "additionalScopeFieldName": "field id used as additional scope"

  },

  "entityWebUrl": {

    "baseUrl": "https://example.com/",

    "trailingTemplate": "browse/{0}/{1}",

    "substitutes": {

      "0": "field id of the field whose value need to be first replacement",

      "1": "field name of second replacement field"

    }

  },

  "isFieldIdConstantAcrossProjects": "true/false | datatype: boolean",

  "isInternalValueExistForLookupField": "true/false | datatype: boolean",

  "isUpdateAvailable": "true/false | datatype: boolean",

  "waitTimeInMillisIfApiResponseDelayed": "Max delay in API response in milli seconds. | datatype: number",

  "searchEntityInfo": {

    "sortableFields": "CREATED_UPDATED_TIME, ENTITY_ID, REVISION_ID",

    "isGroupingSupported": "true / false",

    "isSearchPossibleOnAnyField": "true / false",

    "isCriteriaInSystemNativeFormat": "true / false",

    "dateTimeFormat": "dd/MM/YYYY’T’hh:mm:ss.SSSz",

    "queryFieldNameInfo": {

      "entityIdFieldName": "entity id field id",

      "entityTypeIdFieldName": "entity type field id",

      "projectIdFieldName": "project id’s field id",

      "createdDateFieldName": "created date’s field id",

      "updatedDateFieldName": "updated date’s field id",

      "createdByFieldName": "created By’s field id"

    },

    "batchSizeForInQuery": "number of entities that can be passed in 'IN' or 'OR' query"

  },

  "fieldNameInfo": {

    "entityIdFieldName": "field id of unique and uneditable entity primary id field",

    "entityTitleFieldName": "field id for entity title",

    "entityDisplayIdFieldName": "field id of field that has entity display id (id any)",

    "entityTypeIdFieldName": "field id for entity type",

    "projectIdFieldName": "field id of field that contains project info for entity",

    "createdDateFieldName": "field id of Created date field",

    "updatedDateFieldName": "field id of updated date field",

    "createdByFieldName": "field id of created By field",

    "updatedByFieldName": "field id of updated By field",

    "archiveMetadata" : {
	
	"archivedByFieldName": "field id of archived By field",

	"isArchivedFieldName": "field id of is Archived field"

     }
	

  },

  "fields": [

    {

      "id": "unique id or key for each field",

      "name": "Field name",

      "dataType": "TEXT, HTML, WIKI, LOOKUP, DATE, DATE_TIME, DATE_STRING, BOOLEAN, NUMBER, USERNAME_AS_USER, TIME_UNIT, EMAIL_AS_USER, RTF, HYPERLINK, TEST_STEP, PARAMETER, REFERENCE, IMAGE, HIERARCHY",

      "isMandatory": "true/false | datatype: boolean",

      "isMultiSelect": "true/false | datatype: boolean",

      "isReadOnly": "true/false | datatype: boolean",

      "isHistorySupported": "true/false | datatype: boolean",

      "userMentionSupported": "true/false | datatype: boolean",

      "entityMentionSupported": "true/false | datatype: boolean",

      "timeUnit": "MILLISECOND, SECOND, MINUTE, HOUR, DAY",

      "dateFormat": " yyyy-MM-dd or yyyy-MM-dd’T’HH:mm:ss.SSSz",

      "canBeSetAtEntityCreateTime": "true/false | datatype:boolean",

      "updateStepNumber": "// Number starting with 1,2,3",

      "inlineFileMetadataForComplexFields": "FIELD_LEVEL_STORAGE",
  
      "referenceFieldMetadata": {
	
		"referencedEntityTypeId": "id of the entity type which is referenced through field",

		"idFieldName": "id field name which stores id or URL of the referenced entity in Entity - GET API and History - List API for base entity",

		"referenceUrl": {

			 "baseUrl": "https://example.com/",

			 "trailingTemplate": "browse/{0}/{1}",

   			 "substitutes": {

     	 			"0": "field id of the field whose value need to be first replacement",

      				"1": "field id of the field whose value need to be second replacement"

    			}

		},

		"titleFieldName": "title field name which stores title or equivalent field of the referenced entity in the Entity - GET API and History - List API for base entity"        

       },
      
      "additionalFieldMetaData": {
        
        "richTextDataType": "An additional meta of field to determine rich text data type of field.",
        
        "stepExecutionType": "An additional meta of field to store execution behavior of Test Step field"
      }

    },

    {

      "id": "unique id or key for each field",

      "name": "Field name",

      "dataType": "TEXT, HTML, WIKI, LOOKUP, DATE, DATE_TIME, DATE_STRING, BOOLEAN, NUMBER, USERNAME_AS_USER, TIME_UNIT, EMAIL_AS_USER, RTF, HYPERLINK, TEST_STEP, PARAMETER, REFERENCE, IMAGE, HIERARCHY",

      "isMandatory": "true/false | datatype: boolean",

      "isMultiSelect": "true/false | datatype: boolean",

      "isReadOnly": "true/false | datatype: boolean",

      "isHistorySupported": "true/false | datatype: boolean",

      "userMentionSupported": "true/false | datatype: boolean",

      "timeUnit": "MILLISECOND, SECOND, MINUTE, HOUR, DAY",

      "dateFormat": "yyyy-MM-dd or yyyy-MM-dd’T’HH:mm:ss.SSSz",

      "canBeSetAtEntityCreateTime": "true/false | datatype:boolean",

      "updateStepNumber": "// Number starting with 1,2,3",

      "inlineFileMetadataForComplexFields": "FIELD_LEVEL_STORAGE",
  
      "referenceFieldMetadata": {
	
		"referencedEntityTypeId": "id of the entity type which is referenced through field",

		"idFieldName": "id field name which stores id or URL of the referenced entity in Entity - GET API and History - List API for base entity",

		"referenceUrl": {

			 "baseUrl": "https://example.com/",

			 "trailingTemplate": "browse/{0}/{1}",

   			 "substitutes": {

     	 			"0": "field id of the field whose value need to be first replacement",

      				"1": "field id of the field whose value need to be second replacement"

    			}

		},

		"titleFieldName": "title field name which stores title or equivalent field of the referenced entity in the Entity - GET API and History - List API for base entity"        

       },
      
      "additionalFieldMetaData": {
        
        "richTextDataType": "An additional meta of field to determine rich text data type of field.",
        
        "stepExecutionType": "An additional meta of field to store execution behavior of Test Step field"
      }
      
    }

  ],

  "comments": {

    "userMentionSupported": "true/false | datatype: boolean",

    "entityMentionSupported": "true/false | datatype: boolean",

    "commentBodyDataType": "TEXT, HTML, WIKI",

    "commentIdDataType": "NUMBER, TEXT",

    "createdUpdatedByFieldDataType": "USERNAME_AS_USER, EMAIL_AS_USER"

    "htmlReplacementForNewLine": "<br/> or \n or null",

    "delayInCommentUpdateTimeInMillis": 2000,

    "createUpdateDateFormat": "yyyy-MM-dd'T'HH:mm:ss.SSSZ",

    "typesOfComments": [

      "Private",

      "Public",

      "etc."

    ],

    "fieldNameInfo": {

      "idFieldName": "Field name of comment id as it is received in API by end system",

      "titleFieldName": " Field name of comment title as it is received in API by end system ",

      "bodyFieldName": " Field name of comment body as it is received in API by end system ",

      "createdDateFieldName": " Field name of comment created date as it is received in API by end system ",

      "updatedDateFieldName": " Field name of comment updated date as it is received in API by end system ",

      "createdByFieldName": " Field name of comment created by as it is received in API by end system ",

      "updatedByFieldName": " Field name of comment updated by as it is received in API by end system ",

      "commentTypeFieldName": " Field name of comment type as it is received in API by end system "

    }

  },

  "attachments": {

    "updateSupported": "true/false | datatype: boolean",

    "deleteSupported": "true/false | datatype: boolean",

    "historySupported": "true/false | datatype: boolean",

    "createUpdateDateFormat": "yyyy-MM-dd'T'HH:mm:ss.SSSZ",

    "typesOfAttachments": [

      "Internal",

      "External",

      "etc."

    ],

    "fieldNameInfo": {

      "idFieldName": " Field name of attachment id as it is received in API by end system ",

      "contentUriFieldName": " Field name of attachment content URI as it is received in API by end system ",

      "renderUriFieldName": " Field name of attachment render URI as it is received in API by end system ",

      "fileNameFieldName": " Field name of attachment file name as it is received in API by end system ",

      "contentTypeFieldName": " Field name of attachment content type as it is received in API by end system ",

      "contentLengthFieldName": " Field name of attachment length as it is received in API by end system ",

      "createdOrUpdatedDateFieldName": " Field name of attachment updated as it is received in API by end system ",

      "createdByFieldName": " Field name of attachment created by as it is received in API by end system ",

      "attachmentTypeFieldName": " Field name of attachment type as it is received in API by end system ",
      
      "typeItemIdFieldName": " Field name of type id to which attachment is added as it is received in API by end system ",

      "fileCommentFieldName": " Field name of the attachment file comment as it is received in API by end system "

    }

  },

  "inlineFiles": {

    "deleteSupported": "true/false | datatype: boolean",

    "inlineFileStorageType": "ENTITY_LEVEL_STORAGE | EXTERNAL_STORAGE",

    "inlineFileUrlPrefix": ""

  },

  "links": {

    "deleteSupported": "true/false | datatype: boolean",

    "historySupported": "true/false | datatype: boolean",

    "createUpdateDateFormat": "yyyy-MM-dd'T'HH:mm:ss.SSSZ",

    "rank": {

        "rankType": "FLAT_SINGLE | FLAT_MULTIPLE | HIERARCHY_SINGLE | HIERARCHY_MULTIPLE",

        "supportedRankOperations": [

            "MOVE_BEFORE",

            "MOVE_AFTER",

            "LAST_IN_LIST",

            "MOVE_BULK_AFTER"
        ],

        "rankFieldName": "If entity stores the rank info in a field, provide that field name.",

        "rankScope": {

            "template": "{0}::{1}",

            "substitutes": {

                "0": "field name of the field whose value needs to be replacement for 0",

                "1": "field name of the field whose value needs to be replacement for 1"

            }

        }

    },

    "linkTypes": [

      {

        "linkType": "Name of the link between current entity and the other entity",
 
        "linkTypeInternalName": "Applicable only if end system returns or expects internal name of the link.",
        
        "linkTypeDirection": "Applicable only if end system supports directions in links. Possible values are FORWARD and BACKWARD.",

        "reverseLinkType": "Name of the link from the other entity to the current entity.",

        "isMultiLinkAllowed": "true/false | datatype: boolean",

        "isLinkMandatory": "true/false | datatype: boolean",

        "isBulkLinkingSupported": "true/false | datatype: boolean",

        "isExternalLink": "true/false | datatype: boolean"

      }

    ],

    "fieldNameInfo": {

      "linkTypeFieldName": "Field name of link type (parent, child, related etc.) as it is received in API by end system ",

      "linkTypeDirectionFieldName": "Field name of link direction(FORWARD, BACKWARD). Applicable only if link direction is supported by end system.",
      
      "linkedEntityIdFieldName": "Field name of linked entity id as it is received in API by end system ",

      "linkedEntityTypeFieldName": "Field name of linked entity type as it is received in API by end system ",

      "linkedEntityScopeIdFieldName": "linkedEntityScopeId | TODO: Revisit this",

      "createdDateFieldName": "Field name of link created date as it is received in API by end system ",

      "createdByFieldName": "Field name of link created by user as it is received in API by end system ",

      "linkCommentFieldName": "Field name of link comment as it is received in API by end system ",

      "externalLinkUrlFieldName": "Field name of link external URL as it is received in API by end system ",

      "isExternalLinkFieldName": "Field name of field which says if it’s an external link or not, as it is received in API by end system "

    }

  },

"userMention": {

    "userMentionDataType": "USERNAME_AS_USER / EMAIL_AS_USER",

    "mentionDetails": [

      {

        "fieldDataType": "HTML",

        "selectorOrRegex": ["Example: a[href]"],

        "mentionTemplate": "Example: <a href=\"https://example.com/users/${username}\" rel=\"${username}\"> ${displayName} </a>",

        "userDataRegex": "",

        "userDataAttributeName": "Example: href / rel / data-mention"

      },

      {

        "fieldDataType": "WIKI",

        "selectorOrRegex": "Example: [~ohusermention:(.*?)]",

        "mentionTemplate": "Example: [~accountId:${username}]"

      },

      {

        "fieldDataType": "TEXT",

        "selectorOrRegex": "Example: @OH_USER@ohusermention:(.*?)@OH_USER@",

        "mentionTemplate": "Example: ${username} <${email}>"

      }

    ]

  },

  "entityMention": {

      "mentionDetails": [

        {

          "fieldDataType": "HTML",

          "selectorOrRegex": ["Example: a[href]"],

          "mentionTemplate": "Example: <a href=\"https://example.com/users/${username}\" rel=\"${username}\"> ${displayName} </a>",

          "entityIdAttribute": {

            "dataAttributeName": "href",

            "dataRegEx": "/browse/([A-Z_a-z0-9-]+)"
          },

          "entityTypeAttribute": {

            "dataAttributeName": "href",

            "dataRegEx": ".*\\?detail=/(.*?)(?=/\\d+)"
          },

          "entityProjectAttribute": {

            "dataAttributeName": "href",

            "dataRegEx": ".*([a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12})/_workitems/edit/.*"
          }

        }

      ],
      "entityURLDetails": [

       {
          "entityWebURLMatcher": "a[href~=/browse/[A-Z_a-z0-9-]+-\\d+]",

          "entityIdDataSelector": ".*\\/browse/([A-Za-z0-9-]+-\\d+)]"
       }

      ]

    }

}
```
> **Internal note:** For attachment, comment, link: `readSupported`, `writeSupported` can be derived from sync direction of entityType.

# Response Parameters





| Parent Parameters | Name | Required | Type | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|------------------|------|----------|------|-------------|
| |multiStepUpdate | True | Enum | OpsHub uses this flag to identify if all fields can be updated in single update entity call or multiple update entity calls are required. For example: If all the fields under fields can be updated in single API call in end system, then pass NO_SUB_STEP. But let’s say, if the end system has a separate API to transition entity from one state to another, then connector can pass STATIC_SUB_STEPS or DYNAMIC_SUB_STEPS depending on need. If ‘DYNAMIC_SUB_STEPS‘ is being passed, then /entities/{entityTypeId}/sub-steps-for-update API is mandatory to implement.<br><br> * *NO_SUB_STEP*: All the fields of an entity can be updated in single update entity API call. <br><br>* *STATIC_SUB_STEPS*: Step number of the field to be updated is predefined. So, every time when multiple fields are updated in single update, based on updateStepNumber of field, the order of field can be decided for the update. <br><br>* *DYNAMIC_SUB_STEPS*: The order in which the fields can be passed to the end system for the update is dynamically decided based on field value. E.g., if the entity is getting closed along with few other fields getting updated. In this case, other fields must be updated first and then entity status should be updated to closed. |
| **recovery** | |True | |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| |Type | True | Enum | Helps OpsHub determine if the given transaction has already taken place in failure and recovery scenarios.<br><br> *HISTORY_BASED*: (Preferred) Entity History – Get (/entities/{entityTypeId}/history) must be implemented, if this is passed. OpsHub will use the entity revision to identify if a given transaction was completed or not.<br> *FIELD_BASED*: Add a custom field of type text to end system (E.g., oh_last_update) to perform recovery. Ensure this field is passed under ‘fields’ of this API.<br><br> *COMPARISON_BASED*: This is a less reliable recovery mechanism as compared to HISTORY_BASED or FIELD_BASED. OpsHub compares last entity state saved in its database with current state in end system, to determine if last transaction was completed or not. <br><br> **Select this recovery mechanism if the pollerType for entity type is NON_TIME_BASED.**                                                                                                                                                                                                                                                                                                                                                                                         |
|| fieldName | True, if recovery type=FIELD_BASED | String | In case of FIELD_BASED recovery, the field id of the custom field can be used by OpsHub for storing recovery flags. (E.g., oh_last_update). Note: This field should not be updated by other users in the end system.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| **History** | | False | | Pass this parameter, if the pollerType for entity type is ENTITY_WISE_HISTORY                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| |Type | True | Enum | How the end system returns entity history?<br><br> *FIELD_BASED*: In a given revision, the old and new values are obtained only for those fields of an entity that were changed in a given transaction.<br>*FULL_STATE_BASED*: For a given revision, the end system returns the entity field state for all fields as of that revision.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| |revisionDateFormat | True | String | Date format for the field, which contains revision date time                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| |isRevisionIdNumeric | True | Boolean | When true, all the revision sorting will happen considering numeric value of revision id. When false, all the revision sorting will happen considering string value of revision id. Default will be false                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| |revisionUserDataType | True | Enum | Data type of the revision user. <br><br> *EMAIL_AS_USER*: When the user’s email is provided in the revision user field.<br><br> *USERNAME_AS_USER*: When the username is provided in the revision user field.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| |separateHistoryApis | False | String | This is an optional input. Provide only if the end system has a separate history API for attachments, comments and/or links.<br>If separate history APIs is available for attachments, comments and/or links, provide the following as per API availability:<br><br> *ATTACHMENTS*: When separate history API for attachments is available. <br><br> *COMMENTS*: When separate history API for comments is available.<br><br>*LINKS*: When separate history API for links is available.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| |sortableFields | False | Set`<Enum>` | Send set of fields for which end system supports sorting on history API. The fields can be sent in any order in the list. Connector should sort all the fields provided in the set.<br>Example:<br> `If end system supports sorting on ENTITY_ID, CREATED_UPDATED_TIME and REVISION_ID: `sortableFields = {CREATED_UPDATED_TIME, ENTITY_ID, REVISION_ID}``<br><br> `If end system supports sorting only on CREATED_UPDATED_TIME: `sortableField={CREATED_UPDATED_TIME}``.<br>In case of history, CREATED_UPDATED_TIME is same as REVISION_DATE_TIME.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|  |readWaitTimeInMillis | False | Long | In some systems, updates to an entity’s history are not immediately available in their final form. This is because the end system may still be processing recent changes, and the latest revision data may not yet be fully updated.<br>Instead of recording every individual change, such systems may combine multiple updates made to the same field within a short period into a single final update.<br><br>**For Example:**<br>* In the Aha system, updates made to the same field within a 5-minute interval are merged into a single revision. This means intermediate changes during that time are not stored separately and only the final result is available.<br><br>By default, OIM does not wait for this cooling period before fetching revisions. As a result, it may read data before it has fully stabilized.<br><br>If the end system has such cooling period and you want OIM to wait and process only stable revisions, provide the duration of the delay in milliseconds in this field.                                                                                                                                                                                                                                                                    |

| Parent Parameter | Name | Required | Type | Description |
|-----------|------|----------|------|--------------|
| **entityScope** | | False |  | If entity scope is decided based on only entity type and any additionalScopeField (like a project) is not required, this field can be set to null. |
| | **additionalScopeFieldName** | True, if entityScope is passed. | Boolean | If entity scope is decided based on only entity type, this field can be set to null.<br>If entity scope is dependent on entity type as well as any other field of the entity (e.g., projectId, workspaceId, or domainId), provide that field name of the entity.<br>Ensure that this field name matches one of the field names in “entityFieldNameInfo”. |
| **entityWebUrl** |  |False |  | Pass this if you want the Remote Entity Link feature enabled for the connector. Otherwise, do not include entityWebURL in response. |
|  |**baseUrl** | True |String| String containing the base URL of the end system.<br>e.g., if the actual URL format is "https://example.com/browse/{0}/{1}" then set baseUrl as "https://example.com/" and trailingTemplate as "browse/{0}/{1}".<br>This URL is used to form the Remote Link. If value for the field "Base URL for Remote Link" is not given in the system configuration form, the baseUrl will be used by default to form Remote Link. |
| | **trailingTemplate** | True |String| String template containing the trailing part of the URL format.<br>Provide all the dynamic parts in the URL as substitute numeric variables, e.g., {0}, {1} etc.<br>e.g., If the projectId is 101 and entity is 10001, the base URL is https://example.com/ and trailingTemplate is browse/<projectId>/<entityId>.<br>So, the actual web URL will be "https://example.com/browse/101/10001". |
|  |**substitutes** | True |List| Map containing all the substitute numeric parameters to the replacement field name of the entity.<br>e.g., {"0": "projectIdFieldName", "1": "entityIdFieldName"}<br><br>In the “trailingTemplate":<br>* The value of parameter {0} will be replaced with actual value coming in field project id for the entity.<br>* The value of parameter {1} will be replaced with actual value coming in entity id for the entity.<br>Ensure that this field name matches one of the field names in “fieldNameInfo”. |
| **isFieldIdConstantAcrossProjects** | | True |Boolean| Set to 'True' if the field id for the same field is same in different projects; else, set to 'False'.<br>e.g., If for a field with the display name 'Priority', field id in Project A is '100' and for Project B is '101', then send 'False'.<br>On the other hand, if the field id is the same (say 'priority' or '100') for all projects, then send 'True'.<br><br>If this is 'True', in FieldsMeta, we will use Field Id; otherwise, we will use Field Name. |
| **isInternalValueExistForLookupField** | | |Boolean| Set to 'True' if the lookup fields have different internal and display values.<br>Set to 'False' if the lookup fields have only one value, the display value.<br><br>Example 1:<br><pre>"isInternalValueExistForLookupField": true<br> [ { "id": "low", "value": "Low" }, { "id": "medium", "value": "Medium" }, { "id": "high", "value": "High" } ]</pre><br>Here, priority field has values having different internal value and display value.<br><br>Example 2:<br><pre>"isInternalValueExistForLookupField": false, [ { "id": "Low", "value": "Low" }, { "id": "Medium", "value": "Medium" }, { "id": "High", "value": "High" } ]</pre> Here, the priority field does not have a different value for internal value. |


| Parent Parameter | Name | Required | Type | Description |
|-----------|------|----------|------|--------------|
| **isUpdateAvailable** | | False | Boolean | Set to 'True' if update is possible on the entity.<br>Set to 'False' if entity is create only. |
| **waitTimeInMillisIfApiResponseDelayed** | |False | Number | In some systems, there is a delay in API returning updated data in response.<br><br>e.g., If an entity is updated:<br>* If within next second we try to fetch list of entities, the system might not return the last updated entity.<br>  But if we get the list of updated entities after 2 seconds, the system will start returning the entities.<br>  This delay might be due to indexing in the end system.<br><br>* Similarly, for history based systems, if we update an entity:<br>  The last revision might not be available in the audit API within a second or two.<br>  But if we query the revisions after 3 seconds, the system will start returning the revision.<br>  This delay might be due to system inserting audit records separately than the actual entity update.<br><br>OIM handles this type of delays for update up to 2 seconds (2000 milliseconds).<br>* If the end system has delay of up to 2 seconds, the value can be kept null.<br>* If the end system has delay of more than 2 seconds, provide the maximum delay value in milliseconds in this field. |

| Parent Parameter | Name | Required | Type | Description |
|-----------|------|----------|------|--------------|
| **searchEntityInfo** | | True |  | All the metadata for querying end system to search entities. |
| | **sortableFields** | False | Set`<Enum>` | Send set of fields for which end system supports sorting. For searchEntityInfo no need to pass REVISION_ID in sortableFields set.<br>*E.g. If end system supports sorting on both ENTITY_ID and CREATED_UPDATED_TIME,*<br>`sortableFields = {ENTITY_ID, CREATED_UPDATED_TIME}` |
| | **isGroupingSupported** | True | Boolean | True (Preferred) if end system support order by for both created/updated time and entity id fields, otherwise false. If it is false, OpsHub will sort the results. |
| |**isSearchPossibleOnAnyField** | True | Boolean | If criteria storage needs to be in the end system, then only set the field to true.<br>*The field selected for end system criteria should be queryable. If that's true, pass true here.*<br>To get more details on end system criteria storage, refer [[ Integration_Configuration#Criteria_Configuration | Criteria Configuration ]] |
| |**isCriteriaInSystemNativeFormat** | True | Boolean | Send 'True' if configured criteria in OIM will be in the end system native query format.<br>If 'Yes', the criteria can be the exact query that the end system supports.<br>If 'No', the criteria should be OpsHub standard JSON format query. |
| |**dateTimeFormat** | True | String | Date time format supported within the query.<br>E.g., (where updatedDate > ‘2021-12-31 00:00:00’). Here, dateTimeFormat should be set as `yyyy-MM-dd HH:mm:ss` |
| |**queryFieldNameInfo** | False |  | Query field names should be provided for entity id, entity type id, project id, created date, updated date and created by field.<br>If the query field name for the above fields is the same as their field id given in 'fieldNameInfo', then set this field as 'Null'. Otherwise, provide the end system field names used for querying. If these field names are provided, they will be used to generate queries. Here is a sample format of data to be passed under this parameter:<br><pre>"entityIdFieldName": "entity id field id",<br>&nbsp;&nbsp;"entityTypeIdFieldName": "entity type field id",<br>&nbsp;&nbsp;"projectIdFieldName": "project id’s field id",<br>&nbsp;&nbsp;"createdDateFieldName": "created date’s field id",<br>&nbsp;&nbsp;"updatedDateFieldName": "updated date’s field id",<br>&nbsp;&nbsp;"createdByFieldName": "created by field id"</pre> |
| |**batchSizeForInQuery** | False | Integer | Number of entities end system supports in "IN" or "OR" query. Default will be 250.<br>*E.g. for IN query:* `entityId IN (1, 2, 3)`<br>*E.g. for OR query:* `(entityId = 1) OR (entityId = 2) OR (entityId = 3)` |

| Parent Parameter | Name | Required | Type | Description |
|-----------|------|----------|------|--------------|
| **fieldNameInfo** | | True |  | Provide the end system field details for all the fields that need to be integrated |
|  |  |  |  |For below fields, specify name of the field under which OpsHub will get or send given information for an entity from SDK |
| |**entityIdFieldName** | True | String | Name of the field that contains a unique and uneditable primary id of the entity |
| | **entityTitleFieldName** | False | String | Name of the field that contains title of the entity (For e.g. name, title, summary). Provide this input only if field is to be synchronized as reference field. |
| |**entityDisplayIdFieldName** | True | String | Name of the field that contains a user friendly id of the entity (For e.g. in Jira Issue Key will be entity display field and Issue Id will be entity id) |
| |**entityTypeIdFieldName** | True | String | Name of the field that contains type (Requirement, Bug, etc.) of the entity |
| |**projectIdFieldName** | True | String | Name of the field that contains the project id in which the entity exists |
| | **createdDateFieldName** | True | String | Name of the field that contains the created date of the entity |
| |**updatedDateFieldName** | True | String | Name of the field that contains the last updated date of the entity |
| | **createdByFieldName** | True | String | Name of the field that contains the created by user details of the entity |
| |**updatedByFieldName** | True | String | Name of the field that contains the updated by user details of the entity |
| | **archiveMetadata** | False | Object | Pass this metadata if the entity supports archive operation.<br><pre>"archiveMetadata": {<br>&nbsp;&nbsp;"archivedByFieldName": "Name of the field that contains Archived by User details of the entity",<br>&nbsp;&nbsp;"isArchivedFieldName": "Name of the field that contains If Entity is Archived details of the entity"<br>}</pre> |

| Parent Parameter | Name | Required | Type | Description |
|-----------|------|----------|------|--------------|
| **fieldNameInfo.fields**|  | True |  | Details of all the fields that user want to integrate via SDK |
| | **id** | True | String | Internal name of the field. Always pass internal name only even if field meta is different across projects. OIM will handle the different internal names for the field having the same display name in different projects |
| | **name** | True | String | Display name of the field |
| |**dataType** | True | Enum | Data Type of the field which OIM understands. TEXT, HTML, WIKI, LOOKUP, DATE, DATE_TIME, DATE_STRING, BOOLEAN, NUMBER, USERNAME_AS_USER, TIME_UNIT, EMAIL_AS_USER, RTF, HYPERLINK, TEST_STEP, PARAMETER, REFERENCE, IMAGE, HIERARCHY<br>For example, the end system data type is 'string' but for OIM it's 'TEXT'. So, set dataType as 'TEXT'<br><br>If a field contains sub-fields that can have attachments, inline images, or files at the sub-field level, then it is classified as 'Complex Field' and the data type of this field is considered a 'Complex Data Type'.<br>For example, the Test Step field contains multiple sub-fields, and these sub-fields can have attachments, inline images or files. Hence, TEST_STEP is considered a 'Complex Data Type'.<br><br>Current Complex Data Types: TEST_STEP |
| | **additionalFieldMetaData** | False | Object | This property can be used to set additional meta data of field.<br>For example, the 'Test Step' field is a complex field with nested fields, such as 'Description,' 'Expected Result,' etc. If the 'Description' is of the 'HTML' type, then set the richTextDataType of the 'Test Step' field to 'HTML' inside 'additionalFieldMetaData'.<br><pre>"additionalFieldMetaData" : {<br>&nbsp;&nbsp;"richTextDataType" : "An additional meta of field to determine rich text data type of field."<br>&nbsp;&nbsp;"stepExecutionType" : "An additional meta of field to store execution behavior of Test Step field."<br>}<br><br>Possible values of stepExecutionType:<br>1) ALL_STEP: provide if all the steps are required in request body while editing steps <br>2) SINGLE_STEP: provide if the request can be executed for a single step (other steps remain un-changed)<br><br>Example 1: If all steps are required in request body,<br>{<br>&nbsp;&nbsp;...,<br>&nbsp;&nbsp;"additionalFieldMetaData":{<br>&nbsp;&nbsp;&nbsp;&nbsp;"richTextDataType":"HTML"<br>&nbsp;&nbsp;&nbsp;&nbsp;"stepExecutionType":"ALL_STEP"<br>&nbsp;&nbsp;},<br>&nbsp;&nbsp;...,<br>}<br><br>Example 2: If the request can be executed for a single step (other steps remain un-changed),<br>{<br>&nbsp;&nbsp;...,<br>&nbsp;&nbsp;"additionalFieldMetaData":{<br>&nbsp;&nbsp;&nbsp;&nbsp;"richTextDataType":"HTML"<br>&nbsp;&nbsp;&nbsp;&nbsp;"stepExecutionType":"SINGLE_STEP"<br>&nbsp;&nbsp;},<br>&nbsp;&nbsp;...,<br>}</pre> |
| |**timeUnit** | True |  | If the dataType is TIME_UNIT, this field is required. "MILLISECOND, SECOND, MINUTE, HOUR, DAY" |
| | **dateFormat** | True |  | If the dataType is DATE, this field should only have the date format. E.g., yyyy-MM-dd<br>If dataType is DATE_TIME, this field should have date time format. E.g., yyyy-MM-dd HH:mm:ss.SSS z |
| |**isMandatory** | True | Boolean | Send true if the field is mandatory, otherwise send false |
| | **isMultiSelect** | True | Boolean | Send true if the field is of type lookup or user and multiple values can be selected, otherwise send false |
| | **isReadOnly** | True | Boolean | Send true if the field is read only and cannot be written, otherwise send false |
| | **isHistorySupported** | True | Boolean | Send true, if for /entity-types request, pollerType is ‘ENTITY_WISE_HISTORY’ and end system tracks changes on this field, under revisions. E.g., if the Entity Title/Name is updated and the end system track history like Name updated from ‘oldName’ to ‘New title’, then send True. Send false, otherwise. |
| | **userMentionSupported** | False | Boolean | Send true if users can be mentioned (@Smith) in the given field, otherwise return false |
| | **entityMentionSupported** | False | Boolean | Send true if entities can be mentioned (@entity) in the given field, otherwise return false |
| | **canBeSetAtEntityCreateTime** | True | Boolean | Send true if the field value can be set at the time of entity creation, otherwise false |
| |**inlineFileMetadataForComplexFields** | False    | Enum    | set FIELD_LEVEL_STORAGE if the field stores attachment at field level; otherwise, the storage type mentioned in inline file data will be used by default. |
| | **updateStepNumber** | False | Number | Required only if you are returning ‘STATIC_SUB_STEPS’ in ‘multiStepUpdate’ from this API. Step number in which the field can be updated. Field group number – where group is for update groups. Number starting with 1,2,3....<br>For example, if there is separate API to transition Status from one state to another and all other fields can be updated in single update request to the end system, then send 1 for all fields except Status. For Status, send 2. For any update request, OpsHub will call update entity SDK API twice, once with payload for all other fields and second time only with Status field<br><br>If the end System allows the Entity Type movement and Project movement then this will be required if you are returning 'STATIC_SUB_STEPS' or 'DYNAMIC_SUB_STEPS' in 'multiStepUpdate' from this API:<br><br>**updateStepNumber for entityTypeIdFieldName:**<br>- "-3": In case the end system have different API for Entity Type and Project Movement. Or the end system doesn't support Project Movement.<br>- "-6": In case the end system have same API for Entity Type and Project Movement.<br><br>**updateStepNumber for projectIdFieldName:**<br>- "-2": In case the end system have different API for Project and Entity Type Movement. Or the end system doesn't support Entity Type Movement.<br>- "-6": In case the end system have same API for Entity Type and Project Movement.<br><br>*If no metadata for the updateStepNumber for either entityTypeIdFieldName or projectIdFieldName is provided then by default they will be treated as having separate API for Entity Type and Project Movement.*<br>*In case of different updateStepNumber of entityType and project, If both entityType and project movement is found supported then the order for update operation will first be Project Movement and then Entity Type movement.* |
| |**referenceFieldMetadata** | False | Object | Pass this metadata if the field is to be synchronized as reference field.<br><pre>referenceFieldMetadata: {<br>&nbsp;&nbsp;referencedEntityTypeId: id of the entity type which is referenced through field. For e.g., if in Bug Entity, release is a reference field, provide id of the release entity type.<br><br>&nbsp;&nbsp;idFieldName: Provide the field name which stores id or URL of the referenced entity in Entity - GET API and History - List API for base entity. If end system provides both id and url of the referenced entity, provide the name of the field which stores id.<br><br>&nbsp;&nbsp;Example 1: If the response of the getting Bug API is as follows:<br>&nbsp;&nbsp;{<br>&nbsp;&nbsp;&nbsp;&nbsp;"id": "391",<br>&nbsp;&nbsp;&nbsp;&nbsp;"fields": {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"release": {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"releaseId": "100",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"description": "This release addresses major customer escalations and some critical defects",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"releaseName": "Release 1",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"archived": false<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>&nbsp;&nbsp;}<br>&nbsp;&nbsp;Here, id field name of the referenced entity is "releaseId".<br><br>&nbsp;&nbsp;Example 2: If the response of getting base entity API is as follows:<br>&nbsp;&nbsp;{<br>&nbsp;&nbsp;&nbsp;&nbsp;"bugRef": "https://example.com/bug/391",<br>&nbsp;&nbsp;&nbsp;&nbsp;"fields": {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"release": {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"releaseRef": "https://example.com/project1/release/100",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"description": "This release addresses major customer escalations and some critical defects",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"releaseName": "Release 1",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"archived": false<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>&nbsp;&nbsp;}<br><br>&nbsp;&nbsp;Here, id field name of the referenced entity is "releaseRef".<br><br>&nbsp;&nbsp;referenceUrl: Provide this input if end system's API provides link to url of the referenced entity instead of id. If end system provides both id and url of the referenced entity, do not include referenceUrl in response.<br>&nbsp;&nbsp;For example 2, if link to url is: "https://example.com/{0}/{1}/{2}" then referenceURl.baseUrl: https://example.com/,  referenceURl.trailingTemplate: {0}/{1}/{2}<br>&nbsp;&nbsp;And referenceUrl.substitutes would be {0, "projectIdFieldName", 1, "entityTypeIdFieldName", 2, "entityIdFieldName"}<br><br>&nbsp;&nbsp;titleFieldName: Provide the field name which stores title or equivalent field of the referenced entity in the Entity - GET API and History - List API for base entity. If end system's APIs' do not have name of the referenced entity in Entity - GET API and History - List API, set this input to null.<br>&nbsp;&nbsp;For example 2, titleFieldName would be releaseName.<br>}</pre> |

| Parent Parameter | Name | Required | Type | Description |
|-----------|------|----------|------|--------------|
| **comment** |  | False | |Pass this parameter if you want to integrate comments for a given entity type. Otherwise, do not send the comment parameter at all. If this parameter is passed, SDK must implement all the Comment APIs. |
| |**fieldNameInfo** | True | Object | If the comment parameter is sent back, then it is mandatory to send fieldNameInfo. The user needs to send the field names as they will be sent by SDK to OpsHub when reading comments and from OpsHub to SDK when adding comments. OpsHub will try to find the given information in the field name specified as part of the data sent here.<br><pre>{<br>&nbsp;&nbsp;"idFieldName":&nbsp;"id",<br>&nbsp;&nbsp;"titleFieldName":&nbsp;"title",<br>&nbsp;&nbsp;"bodyFieldName":&nbsp;"body",<br>&nbsp;&nbsp;"createdDateFieldName":&nbsp;"created",<br>&nbsp;&nbsp;"updatedDateFieldName":&nbsp;"updated",<br>&nbsp;&nbsp;"createdByFieldName":&nbsp;"createdBy",<br>&nbsp;&nbsp;"updatedByFieldName":&nbsp;"updatedBy",<br>&nbsp;&nbsp;"commentTypeFieldName":&nbsp;"commentType"<br>}</pre> |
| |**userMentionSupported** | False | Boolean | Send true if the user mention supported within comments; otherwise, false. |
| |**entityMentionSupported** | False | Boolean | Send true if the user mention supported within comments; otherwise, false. |
| |**commentBodyDataType** | True | Enum | TEXT, HTML, WIKI |
| |**commentIdDataType** | True | Enum | NUMBER, TEXT |
| |**createdUpdatedByFieldDataType** | False | Enum | Pass this parameter if you need user data while creating comment. Example, you want to create comment with same user as source endpoint. If you require username send USERNAME_AS_USER, if you require email address send EMAIL_AS_USER. |
| |**htmlReplacementForNewLine** | True | String | Exact value for new line character in the comment.<br>Possible values are: ‘<br/>’, ‘\n’ or null. |
| |**createUpdateDateFormat** | True | String | Date format for created and updated dates of the comment. |
| |**delayInCommentUpdateTimeInMillis** | False | Number | Expected delay between entity update time and comment update time.<br>There are systems in which comment update is delayed after entity update time. In such systems, identify the maximum delay that may be there in comment update time after entity update time.<br>If there is no delay in the system, the below value can be set as 0.<br>If there is delay of let say up to 2 seconds, set the value to 2000 (in millis). If the delay is up to 5 seconds, set the value to 5000. |
| |**typesOfComments** | True | List`<String>` | The supported list of comment types. E.g., Internal, External, Work Notes, Additional etc. OpsHub will display these comment types under comment mapping. The user can map comment types across connectors to decide the type of comments they want to integrate. |

| Parent Parameter | Name | Required | Type | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|-----------|------|----------|------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|**attachment** |  | False |  | Pass this parameter if you want to integrate attachments for a given entity type. Otherwise, do not send the attachment parameter at all.<br>If this parameter is passed, SDK must implement all the Attachment APIs.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| |**fieldNameInfo** | True | Object | If the attachment parameter is sent back, then it is mandatory to send fieldNameInfo. The user needs to send field names as they will be sent by SDK to OpsHub when reading attachments and from OpsHub to SDK when adding or updating attachments. OpsHub will try to find the given information in the field name specified as part of the data sent here.<br><br><pre>{<br>&nbsp;&nbsp;"idFieldName":&nbsp;"id",<br>&nbsp;&nbsp;"contentUriFieldName":&nbsp;"uri",<br>&nbsp;&nbsp;"renderUriFieldName":&nbsp;"renderUri",<br>&nbsp;&nbsp;"fileNameFieldName":&nbsp;"fileName",<br>&nbsp;&nbsp;"contentTypeFieldName":&nbsp;"contentType",<br>&nbsp;&nbsp;"contentLengthFieldName":&nbsp;"contentLength",<br>&nbsp;&nbsp;"createdOrUpdatedDateFieldName":&nbsp;"updated",<br>&nbsp;&nbsp;"createdByFieldName":&nbsp;"createdBy",<br>&nbsp;&nbsp;"attachmentTypeFieldName":&nbsp;"attachmentType",<br>&nbsp;&nbsp;"typeItemIdFieldName":&nbsp;"typeItemId"<br>}</pre><br>**contentUriFieldName:** The field which has the value as the URL to get/download the content of the attachment. If there's no such field in the end system, keep the fieldName as 'contentUri' and set the download link in that field in the actual attachment object.<br><br>**renderUriFieldName:** The field which has value as the URI to render/display the content of the attachment.<br><br>**Note:** This URI is not used to download an attachment. For downloading the attachment URI, refer to **contentUriFieldName**.<br><br>Example: If an inline image is shown with the `<img>` tag, render URI is the value of the `src` attribute of the `<img>` tag. |
| |**updateSupported** | True | Boolean | Send true if the end system supports updating attachment via API; otherwise, false. If false, OpsHub will simulate update attachment behaviour by deleting the attachment and adding a new version.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| |**deleteSupported** | True | Boolean | Send true if the end system has an API to delete the attachment; otherwise, false.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| | **historySupported** | True | Boolean | Does the system support history for attachment? True if yes, else false.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| |**createUpdateDateFormat** | True | String | Date format for created and updated dates of the attachment.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| |**typesOfAttachments** | True | List&lt;String&gt; | Types of attachments supported by the system: INTERNAL, EXTERNAL, etc.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |


| Parent Parameter | Name | Required | Type | Description |
|-----------|------|----------|------|--------------|
|**inlineFile** | | False |  | Pass this parameter if you want to integrate inline files for a given entity type. Otherwise, do not send this parameter at all.<br>Attachment APIs must be implemented to integrate inline files. |
| |**deleteSupported** | True | Boolean | Does the system allow deleting inline files? |
| |**inlineFileStorageType** | True | Enum | Is the inline file/attachment stored at the entity or global level in the system?<br><br>Possible values:<br>1) ENTITY_LEVEL_STORAGE: When inline files are stored in the entity itself<br>2) EXTERNAL_STORAGE: When inline files are stored at the system level<br>3) FIELD_LEVEL_STORAGE: When inline files are stored in the field itself |
| |**inlineFileUrlPrefix** | True | List&lt;String&gt; | What is the prefix of inline files?<br>This is used to identify if an inline file or image URL is the URL to some external site or the system's URL.<br><br>Provide the common initial part of the inline files URL. E.g., If the system has inline file URLs like these:<br>- https://media.example-system.com/files/file1.png<br>- https://media.example-system.com/files/file2.docx<br>- https://media.example-system.com/files/file3.pdf<br><br>In this case, the inline file URL prefix is: "https://media.example-system.com/files" |


| Parent Parameter | Name | Required | Type    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|-----------|------|----------|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **link**         | | False |         | Pass this parameter if you want to integrate entity relationship for a given entity type. Otherwise, do not send this parameter at all. Links APIs must be implemented to integrate links                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|  |**fieldNameInfo** | True | Object  | <pre>{<br>&nbsp;&nbsp;"linkTypeFieldName":&nbsp;"linkType",<br>&nbsp;&nbsp;"linkTypeDirectionFieldName":&nbsp;"linkDirection",<br>&nbsp;&nbsp;"linkedEntityIdFieldName":&nbsp;"linkedEntityId",<br>&nbsp;&nbsp;"linkedEntityTypeFieldName":&nbsp;"linkedEntityType",<br>&nbsp;&nbsp;"linkedEntityScopeIdFieldName":&nbsp;"linkedEntityScopeId",<br>&nbsp;&nbsp;"createdDateFieldName":&nbsp;"createdDate",<br>&nbsp;&nbsp;"createdByFieldName":&nbsp;"createdBy",<br>&nbsp;&nbsp;"linkCommentFieldName":&nbsp;"linkComment",<br>&nbsp;&nbsp;"externalLinkUrlFieldName":&nbsp;"externalLinkUrl",<br>&nbsp;&nbsp;"isExternalLinkFieldName":&nbsp;"isExternalLink"<br>}</pre>                                                                                                                                                                                                      |
|                  | deleteSupported | True | Boolean | Does the system allow to delete link?                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                  | historySupported | True | Boolean | Does the system support history for link?                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|                  |createUpdateDateFormat | True | String  | Date format for created and updated dates of link                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|                  |**linkTypes** | True |         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|                  |linkType | True | String  | Name of link type: Parent, Child, Relates To, Blocked By, etc                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|                  | linkTypeInternalName | False | Sring   | Specifies the unique system identifier for the link relationship: parent, relates_to etc. This value is used for interactions with end system and is not intended for display purposes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|                  | linkTypeDirection | False | Enum    | This field is required when same linkTypeInternalName is used for two different link relationships in the end system. For example, `parent` is internal link name for `is parent of` and `has parent`. In such cases, you must provide `linkTypeDirection` to specify how the link should be created relative to the current entity.<br><br> Possible values:<br>1) FORWARD: Use this value when the `linkType` defines the relationship from the current entity to the other entity. For example, if the linkType is `is parent of` and the current entity is the parent of the other entity, select `FORWARD` value.<br>2) BACKWARD: Use this value when the `reverselinkType` defines the relationship from the other entity to the current entity. For example, if the reverseLinkType is `has parent` and the current entity is the child entity, select `BACKWARD` value. |   
|                  |reverseLinkType | True | String  | Name of its reverse link. E.g., if the link type is Parent, then the opposite linkType is Child, i.e. Entity E1 is the parent of entity E2, and E2 is the child of E1                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                  |isMultiLinkAllowed | True | Boolean | True: If multiple links of this type can be created. False: if only one link of this type can be created. For example: Adding only one parent is allowed to be added for any entity, so set multiLinkAllowed to false for Parent Type. On the other hand, for the ‘Related’ link type, any number of links can be added, so send true                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                  |isLinkMandatory | True | Boolean | True: If link of this type is mandatory for entity create or update. False: If link of this type is not mandatory for entity create or update. For example, it might be mandatory to have a Parent link to another work item for sub-task or task entity type. In this case, send true for the Parent link type for Task                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|                  |isBulkLinkingSupported | True | Boolean | True: If bulk linking is supported via API. False: If bulk linking is not supported via API. For example, Bug and task can be linked by relates link type. Multiple tasks (with link type - relates) can be added and removed via a single API. In this case, send true for relates link type for Bug                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |


| Parent Parameter | Name | Required | Type | Description |
|-----------|------|----------|------|-------------|
| **link.rank** | **rank** | False |  | If entity type supports keeping ordering / ranking of entities, provide metadata for that.<br>e.g., If entities can be ranked and the rank is preserved in the end system, it supports rank.<br><br>In below example, order of 1.1, 1.2, 1.3 are stored and can also be changed and preserved.<br>Similarly order of 2.1 and 2.2 is also preserved.<br><pre>- 1<br>  - 1.1<br>  - 1.2<br>  - 1.3<br>- 2<br>  - 2.1<br>  - 2.2</pre><br>The order can be stored in a field, e.g., rank.<br>The order can also be maintained through siblings (before and after).<br><br>Pass null if rank is not supported by entity type in the end system. |
|  | rankType | True | Enum | The way entities are ranked in the end system.<br><br>* **FLAT_SINGLE**: Entities of same type can only be ranked together.<br><pre>Bug1<br>Bug2<br>Bug3</pre><br>* **FLAT_MULTIPLE**: Entities of different types can be ranked together.<br><br>Bug1<br>Story1<br>Bug2<br>Story<br><br> * **HIERARCHY_SINGLE**: Entities of same type can be ranked in a tree structure.<br><pre>Bug1<br>Bug2<br>  - Bug3<br>  - Bug4<br>Bug5</pre><br>* **HIERARCHY_MULTIPLE**: Entities of different types can be ranked together in a tree structure.<br><pre>Epic 1<br>Story 1<br>&nbsp;&nbsp;- Bug 2<br>&nbsp;&nbsp;- Story 2<br>&nbsp;&nbsp;- Story 3<br>Epic 3</pre> |
|  | supportedRankOperations | True | List`<String>` | List of rank operations supported by the system for ranking entities.<br> * MOVE_BEFORE: Moves current entity before its sibling under a linked entity<br> * MOVE_AFTER: Moves current entity after its sibling under a linked entity<br> * LAST_IN_LIST: Move current entity at the end of the list under its linked entity.<br> * MOVE_BULK_AFTER: Reorders multiple child entities under a parent after a specific sibling.<br><br>Example:<br>Consider the below scenario, where entity type for entities Epic 1 and Epic 2 is Epic and entity type for entities Story 1, Story 2, Story 3, Story 4 and Story 5 is Story<br>Epic 1<br>&nbsp;&nbsp;- Story 1<br>&nbsp;&nbsp;- Story 2<br>&nbsp;&nbsp;- Story 3<br>&nbsp;&nbsp;- Story 4<br>&nbsp;&nbsp;- Story 5<br>Epic 2<br><br>MOVE_BEFORE: Story 3 is moved before Story 2.<br>Here, current entity is Story 3, siblingEntity is Story 2, and linked entity is Epic 1<br><br><br>MOVE_AFTER: Story 2 is moved after Story 4.<br>Here, current entity is Story 2, siblingEntity is Story 4, and linked entity is Epic 1<br><br>LAST_IN_LIST: Story 2 is moved at the last of the list under Epic 1.<br>Here, current entity is Story 2, and linked entity is Epic 1<br><br><br>MOVE_BULK_AFTER: The position of Story 3 and Story 5 are swapped. Now entities under Epic 1 are in following order - Story 1, Story 2, Story 5, Story 4, Story 3<br>Here, current entity is Epic 1, sibling entity is Story 2, and linked entities are Story 5, Story 4 and Story 3<br><br>Note:<br> * MOVE_BULK_AFTER should be provided for the entity under which links can be ordered in bulk manner. In the above example, MOVE_BULK_AFTER should be provided for entity type Epic.<br> * MOVE_BEFORE, MOVE_AFTER, and LAST_IN_LIST should be provided for the entity whose order is being changed. In the above example, these should be provided for entity type Story.<br> * If MOVE_BULK_AFTER is supported for an entity (e.g., Epic), it is not required to configure MOVE_BEFORE, MOVE_AFTER, or LAST_IN_LIST in the linked entity's (e.g., Story) metadata.
|  | rankFieldName | False | String | If entity stores the rank information in a field, provide that field name. Example: stack rank in Azure DevOps, rank in Jira|
|  | rankScope | False | Object | A scope in which the rank of an entity can be uniquely identified.<br><br>e.g., If the rank is uniquely identified under a project, the project id will be the scope of the rank.<br><br>If the rank is uniquely identified under a project and a module, the '{projectId} {moduleId}' will be the scope of the rank.<br><br>If the rank is always unique in the system (across projects, across modules, across components), the scope can be set as null. |


| Parent Parameter | Name | Required | Type | Description |
|------------|------|-----------|------|--------------|
| **link.rank.scope** |  |  |  |  |
|  | template | True | String | String template for rank scope.<br><br>What is the scope made of?<br><br> * If scope is just projectId, provide template as `{0}` and provide substitutes for projectId field name.<br>* If scope is projectId and entityType, provide template as `{0}{1}` and provide substitutes for projectId and entityTypeId field names.<br><br><pre>e.g., "{0}", "{0}{1}", "{0}::{1}", etc.</pre><br>If the projectId is 101 and entityType is 10001,<br><br> * If "{0}::{1}" is provided as template and substitutes are provided for projectId and entityTypeId, the actual scope will be "101::10001". |
|  | substitutes| True | Object | Map containing all the substitute numbers used in template and field name that needs to be replaced against given substitute.<br>The substitute field name can be any field in the entity object.<br><br>**e.g.,**<br>If a template is "{0}::{1}", substitute map can be as follows:<br>`{"0": "projectIdFieldName", "1": "entityTypeIdFieldName"}`<br><br>In the template:<br> * The value of parameter {0} will be replaced with actual value of project id for the entity.<br> * The value of parameter {1} will be replaced with actual value of entity type id for the entity. |

| Parent Parameter | Name | Required | Type | Description |
|------------|------|-----------|------|--------------|
| **userMention** |  | False |  |  |
| | userMentionDataType  | True | Enum | In the case of a given user mentioned, what data will SDK send for that user?<br>*USERNAME_AS_USER*: user's username<br>*EMAIL_AS_USER*: user's email address<br><br>Depending on the data type, OpsHub will search for required user information from the user API. |
|  | **mentionDetails** | True |  |  |
|  | fieldDataType | True | Enum | Type of usermention detection system for field or comment. Each type correlates with a data type of field or comment.<br>For e.g., HTML, WIKI, MARKDOWN, TEXT, HTML_REGEX (If mention containing field is HTML type and all mentions are not detected with html selector, instead provide HTML_REGEX enum and provide a regex in selectorOrRegex that can detect the mention). |
|  | selectorOrRegex | True | List<String> | If the usermention detection system used is of type WIKI or TEXT, return regex to search usermention.<br>Example: return `\\[~accountId:([a-z0-9.]+)\\]` for searching `[~accountId:john.doe]` tags.<br><br>The regex should have 3 parts but only 1 group.<br>The regex must have only 1 group, corresponding to the user field's value as per userMentionDataType.<br><br>*Prefix:* \\[~accountId:<br>*Infix:* ([a-z0-9.]+)<br>*This part will be replaced with username or email*<br>*Only part for username/email should be provided as the group '()'*<br>*Postfix:* \\]<br><br>If the usermention detection system used is of type HTML, return HTML tag selector to search usermention.<br><br>Example:<br>If the usermention tag is `<a>` tag having 'href' attribute, return `a[href]` to search for usermention.<br>Return `a[href]` for `<a href="https://example.com/users/john.doe" rel="john.doe"> John Doe </a>` as the mention tag.<br><br>If HTML tag selector didn't work, use HTML_REGEX as fieldDataType and return regex to search usermention.<br>Example: return `"mentionUser\s(\w+)"` for searching john_doe and jane_doe from data such as:<br>`mentionUser john_doe is working with mentionUser jane_doe`<br><br>*It's important that regex has only 1 group and that 1 group captures the user data corresponding to the user field's value as per userMentionDataType.* |
|  | mentionTemplate | True | String | Usermention template that will be used to create a usermention tag for the target system. As template variables, following variables can be used:<br><br>${id} : id of the user.<br>${username} : Username of the user.<br>${email} : Email of the user.<br>${displayName} : Display name of the user.<br><br>If null value is expected and default template variable value needs to be provided, ':-' operator can be used.<br><br>Examples:<br>${displayName:-Display Name}: This will replace this template variable with 'Display Name' if value of displayName is not present.<br>${displayName:-}: This will replace this template variable with '' (empty string) if value of displayName is not present.<br><br>As per various data types, mention templates can vary.<br><br>**Examples:**<br>HTML: `<a href="https://example.com/users/${username}" rel="${username}"> ${displayName} </a>`<br>Resolved: `<a href="https://example.com/users/john.doe" rel="john.doe"> John Doe </a>`<br><br>Wiki: `[~accountId:${username}]`<br>Resolved: `[~accountId:john.doe]`<br><br>Text: `${username} <${email}>`<br>Resolved: `john.doe <john.doe@email.com>` |
|  | userDataRegex | False |  | Regex to extract user data out of HTML tag attribute or inner text of tag.<br><br>This field is only needed when #fieldDataType is HTML and user data has to be extracted from HTML tag attribute or inner text.<br>This field can be null when #fieldDataType is not HTML.<br>It can also be null if one of the user field values is exact HTML attribute value or inner text.<br>This regex must have only 1 group which corresponds to the value of the user field as per #userMentionDataType.<br><br>**Examples:**<br>1. `<a href="https://example.com/users?name=john.doe"> John Doe </a>`<br>To extract the username from `href`, set `userDataRegex` to `".*[?&]name=([a-z.]+)"`.<br><br>2. `<a href="https://example.com/users/101"> @john.doe </a>`<br>To extract the username from inner text, set `userDataRegex` to `"@([a-z.]+)"`.<br><br>3. `<a href="https://example.com/users/101" rel="john.doe"> John Doe </a>`<br>Here, `rel` attribute's exact value is username. So, no need to provide regex. The userDataRegex can be null.<br><br>4. `<a href="https://example.com/users/101"> john.doe </a>`<br>Here, the inner text's exact value is username. So, no need to provide regex. Hence, the userDataRegex can be null. |
|  | userDataAttributeName | False | String | Name of the HTML tag attribute which contains user field value as per #userMentionDataType.<br>This field is only needed when #fieldDataType is HTML.<br>This field can be null when #fieldDataType is not HTML.<br>If for HTML data type, userDataAttributeName is null, HTML tag's inner text will be considered to have user field value. |


| Parent Parameter | Name | Required | Type | Description |
|------------------|------|-----------|------|-------------|
| **entityMention** |  | False |  |  |
|  | **mentionDetails** | True |  |  |
|  | **fieldDataType** | True | Enum | Type of entity mention detection system for field or comment. Each type correlates with a data type of field or comment. <br><br>For example: **HTML**, **WIKI**, **MARKDOWN**, **TEXT**, **HTML_REGEX** (If mention containing field is HTML type and all mentions are not detected with HTML selector, instead provide **HTML_REGEX** enum and a regex in `selectorOrRegex` that can detect the mention). |
|  | **selectorOrRegex** | True | List `<String>` | If the entity mention detection system used is of type **WIKI** or **TEXT**, return regex for which entity mention needs to be checked.<br><br>The regex must have only one group, corresponding to the entity mention’s value as per `fieldDataType`. <br>**Example:** `\[~([a-z0-9.]+)\]` would search for all `~entitymention` tags.<br><br>If the detection system is **HTML**, return the selector for which entity mention needs to be checked.<br>**Example:** `doc.select("a[href]")` will search for all anchor tags having an `href` attribute.<br><br>If the HTML tag selector didn’t work, use **HTML_REGEX** as `fieldDataType` and return regex to search entity mention.<br>**Example:** return `"workitem\s(\d+)"` for searching entity with id `123` and `456` from data such as `workitem 123 depends on workitem 456`.<br><br> *It's important that the regex has only one group, and that group captures the entity id of the mention.* |
|  | **mentionTemplate** | True | String | The `entityMention` template that will be used to create an entity mention tag for the target system.<br><br>As template variables, the following variables can be used:<br>${entityId} – id of the entity<br>${entityDisplayId} – display id of the entity<br>${entityProject} – project name of the mention scope<br>${entityProjectId} – project id of the mention scope<br>${entityType} – entity type of the mention scope<br><br>As per various data types, mention templates can vary.<br><br>**Examples:**<br>HTML: `<a href="https://example.com/${projectId}/_entity/edit/${entityId}" data-vss-mention="version:1.0">#${entityDisplayId}</a>`<br>Resolved: `<a href="https://example.com/Prj-101/_entity/edit/101" data-vss-mention="version:1.0">#Bug-101</a>`<br><br>Wiki: `https://example.com/browse/${entityId}\|smart-link` <br>Resolved: `https://example.com/browse/DCPA3-7 \|smart-link` <br><br>Text: `${entityId} <${entityDisplayId}>`<br>Resolved: `101 <Bug-101>` |
|  | **entityIdAttribute** | True |  | Parameters to specify the entity id to be read from text, regex, or HTML attribute name.<br>For HTML tag element, attribute name is required.<br>For Wiki, regex is required. |
|  | **dataAttributeName** | False | String | This field is only required when `fieldDataType` is **HTML**. It can be null otherwise.<br>This field contains the name of the HTML tag attribute which contains the entity field value.<br>If `fieldDataType` is **HTML** and this field is null, the HTML tag’s inner text will be considered to have the entity field value. |
|  | **dataRegEx** | False | String | This field is used to extract entity information such as entity id, entity type, project id, or project name from the text.<br><br>In case of HTML, this extracts data from an HTML tag attribute or inner text, based on the selector in `selectorOrRegex`.<br>In case of WIKI, this extracts data from matched text using the selector provided.<br><br>This field is only required when `fieldDataType` is HTML and Id data has to be extracted from HTML tag attribute or inner text. It can be null otherwise or when the id value directly matches HTML content. |
|  | **entityTypeAttribute** | False |  | If end system provide entity type corresponds to mentioned entity along with the mentioned entity id then it is recommended to provide the meta information to extract or read entity type information from mentioned tag.<br><br>If this parameter is not given then OpsHub will search mentioned entity using mentioned id parameter without the entity type and it would be considered that entity id is sufficient, otherwise OpsHub will search mentioned entity using entity type along with id. Examples:<br><br>**Examples:**<br>HTML: `<a class="cke-link-popover-active" href="https://www.example.com/#/23468038167ud/defects?detail=/defect/669232438245">Entity101</a>`<br>WIKI: `[DCPA3-7\|https://www.example.com/browse/DEFECT/DCPA3-7] [displayText\|url]`<br>For above entity mentioned tag the text 'defect' in html example and 'DEFECT' in wiki example is entity type.<br><br>WIKI: `[DCPA3-7\|https://opshub.atlassian.net/browse/DCPA3-7][displayText\|url]`, For above tag: entity type does not exist as part of the mentioned tag, so end system do not require to provide this parameter entityTypeAttribute. |
|  | **entityProjectAttribute** | False |  | If end system provide project corresponds to mentioned entity along with the mentioned entity id then it is recommended to provide the meta information to extract or read project information from mentioned tag. <br><br>If this parameter is not given then OpsHub will search mentioned entity using mentioned id parameter without the project and it would be considered that entity id is sufficient, otherwise OpsHub will search mentioned entity using project along with entity id.<br><br>**Examples:**<br>HTML: `<a href="https://www.example.com/40723eb0-0857-4970-a4f4-8cf657085847/_entity/edit/101" data-vss-mention="version:1.0">#Bug-101</a>`<br>WIKI: [DCPA3-7\|https://www.example.com/browse/TESTP/DCPA3-7][displayText\|url]<br>For above entity mentioned tag the text '40723eb0-0857-4970-a4f4-8cf657085847' in HTML example and 'TESTP' in WIKI example is project of mentioned entity.<br><br>WIKI: [DCPA3-7\|https://www.example.com/browse/DCPA3-7][displayText\|url], For above tag: project does not exist as part of the mentioned tag, so end system do not require to provide this parameter entityProjectAttribute. |
|  | **entityURLDetails** | False |  | This field supports reverse sync for source URL/target URL option.<br><br>Provide the matcher or selector for the matching entity URL of the end system.<br>If the system supports HTML mentions, provide a JSoup matcher for URLs within `href`.<br>If the system supports Wiki, provide a regex for URLs.<br>If both HTML and Wiki mentions are supported, provide a list of entity URL details in mention metadata. |
|  | **entityWebURLMatcher** | False | String | This field contains regex or selector to match entity web url |
|  | **entityIdDataSelector** | False | String | This field contains regex to read the entity id from web url |
