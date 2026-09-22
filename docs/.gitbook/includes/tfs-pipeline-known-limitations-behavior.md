* Attachments, Comments, and Inline images' synchronization is not supported.
  * Reason: Build Pipeline does not have Attachments, Comments, and Inline images.
* End System Criteria Storage is not supported.
  * Reason: Build Pipeline does not have any custom fields.
* Secure Files and Azure Git Repositories with the same names in the source system must be present in the target system to avoid any sync failures.
* Impersonation is not supported.
* For on-premise deployment, there is a Retention tab in the Build Pipeline entity [not available in cloud deployment]. This Retention tab synchronization is not supported.
* Process parameters are not supported.
* During synchronization, processing of GitHub pipeline will result in a failure when the target system is Azure DevOps Server (TFS). 
  * Reason: Azure DevOps Server (TFS) does not support GitHub pipeline.
* During the Build Pipeline entity synchronization, the processing failure may come while syncing the Service Connection for the below mentioned use case. For more details around the next steps, refer to [this](../../help-center/faqs/tfs/pipelineserviceconnectionfailure.md) section.
  * Use case: Service Connection 1 was associated with some steps of any job in the Pipeline entity. The user changed the Service Connection from Service Connection 1 to Service Connection 2 and deleted the Service Connection 1 from the end system.
* During synchronization, a processing failure may occur if the pipeline contains tasks installed from the marketplace and the task version referenced in the source pipeline is not available on the target system.
  * The versions available for a Marketplace task depend on when the task was installed on each system. For example, if the task was installed earlier on the source system, versions 3 and 4 may be available, whereas a more recent installation on the target system may provide only version 4.
  * If the source pipeline references version 3, synchronization will attempt to create the pipeline on the target system using the same version. Since version 3 is not available on the target system, the pipeline creation request will result in a processing failure.
  * This failure is conditional on the task version referenced by the source pipeline. For example, if the source pipeline references version 4, which is also available on the target system, the pipeline will be created successfully.
  * Resolution : If failure occurs, the user must update the failed event data with correct version of task available on the target system, and retry the failure.

{% if "OM4ADO" === visitor.claims.unsigned.product %}

* Actual revision time and user email are suffixed to the comment of that particular revision.

{% endif %}
