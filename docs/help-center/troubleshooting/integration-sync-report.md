---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# Overview

Integration Sync Report provides the information for each entity synchronized by <code class="expression">space.vars.OIM</code>. The report gives insight into which entity from which project in the source system has synchronized to which project in the target system. The report also shows source entities ids and target entities ids. You can also navigate to the failed event of a particular entity from this report. Each integration has a separate Integration Sync Report.

The Global Sync Report provides a comprehensive view of all synced entities across integrations and folders. It allows users to monitor, filter, and analyze synchronization data in one place. Users can apply filters to narrow down results or reset them to view the complete global dataset. Access to data is restricted based on user permissions

# How to Navigate to the Integration Sync Reports

To view the report for any integration, go to an integration, click the **Show List** button. From the list, click **Last Event ID** or **Last Event Time** button.  
<p align="center">
  <img src="../../assets/Report-Image-1a.png"/>
</p>

<p align="center">
  <img src="../../assets/Report-Image-2a.png"/>
</p>

## Global Sync Report

- Easily view what data has been synchronized across all integrations and folders, based on your access permissions. This gives you a complete picture of your synced records in one place.
- To see data across all integrations, simply clear the filters (including integration selection). By default, when you open the report, it may show data from a specific integration — removing filters will show a broader view
 - You can also select multiple integrations as needed, depending on your use case, to focus on specific data. 
 - Note: The integration filter allows selecting up to 50 integrations at a time to help you analyze data more effectively.
- The report will only display data that you are authorized to access, ensuring proper security and visibility control.
- You can apply filters anytime to focus on specific integrations, folders, or entities based on your needs.
- By default, folder-level filtering is turned off so you can view data across all folders. If you want to focus on a specific folder (like a current or child folder), you can enable the folder filter. For more details on filters refer to [this](#filtering-an-integration-sync-report) section.
- For exporting the sync report, refer to [export functionality](#export-functionality) section.

<p align="center">
  <img src="../../assets/global_sync_report.png" />
</p>

# Reading an Integration Sync Report

The integration sync report is divided into two panes:
1. **In Sync Entities** : Report of the entities which are synchronized under the create/update events  
2. **Deprecated/Deleted Entities** : Report of the entities which are synchronized under the Delete events.

The Integration Sync Report includes:  
- **Integration:** This column shows the integration name of the synced entity.  
- **Source Entity Id:** This column shows the entity id of the source system
- **Source Project Name:** This column shows the name of the project from which entity gets polled by <code class="expression">space.vars.OIM</code>  
- **Source Entity Sync State:** This column shows the [state](#state) of the entity in the source system  
- **Last Updated in Source:** This column shows the last updated time for the given entity in the source system  
- **Target Entity Id:** This column shows the entity id of the target system in which entity gets created by <code class="expression">space.vars.OIM</code>  
- **Target Project Name:** This column shows the project name of the target system in which entity gets created by <code class="expression">space.vars.OIM</code>  
- **Target Entity Sync State:** This column shows the [state](#state) of the entity in the target system  
- **Last Processed Time:** This column show the time when entity was last processed by <code class="expression">space.vars.OIM</code>  
- **No. of Failures:** This column shows the number of failed events for a given entity. By clicking on the number, you will be navigated to failed events for that entity.  

<p align="center">
  <img src="../../assets/Integration_Report_OneIntegration.png"/>
</p>

# Filtering an Integration Sync Report

You can filter data from an Integration Sync Report by using the following parameters:

- **Filter On Folder:** Turn this on to view synced data from the current folder and its child folders. By default, this option is turned off, so you can see data across all folders.
- **Select Integrations:** Choose one or more integrations to see their synced data.
By default, the integration you came from will already be selected. You can add more integrations from different folders based on what you want to analyze. 
- **Source Entity Id:** Search the entity by providing Source Entity Id  
- **Source Project Name:** Search the records with the source project name specified in the field  
- **Target Project Name:** Search the records with the target project as specified in the field  
- **Last Processed Time:** Search the entities with the Last Processed time between the range specified in the **Last Processed Time From** and **Last Processes Time To** fields  
- **Target Entity Id:** Search the entity by providing the Target Entity Id  
- **Source Entity Sync State:** Search the records with the source entity sync [state](#state) specified in the field  
- **Target Entity Sync State:** Search the records with the target entity sync [state](#state) specified in the field

Enter the details in the field that you want to use for filtering the data. Then, click the **Search** button.

<p align="center">
  <img src="../../assets/multiple_integration_report_view.png" />
</p>

- If you turn on the filter on folder, below is the example.

<p align="center">
  <img src="../../assets/Filter_on_folder_report.png" />
</p>


# Export Functionality

- The report can be exported by clicking the Export button, which provides options to download the data in Excel or PDF format.
- The exported file includes all currently displayed data across all pages, based on the selected export format.
Note: 
- When exporting synced data, you can export up to 65,000 records at a time to maintain system performance and avoid delays or failures during export.
- OpsHub Integration Manager allows you to retrieve complete data without any upper limit using its REST APIs, making it ideal for large‑scale data access and advanced processing needs.

<p align="center">
  <img src="../../assets/export_sync_report.png" />
</p>

# Some Key Points to Note

- Project column remains empty for the system that doesn't have the concept of projects. If the system has the concept of projects and the project column is empty, it means the entity has not yet synchronized to the target system.
- When selecting multiple integrations in filter, you can choose up to 50 integrations at a time to help you analyze data more effectively.
- When exporting synced data, you can export up to 65,000 records at a time to maintain system performance and avoid delays or failures during export.
- In case of migration or up-gradation the value of the column **Last Processed Time** for already synced entity is the time at which migration runs and **Project** remains empty.  
- In case of integration, if any entity has failure(s) on **Create event**, then **Last Updated in `<Source>` System, `<Target>` Entity Id and `<Target>` Project** columns remain empty for that record.


# Glossary

## State

- Represents the current synchronization status of the entity for the configured integration in <code class="expression">space.vars.OIM</code>.

- The possible values are as follows:

### 1. General State

1. **Active:** The entity is available and accessible to <code class="expression">space.vars.OIM</code>.

### 2. When *Source Delete Synchronization* Is Enabled

The following states are applicable when deletion or archival changes in the source system are synchronized to the target system for an integration where [Source Delete Synchronization](../../integrate/source-delete-synchronization.md) is configured.

1. **Not Accessible:** The entity is no longer accessible to <code class="expression">space.vars.OIM</code>.

2. **Not Applicable:** The entity is not eligible for synchronization due to its type and/or project change, as no integration configuration matches the updated type and/or project.

3. **Archived:** The entity has been archived in the source system.

4. **Deleted by Sync:** The entity has been logically/soft deleted in the target system by <code class="expression">space.vars.OIM</code> as part of source delete synchronization.

5. **Archived by Sync:** The entity has been archived in the target system by <code class="expression">space.vars.OIM</code> as part of source delete synchronization.

### 3. When *Entity Type and/or Project Change Synchronization* Occurs

The following states are applicable when entity type and/or project changes in the source system are synchronized to the target system. For more details, refer to ["Entity Type" and/or "Project" Change Synchronization](../../integrate/entity-move-synchronization.md).

#### Conversion States

1. **Type Converted:** The entity's type has been changed in either the source or the target system.

2. **Project Converted:** The entity has been moved to a different project in either the source or the target system.

3. **Type and Project Converted:** Both the entity type and the project have been changed.

#### Deprecation States

4. **Deprecated due to Type Conversion:** The entity has been marked as deprecated in the target system because the type of the corresponding source entity was changed in the source system.

5. **Deprecated due to Project Conversion:** The entity has been marked as deprecated in the target system because the project of the corresponding source entity was changed in the source system.

6. **Deprecated due to Type and Project Conversion:** The entity has been marked as deprecated in the target system because both the type and project of the corresponding source entity were changed in the source system.

### 4. Applicable When Batch Writing Is Supported in the Target System

These states are applicable only for integrations with systems for which <code class="expression">space.vars.OIM</code> supports batch writing.

1. **Sync Queued:** The source changes are scheduled in a synchronization queue for batch writing. <code class="expression">space.vars.OIM</code> first collects all changes read by the integrations configured within the same group before applying them to the target system. At this stage, the changes are waiting in the queue and have not yet been written.
2. **Sync Started:** The processing of the queued changes has started. <code class="expression">space.vars.OIM</code> evaluates the queued updates one by one to determine the changes to be applied to the target system. Once all processing is completed, the consolidated updates are written to the target system.

> *Note:* To view queued changes for batch processing, refer to [Viewing Queued Entities for Synchronization](integration-sync-report.md#viewing-queued-entities-for-synchronization).
## Viewing Queued Entities for Synchronization

<code class="expression">space.vars.OIM</code> temporarily stores changes queued for batch writing in its database to ensure consistency and reliable processing.

Entities whose data is in the synchronization queue will have the **Sync Queued** or **Sync Started** state. Otherwise, they will have the **Active** state, which indicates that synchronization has either been completed for that entity or that no pending changes remain in the synchronization queue.

Follow the steps below to view them:
1. Open the **Sync Report** for the integration where the changes are under synchronization.
2. Click on the **"Sync Queued"** or **"Sync Started"** status.

  <p align="center">
    <img src="../../assets/SyncReport.png" width="600" />
   </p>

3. The pop-up lists all changes currently queued for synchronization for the selected entity as follows:
  
  <p align="center">
    <img src="../../assets/SyncQueuedData.PNG" width="600" />
   </p>

4. Click on ![editruleicon](../../assets/editruleicon.png) to view the details of the changes.

  <p align="center">
    <img src="../../assets/AccumulatedEvent.png" width="600" />
   </p>


