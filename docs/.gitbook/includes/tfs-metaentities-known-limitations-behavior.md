* Impersonation is not supported.
* Synchronization of Meta Entities for Team Foundation Server 2010 or lower is not supported.
* <code class="expression">visitor.claims.unsigned.product</code> will not sync the following two permissions at collection level for Group and Users due to lack of API:
  * Delete team project
  * Delete team project collection
    However, the first permissions for a group or a user will be set at the project level.
* **Groups with reserved names**: Synchronization of the groups with reserved name is only possible if they are present in the target system. If such groups are not present in the target system, processing failures will be observed in <code class="expression">space.vars.OIM</code>.
  * Reason: Groups cannot be created with reserved names, i.e., Group name 'Endpoint Creators' is reserved by the end system. While trying to create this group, a failure error message will be generated, 'Cannot complete the operation because the group name 'Endpoint Creators' is reserved by the system.'
  * You need to manually delete this failure and start the synchronization again.
* **Groups with reserved scopes**: When Team Foundation Server is configured as source system, groups with a reserved scope, such as **Team Foundation**, can be synchronized only if the required group with same scope already exists in the target system. If it does not exist, processing failures will be observed in <code class="expression">space.vars.OIM</code>.
  * Reason: Due to an API limitation, the end system does not allow to create groups with reserved scope. For example, if Team Foundation Service Accounts is not available in the target system, the synchronization may fail with the error: "Cannot find this active directory group: 'Team Foundation Service Accounts' in target. Add this group in target system."
  * You need to manually add this group in target system to resolve the failure.
* If integration user is not a member of Project Collection Administrators group, collection level permissions will not be synchronized.
* Following are the limitations of <code class="expression">visitor.claims.unsigned.product</code>, if you are syncing Area or Iteration:
  * Target Lookup Query is supported for only one field i.e. Path and the query must be Path=@Path@ for Team Foundation Server to Team Foundation Server integration.
  * Recovery functionality is effective only when Manual Conflict Detection is put off for field Path. It could be set to 'disable conflict detection' or enabled with either 'Source Wins' or 'Target Wins'.
  * Restart Team Foundation Server and OpsHubTFSService.
