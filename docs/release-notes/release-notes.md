{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}

# New Entities(s)
* Windchill PLM: Part, Engineering Materials, Change Request
 
# Enhancements
## Common
* Auto-map functionality is now available for link types in relationship mapping to quickly map links.

## Aha
* Due to Aha! API limitations, User-type fields are supported for current-state synchronization only. For history synchronization, use the corresponding virtual display-name fields (for example, Owner.Name).
 
# Major Bug Fixes 
## Common
* Resolved an issue where the save button was missing in the "OH Comment" configuration in the mapping.
* Resolved an issue where, when "Sync Confirmation" was enabled, the integration processed updates that did not contain any actual business changes, resulting in repeated updates to the Sync Confirmation field.
* Resolved an issue where administrators could encounter an error while removing the Super Admin role from a user, even when another active user already had Super Admin privileges.
 
## Azure DevOps Server/Services
* Resolved an issue where attachments associated with specific test steps within a Test Result were synced as general Test Result attachments instead of remaining linked to the individual test steps where they were originally added.
* Resolved an issue where synced Test Result's Priority field values were not retained and were reset to None during subsequent updates performed as part of the sync.

## GitHub
* Resolved an issue where synchronization failed when Rule-Based Routing was configured using a GitHub custom lookup field to determine the target system's work item type (Bug or Task). In this case, when OIM updated the routing field in GitHub based on the target system's work item type, synchronization failed with the error: "The single select option Id does not belong to the field".

## Enterprise Architect
* Resolved an issue where synchronization failed with a global error, "Can't find matching ID", while processing an element that contained links to corrupted or invalid diagram object references that could no longer be resolved by the EA repository.

## Aha
* Resolved an issue where status synchronization from Aha! to target systems failed with the error, "Transition of issue to status 6872650242336267354 is not available", due to Aha! API limitations.

## ReadyOne
* Updated ReadyOne documentation to clarify that Item Types must be configured as "Versionable" for updates synchronization. Without this setting, updates made to synchronized entities created by the OpsHub sync user may not be synchronized.
 
{% endif %}  
 
{% if "OM4ADO" === visitor.claims.unsigned.product %}  
 
# Major Bug Fixes
* Resolved an issue where attachments associated with specific test steps within a Test Result were migrated as general Test Result attachments instead of remaining linked to the individual test steps where they were originally added.
* Resolved an issue where migrated Test Result's Priority field values were not retained and were reset to None during subsequent updates performed as part of the migration.
 
{% endif %}