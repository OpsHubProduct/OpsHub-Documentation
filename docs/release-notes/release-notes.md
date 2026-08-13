{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}   
 
# Enhancements
## Jira
* Added support for Jira Service Management (JSM) Assets as reference fields, enabling Asset relationships to be synchronized and maintained across integrated systems.
 
## Tosca
* Added support for mapping Parent Folder as a reference field, making it easier to manage parent-child folder relationships using value mappings or default values.
 
## Azure DevOps Server/Services
* Now you can synchronize work items based on attributes of their linked items, enabling more targeted migration and synchronization scenarios.
	* Example: Synchronize only Tasks that are linked to a Bug with Priority = 1
## ServiceNow
* Enhanced support for inline images embedded using ServiceNow image links.
 
# Major Bug Fixes
## Common
* Resolved an issue that could cause high memory utilization during prolonged synchronization operations, resulting in improved application stability and more efficient resource usage.
 
## MBSE
* Resolved an issue that lead synchronization failures when reference fields contained relationships to unsupported or unavailable entity types. Synchronization now continues reliably even when related entity type is missing .
 
# Documentation Updates
## Redmine
* Updated the Product documentation for Redmine system to  specify support for Redmine versions up to 3.4.x and avoid ambiguity regarding newer releases
 
{% endif %}  
{% if "OM4ADO" === visitor.claims.unsigned.product %}  
* Resolved an issue where Shared Steps were not preserved during ADO-to-ADO Test Case migration. Shared Steps now retain their original structure and execution details after synchronization.
{% endif %}