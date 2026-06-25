{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}

# New Entities
## Jama
* Bidirectionally sync the Releases entity

## SolarWinds Service Desk
* Bidirectionally sync the Task entity
 
# Enhancements
## Common
* Added support for API token-based authentication for OIM MCP Server and OIM Admin APIs  
* Introduced a global sync report with a consolidated view across all integrations 
	* Added OIM Admin API support to retrieve sync report data for offline analysis and reporting  

## Azure DevOps Server/Services
* Added support to sync process parameters for Build Pipelines  

# Major Bug Fixes
## Common
* Resolved an issue where field mapping could not be saved when mapping reference fields with more than 100 values
* Resolved an issue where the entity internal ID was displayed in the Remote ID/Link reconciliation.

## Jira
* Resolved an issue where inline attachments were not synchronized when rich text fields or comment were overridden using Jeditor.
* Resolved an edge case where work items could be linked to the wrong Jira issue during synchronization  
  * In rare cases, when Jira delayed making newly created issues available in API.

{% endif %}  

{% if "OM4ADO" === visitor.claims.unsigned.product %}  

# Major Bug Fixes

* Resolved an issue where Epics failed during migration when their Id matched a Release Pipeline ID in the same project  
* Resolved an issue where Release Pipeline creation failed when projects were remapped, as it was linked to the wrong Build Pipeline. 
* Resolved an issue where Build Pipeline creation failed when linked to a repository from another project  

# Enhancements
* Added support to sync process parameters for Build Pipelines  

{% endif %}