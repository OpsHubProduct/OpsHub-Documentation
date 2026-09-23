---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# Prerequisites

## User Privileges

* Create a user in Aras Innovator that is dedicated for <code class="expression">space.vars.OIM</code>. The user shouldn't perform any other action from Aras Innovator user interface. Refer to [Add User in Aras Innovator](aras.md#add-users) section to learn how to add a new user in Aras Innovator.
* The user identity of the user dedicated for <code class="expression">space.vars.OIM</code> must have the following permissions for the 'item type' to be integrated:

| **Permission Types**        | **Justification**                                                                                                                                                                          | **Needed When**                                                                                                                                                                                                                                                                                                                                                             | **How To**                                                                                                                                                                                                                   |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Get                         | To get values of each field for particular item of 'item type' to be integrated                                                                                                            | Aras Innovator is source system,target system or both.                                                                                                                                                                                                                                                                                                                      | To learn how to provide user with the Get permission, refer to [Give Necessary Permissions to User for Itemtype](aras.md#give-necessary-permissions-to-user-for-itemtype) section.                                           |
| Can Discover                | To get the list of items present for a given itemtype.                                                                                                                                     | Aras Innovator is source system,target system or both.                                                                                                                                                                                                                                                                                                                      | To learn how to provide user with the Can Discover permission, refer to [Give Necessary Permissions to User for Itemtype](aras.md#give-necessary-permissions-to-user-for-itemtype) section.                                  |
| Update                      | To update an item.                                                                                                                                                                         | Aras Innovator is target system. Also,when Aras Innovator is source system and Update Permission is required for Remote Id or Remote Link configuration in Integration .Please check '''Tracking Id and Link of Entities Across Systems''' section on [Integration Configuration](../integrate/integration-configuration.md) page to learn about Remote Id and Remote Link. | To learn how to provide user with the Update permission, refer to [Give Necessary Permissions to User for Itemtype](aras.md#give-necessary-permissions-to-user-for-itemtype) section.                                        |
| Can Add                     | To create an item: The user is allowed to create record from the Aras Innovator System (through the UI and API both) only when the user's identity is allowed in the "Can Add" tab         | Aras Innovator is target system.                                                                                                                                                                                                                                                                                                                                            | To learn how to assign "Can Add" permission to user's identity on particular itemtype, refer to [Allow Can Add permission to User](aras.md#assign-identity-on-item-type) section.                                            |
| Life Cycle State Transition | To update the state during transition, the role in Life Cycle transition needs to be set as '''Administrators''' for the Integration User \[configured in the <code class="expression">space.vars.OIM</code>]. | When Aras is the target system.                                                                                                                                                                                                                                                                                                                                             | To learn how to provide user with the Lifecycle State Transition permission, refer to [Assign Life Cycle Transition Permission for Item Type](aras.md#assign-life-cycle-state-transition-permissions-for-item-type) section. |

## Versionable Item Type 

* For any Item Type in Aras Innovator, the versions/history for the item gets generated only when the item is versionable. Hence for <code class="expression">space.vars.OIM</code> to synchronize the items with their revisions, they need to be versionable.
* In case they are not versionable, <code class="expression">space.vars.OIM</code> will synchronize the item as per the current state of that item, available at the time of synchronization. Follow [Make Item Type Versionable](aras.md#make-item-type-versionable) in the Appendix section to learn how to make item types versionable.

## Hosting Opshub Aras Service 

<code class="expression">space.vars.OIM</code> requires this service to communicate with Aras Innovator server. It acts as a communication layer between Aras Innovator and <code class="expression">space.vars.OIM</code>.

### System Prerequisites

* Configure <code class="expression">space.vars.OIM</code> Aras Service on a machine that has .NET Framework version 4.7.2 or a higher version installed.
* Please refer to the following [link](https://docs.microsoft.com/en-us/dotnet/framework/get-started/system-requirements) for information on software and hardware requirements for installing .NET Framework 4.7.2.

### Installation Steps

{% include "../.gitbook/includes/aras-installtion-steps.md" %}

# System Configuration

Before the user continues with the integration, he/she must first configure Aras Innovator System. Refer to [System Configuration](../integrate/system-configuration.md) to learn step-by-step process to configure a system. See the screenshot given below for reference:

<div align="center"><img src="../assets/Aras_System.png" alt="" width="1100"></div>

| **Field Name**       | **Description**                                                                                                                                                                                                                                  |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **System Name**      | Provide a unique name to the Aras Innovator System.                                                                                                                                                                                              |
| **Version**          | Provide version for Aras Innovator Instance. Check [Get Aras Innovator Version](aras.md#get-aras-innovator-version) in the Appendix section to learn how to get Aras Innovator version.                                                          |
| **Instance URL**     | Provide URL for Aras Innovator Instance. Example: `<hostname>/InnovatorServer/Server/InnovatorServer.aspx`                                                                                                                                       |
| **User Name**        | Provide username of the user dedicated for <code class="expression">space.vars.OIM</code>. Please ensure that user has the necessary permissions. Refer to [User privileges](aras.md#user-privileges) for permissions required by user identity. |
| **User Password**    | Provide password of user dedicated for <code class="expression">space.vars.OIM</code> - use plain text if FIPS is disabled, or MD5-hashed if FIPS is enabled.                                                                                    |
| **Database name**    | Provide Aras Innovator Database name to which the connection needs to be done. Refer to [Get Database Name](aras.md#get-database-name) in the Appendix section to learn how to get Database name.                                                |
| **Web Service URL**  | Provide URL for the hosted OpsHubArasService. Refer to [Hosting opshub Aras service](aras.md#hosting-opshub-aras-service) to learn how to host <code class="expression">space.vars.OIM</code> Aras Webservice.                                   |
| **Metadata Details** | Override default entity properties using metadata configuration.. Refer to [Understanding JSON Input](aras.md#understanding-json-input) to learn how to specify the metadata details.                                                            |

* If the system is deployed on HTTPS and a self-signed certificate is used, then the user should import the SSL Certificate to be able to access the system from <code class="expression">space.vars.OIM</code>. Check [Import SSL Certificates](../getting-started/ssl-certificate-configuration.md) to learn how to import SSL certificate.

### Understanding JSON Input

* The entity metadata details can be provided at the time of system configuration in the field 'Metadata details' [in the form of JSON] in the below-mentioned use case:
  * Use Case:
    * This configuration is required when:
      * An item type is used as a reference field in field mapping for synchronization, and 
      * The referenced entity’s display name is configured using a field other than the default **name** field.
  * Configuration Requirement:
    * In Aras, the primary display field of an entity can be customized. Refer to [Create custom property](aras.md#create-custom-property) section for getting the internal-name of the primary display field.
    * If the display field differs from the default name, it must be specified in the JSON under: **PrimaryNameField**
    * If not configured, the integration will assume **name** as the default display field.
  * Reason:
    * The primary display field is not exposed through the API, so the integration cannot automatically determine which field is used for display.
  * Example:
    * A Requirement item type contains a reference field (e.g., PartReference) pointing to Part. 
    * This field is included in synchronization. 
    * By default:
      * Part uses name as its display field → this value is used in sync. 
      * If the display field is customized:
        * The correct field must be defined in PrimaryNameField.
        * This ensures accurate synchronization of the reference value.
        
> **Note**:
> The value for PrimaryNameField must be the internal field name. 
> Separate configurations can be defined for different item types.

```json
{    
  "Part": {
    "PrimaryNameField": "name"
  },
  "Product": {
    "PrimaryNameField": "title"
  }
}  
```

# Mapping Configuration

Map the fields between Aras Innovator and the other system to be integrated to ensure that the data between both the systems synchronize correctly.
Check [Mapping Configuration](../integrate/mapping-configuration.md) to learn the step-by-step process to configure mapping between the systems.

<div align="center"><img src="../assets/Aras_System_mapping_5.png" alt="" width="1250"></div>

## Version Control of Aras Innovator Items (OH_Version)

Aras Innovator creates a new version (generation) of a versionable item every time the item is edited. As <code class="expression">space.vars.OIM</code> edits the item for every change it synchronizes, it adds a generation to the item's version history in Aras Innovator. Map the **OH_Version** field if the versions in Aras Innovator are to be controlled.

### About the OH_Version Field

* **OH_Version** is available in the list of fields for every item type.
* It is a **boolean** field and it is **not mandatory** to map it. If it is not mapped, the items are versioned by default and it creates a version for every change.
* It is not an actual property of the item type in Aras Innovator, and no value is stored against it in Aras Innovator. Its value only decides whether the write performed by <code class="expression">space.vars.OIM</code> creates a new generation of the item, or updates the current generation of the item.
* The item type should be versionable for this field to have any effect. Refer to [Versionable Item Type](aras.md#versionable-item-type) section.

| **Value resolved for OH_Version**             | **Behaviour in Aras Innovator**                                                                                                                                     |
|-----------------------------------------------| ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Field is not mapped (or resolves to no value) | A new generation of the item is created. This is the default behaviour.                                                                                             |
| `true`                                        | A new generation of the item is created.                                                                                                                            |
| `false` or `0`                                | The change is written to the current generation of the item. The item is updated, i.e. its 'Modified On' and 'Modified By' change, but no new generation is created. |


### Operations for Which OH_Version is Considered

| **Operation performed by OpsHub Integration Manager**                              | **Does the operation create a new generation?**                     | **Is OH_Version considered?**                                                                                                                                                                                                                          |
| ------------------------------------------------------------------------------------------------------ |---------------------------------------------------------------------| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Create an entity                                                                                       | The item is created with generation 1                               | Not applicable. A create always results in generation 1.                                                                                                                                                                                               |
| Update field values                                                                                    | Yes                                                                 | Yes                                                                                                                                                                                                                                                    |
| Add or remove a relationship                                                                           | Yes                                                                 | Yes                                     |
| Add an attachment                                                                                      | Yes                                                                 | Yes                                                                                                                                                                                                                                                    |
| Delete an attachment                                                                                   | No. Only the relationship between the item and the file is deleted. | Not applicable                                                                                                                                                                                                                                         |
| Add a comment                                                                                          | No                                                                  | Not applicable                                                                                                                                                                                                                                         |
| Change the state, i.e. Life Cycle transition                                                           | No. The item is promoted, it is not edited.                         | Not applicable                                                                                                                                                                                                                                         |

### When to Use the OH_Version Field

Map the **OH_Version** field when:

* Versions in Aras Innovator are to be created only for the changes made by the users, and not for every change synchronized by <code class="expression">space.vars.OIM</code>.
* A single change in the source system should not create multiple versions in Aras Innovator. For example, a change that updates fields and also adds a relationship or an attachment is written as separate edits, and each edit creates a version.
* The rule for creating a version is specific to the organization. The value can be a fixed `true` or `false`, or it can be decided for each entity using an Advanced XSLT script.

### Configure the OH_Version Field in the Mapping

1. Open the mapping with Aras Innovator as the target system.
2. Select **OH_Version** from the list of the target fields and keep the source field as **--NONE--**.
3. Configure the value of the field in one of the following ways:
   * **Same behaviour for all the entities:** Configure **false** as the value using [Default Value Mapping](../integrate/mapping-configuration.md#default-value-mapping), so that the changes are always written to the current generation of the item.
   * **Decision for each entity:** Click ![XSLT Icon](../assets/XSLT_icon_blue.png) for this field and configure the Advanced XSLT for it. Refer to [View/Edit XSLT Configurations options](../integrate/mapping-configuration.md#view-edit-xslt-configurations-options) and [Advance Mapping Utility](../integrate/advance-mapping-utility.md) for the utilities which can be used in the XSLT script. The XSLT script has to return `false` when the change is to be written to the current generation of the item, and `true` when the item is to be versioned.
4. Save the mapping.

**Sample XSLT script**

The following XSLT script writes the change to the current generation of the item when the item was last modified by the user configured in the Aras Innovator system in <code class="expression">space.vars.OIM</code>, and lets Aras Innovator create a new generation when a user has changed the item since the last synchronization.

```xml
<OH_Version xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <!-- The integration user, as its value can appear in the 'modified_by_id' field of the item -->
  <!-- Replace the value of ohIntegrationUser with the user configured in the Aras Innovator system in OpsHub Integration Manager. -->
  <xsl:variable name="ohIntegrationUser" select="'<integration_user_id>'"/>
  <xsl:variable name="ohEventType" select="translate(normalize-space(string(SourceXML/opshubEventType)), 'abcdefghijklmnopqrstuvwxyz', 'ABCDEFGHIJKLMNOPQRSTUVWXYZ')"/>
  <xsl:choose>
    <!-- Create: the item is created with generation 1 in this synchronization, so the relationships and the
         attachments added right after it should not version it -->
    <xsl:when test="$ohEventType = 'CREATE'">false</xsl:when>
    <xsl:otherwise>
      <!-- Find the Aras Innovator item to which the source entity is synchronized -->
      <xsl:variable name="ohTargetInfo" xmlns:utils="http://com.opshub.eai.core.utility.OIMCoreUtility" select="utils:getTargetEntityInfoBySourceEntityId(string($sourceSystemId), string(SourceXML/opshubEntityId), string($targetSystemId), '', '')"/>
      <xsl:choose>
        <!-- The entity is not synchronized to Aras Innovator yet: version the item -->
        <xsl:when test="count($ohTargetInfo) = 0">true</xsl:when>
        <xsl:otherwise>
          <xsl:variable name="ohArasId" xmlns:entityInfo="http://com.opshub.dao.eai.OIMEntityInfo" select="string(entityInfo:getEntityInternalId($ohTargetInfo))"/>
          <xsl:variable name="ohLastModifiedBy" xmlns:utils="http://com.opshub.eai.core.utility.OIMCoreUtility" select="normalize-space(string(utils:getEntityFieldValue(string($workflowId), string($targetSystemId), '', '', $ohArasId, 'modified_by_id')))"/>
          <xsl:choose>
            <!-- The item could not be read: version the item -->
            <xsl:when test="$ohLastModifiedBy = ''">true</xsl:when>
            <!-- The last change on the item was written by the integration: update the current generation -->
            <xsl:when test="contains($ohIntegrationUser, $ohLastModifiedBy)">false</xsl:when>
            <!-- A user has changed the item since the last synchronization: version the item -->
            <xsl:otherwise>true</xsl:otherwise>
          </xsl:choose>
        </xsl:otherwise>
      </xsl:choose>
    </xsl:otherwise>
  </xsl:choose>
</OH_Version>
```

**Points to consider while writing the XSLT script**

* A blank value means 'create a version'. If the XSLT script should decide 'do not create a version' by default, return `false` explicitly using `xsl:otherwise`, instead of leaving the output empty.
* On a create event, the entity does not exist in Aras Innovator yet, so any condition which reads the target item returns a blank value. Handle the create event explicitly, the way it is handled in the sample XSLT script.

# Integration Configuration

Set polling time as the time after which the user wants to synchronize data between Aras Innovator and the other system to be integrated. Also, define parameters and conditions, for integration, if any. Check [Integration Configuration](../integrate/integration-configruation.md) to learn the step-by-step process to configure integration between two systems.

<div align="center"><img src="../assets/Aras_System_Integration_4.png" alt="" width="1250"></div>

## Criteria Configuration 

* If the user wants to specify conditions for synchronizing an entity between Aras Innovator and the other system to be integrated, he/she can use the **Criteria Configuration** feature.
* To configure criteria in Aras Innovator, integration needs to be created with Aras Innovator as the source system. The user can set a query on a particular ItemType.
* Go to Criteria Configuration section on [Integration Configuration](../integrate/integration-configuration.md) page to learn in detail about Criteria Configuration.
* Aras Innovator Query format is **`[ItemType].<field_internal_name>='<value>'`**

**Criteria samples**

| **Field Type**          | **Criteria Description**                                                  | **Criteria snippet**                                                    |
| ----------------------- | ------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| **Lookup**              | Synchronize all ECR with priority set to 1                                | [ECR].priority = '1'                                                   |
| **Date**                | Synchronize all entities created after certain date                       | [ECR].created_on > '2020-01-31T00:00:00'                              |
| **Text**                | Synchronize all ECR with Title Demo entity                                | [ECR].title = 'Demo entity'                                            |
| **Text** and **Lookup** | Synchronize all ECR with unit EA and Status new                           | [ECR].unit = 'EA' AND [ECR].status = 'New'                            |
| **Lookup** or **Date**  | Synchronize all ECR with priority set to 1 or Effective Date greater than | [ECR].priority = '1' or [ECR].effective_date > '2020-01-31T00:00:00' |

## Target LookUp Configuration 

* Provide Query in Target Search Query field so that it is possible to search the entity in Aras Innovator when it is the target system.
* Go to **Search in Target Before Sync** section on[Integration Configuration](../integrate/integration-configuration.md) page to learn in detail about how to configure Target LookUp.
* Target LookUp configuration is similar to the [Criteria Configuration](aras.md#criteria-configuration) where in the Target Search Query field, the user can provide a placeholder for the source system’s field value in-between ‘@’.
* Target Look Up Query based on internal id of source itemtype:
  **Example query:** `[ECR].custom_text='@oh_internal_id@'`

# Known Behaviors

**Remote ID Synchronization**

* In Aras, custom entity types don't have Item Number (which stores Display Id) field by default. Hence, in such cases, <code class="expression">space.vars.OIM</code> will use entity's Internal Id as Remote Id to be synchronized to the other end system.
* To show the 'Display Id' as Remote Id, it is required to add the Item Number field in Aras.
  Refer to [Add Item Number Field](aras.md#set-item-number-for-custom-entity) for more details.

**Reference Field Lookup Behavior**
* For reference fields, if the referenced entity uses a field other than the standard name field, configure the correct field in Metadata details (JSON) using PrimaryNameField.

## Version Control in Bidirectional Integrations

* When **OH_Version** is mapped to `false` without any condition, every change synchronized by <code class="expression">space.vars.OIM</code> is written to the current generation of the item. As no new generation is created, the values which the item had before that write are not retained in any generation of the item.
* Hence, in a bidirectional setup, if a user changes the item in Aras Innovator and that change is not yet polled by the integration in which Aras Innovator is the source system, the next write from <code class="expression">space.vars.OIM</code> updates the same generation of the item, and the user's change is not available as a separate generation to be picked up from the version history.
* In such a setup, it is recommended to configure any one of the following:
  * Map **OH_Version** with a condition, so that the item is versioned when it is changed by a user and the current generation is updated only when the last change on the item was written by <code class="expression">space.vars.OIM</code>. Refer to the sample script in [Configure the OH_Version Field in the Mapping](aras.md#configure-the-oh_version-field-in-the-mapping) section.
  * Run the integration, in which Aras Innovator is the source system, in the **Current State** mode. In this mode, <code class="expression">space.vars.OIM</code> compares the current state of the item with the state which it had synchronized earlier, instead of reading the changes from the version history. Hence, the changes made by the users are synchronized even when they are written in the same generation. Refer to [Sync Only Current State](../integrate/integration-configuration.md#sync-only-current-state).


# Known Limitations

* Only English alphabets(A-Z,a-z), numeric digits(0-9) and special characters (Example:- :,<,?,>,],\[,!,@ etc.) are supported for Criteria Configuration.
* Attachment as a field is not supported.
* "No Related" Relationship Type is not supported.
* For Aras Innovator as Target System, if the attachment filename contains Windows special characters (/,,",:,\*,?,<,>), then file will not be added in Aras Innovator. As a result, the user will encounter a processing failure. This is because Aras Innovator does not support Windows special characters in filename.
  Please check [Synchronise file with Windows special characters](../help-center/troubleshooting/errors/aras/oh-aras-1502.md) to find how to synchronise attachment with Windows special characters in filename.
* The **OH_Version** field is not considered for the values which <code class="expression">space.vars.OIM</code> writes back into the Aras Innovator item apart from the synchronized data, i.e. remote id, remote link and sync status. Such writes always create a new generation of the item. Configure these fields at the integration level, only when the additional generations are acceptable.

## Limitations to be Resolved in Upcoming Releases of <code class="expression">space.vars.OIM</code>

* To synchronise File as Attachment to Itemtype being synchronised, there should be unique relationship type between Itemtype and File.
* Comments with attachments are not supported.
* Synchronisation of Inline image in a Formatted text field is only **supported** for **External Files of Image type**.
  Inline image synchronisation in Formatted text fields is **not supported** for **Aras Innovator's Internal Images**.

# Appendix

## Add Users

1. Login to the Aras Innovator with user having Administrator Privileges (by default root/admin user has Administrator Privileges).
2. Navigate to **Administration → Users → Create New User**. Refer to [Check Administration Tab](aras.md#check-administration-tab) to learn where to find Administration tab.
3. Provide necessary details for fields like Login Name, Password, First Name and so on
4. Check the **Logon Enabled** box so that user can login from the UI

<div align="center"><img src="../assets/Aras_User_Add_7.png" alt="" width="1250"></div>

## How to Change the Port of Service

1. Open file explorer and navigate to the service installation folder (Ex: `C:\Program Files\OpsHub\Other_Resources\Resources\OpsHubArasService`).
2. Open the file named `ArasService.exe.config` in any text editor.
3. Search `<baseAddresses>` tag in the file. In `<add baseAddress>` tag, change the `<9494>` with the port on which you want to deploy service. Save the changes. Refer to the image below for reference.

<div align="center"><img src="../assets/Aras_SERVICE_PORT_CHANGE_3.png" alt="" width="1250"></div>

## How to Check Availability for Port 9494 for Aras Service

1. Open the Command Prompt in administrator mode.
2. Type `netstat -ano | findStr "9494"` and press Enter.
3. If the port is being used by any application, it will show the application’s detail. The last column is the PID (process ID).
4. If the port is available, there will be empty output for this command.

## Assign Identity in "Can Add" Tab of Item Type

1. Login to the Aras Innovator with user having administrator privileges.
2. Navigate to **Administration → ItemTypes**. Refer [Check Administration Tab](aras.md#check-administration-tab) to learn where to find Administration tab.
3. Search for the ItemType to which you want to assign an identity.
4. Open the Item Type in the edit mode.
5. Click **Can Add** tab.
6. Click ![](../assets/Aras_add_icon1.png).
7. Select the identity of the user from the pop-up.

<div align="center"><img src="../assets/Aras_Select_identity_5.png" alt="" width="1250"></div>

## Assign Life Cycle State Transition Permissions for Item Type

1. Login to the Aras Innovator with user having administrator privileges.
2. Navigate to **Administration → ItemTypes**. Refer [Check Administration Tab](aras.md#check-administration-tab) for more details.
3. Search for the ItemType for which the user wants to give permission to user identity.
4. Open the Item Type in the edit mode.
5. Click **Life Cycles** tab.
6. Open the Life Cycle you want to edit.

<div align="center"><img src="../assets/Aras_LifeCycle_State_Transition_2.png" alt="" width="950"></div>

7. Click on the arrow of transition state you want to edit.

<div align="center"><img src="../assets/Aras_LifeCycle_State_Transition_1.png" alt="" width="950"></div>

8. Change the role to **Administrators** so that the Integration user is allowed to update the state.
9. Save the changes made in Life Cycle Transition.

## Give Necessary Permissions to User for Itemtype

1. Login to the Aras Innovator with user having Administrator Privileges (by default root/admin user has Administrator Privileges).
2. Navigate to **Administration → ItemTypes**. Refer to[Check Administration Tab](aras.md#check-administration-tab) to learn where to find Administration tab.
3. Search for the ItemType for which the user wants to give permissions to user identity.
4. Open the Item Type in edit mode.
5. Click **Permissions** tab.
6. Click ![](../assets/Aras_add_icon1.png) to select from existing permissions. Refer to [Add Identities to Permissions](aras.md#add-identities-to-permissions) to add new identities.
7. Click ![](../assets/Aras_add_icon.png) to create new permissions.

<div align="center"><img src="../assets/Aras_Permissions_tab_1.png" alt="" width="1250"></div>

### Add Identities to Permissions

1. Double-click the existing permission or click ![](../assets/Aras_add_icon.png) in the Permission tab of Itemtype.
2. Give a name for the permission (for new only).
3. Click ![](../assets/Aras_add_icon1.png).
4. Select the identity of the user from the pop-up.
5. Tick checkboxes for **Get**, **Update**, and **Can Discover** for the user identity.
6. Click **Done** to apply the permissions.

<div align="center"><img src="../assets/Aras_Permissions_1.png" alt="" width="1250"></div>

## Make Item Type Versionable

1. Login to the Aras Innovator with user having Administrator Privileges.
2. Navigate to **Administration → ItemTypes**.
3. Search for the ItemType that you want to make versionable.
4. Open the Item Type in edit mode.
5. Check the **Versionable** checkbox under Versioning.
6. Select **Automatic** in the drop-down list of **Discipline**.

<div align="center"><img src="../assets/Aras_versionable_5.png" alt="" width="1250"></div>

## Create Custom Entity

1. Login to the Aras Innovator with Administrator Privileges.
2. Navigate to **Administration → ItemTypes → Create New Itemtype**.
3. Fill in all mandatory fields and ensure **Versionable** is enabled.
4. Assign TOC View and TOC Access.

<div align="center"><img src="../assets/Aras_Custom_entity_4.png" alt="" width="1250"></div>

> Refer to [Create custom property](aras.md#create-custom-property) to add properties after creating ItemType.

## Set Item Number for Custom Entity

1. Navigate to **Dashboard**.
2. Open **ItemTypes** page.
3. Select the entity type and open in edit mode.
4. Under **Properties** tab, add a row named `item_number` with **Sequence** data type.
5. Set **Keyed Name Order** to `1` and save it.

## Create Custom Property

1. Login to the Aras Innovator with Administrator Privileges.
2. Navigate to **Administration → ItemTypes**.
3. Search for the ItemType where you want to add the property.
4. Open the Item Type in edit mode.
5. Click **Properties** tab.
6. Click ![](../assets/Aras_add_icon.png) icon.
7. Assign Name, Data Type, Data Source and other required fields.

<div align="center"><img src="../assets/Aras_Custom_property_6.png" alt="" width="1250"></div>

## Get Database Name

1. Open Aras Innovator's client login page.
2. The available database name is shown on the page.

<div align="center"><img src="../assets/Aras_DB_Name_1.png" alt="" width="1250"></div>

## Get Aras Innovator Version

1. Open Aras Innovator's client login page.
2. The version of the instance is shown on the page.

<div align="center"><img src="../assets/Aras_Version_Name_1.png" alt="" width="1250"></div>

## Check Administration Tab

1. After login, click the **TOC** button at the top left of the screen.
2. Expand the **Administration** tab to find ItemTypes, Users, Identities, etc.

> Refer to the screenshot below for reference:

<div align="center"><img src="../assets/Aras_Administration_Tab_1.png" alt=""></div>
