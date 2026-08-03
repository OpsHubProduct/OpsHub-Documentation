{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}
# New Entities
* Azure DevOps Server/Services: Delivery Plan
* Zephyr Enterprise: Phase
 
# Enhancements
## Azure DevOps Server/Services
* Added support for Defect-to-Test Result relationship synchronization.
 
## ReadyOne
* Enhanced ReadyOne Poly Item reference synchronization to prevent failures when the referenced entity has not yet been synchronized.
 
## Tricentis Tosca
* Added support for Tosca workspaces using the Tricentis Server repository type, in addition to SQL Server repositories.
* Enhanced Personal Access Token (PAT) authentication by adding an authentication user input to the Tosca system configuration.
 
# Major Bug Fixes
## Common
* Resolved an issue where the Metrics & Trends dashboard displayed the following error for a newly created integration that had not yet been executed: `OH-API-0002: java.lang.NullPointerException: Cannot invoke "java.util.Date.getTime()" because "lastRefreshedDate" is null`
* Resolved an issue where Metrics & Trends dashboard refresh operations failed in PostgreSQL-based OIM deployments with the following error: `ERROR: column "last_refreshed_at" does not exist`
* Resolved an issue where renewed SSL certificates for cloud-based systems were not automatically installed after editing and saving the system configuration.
 
## Jira
* Resolved an issue where inline images embedded in Jira rich text fields were not rendered correctly in HTML rich text fields in the target system.
* Resolved an issue where Jira Service Management Request Type values were not synchronized when multiple Jira fields shared the same schema identifier. This caused OIM to retrieve values from an incorrect field during synchronization.
* Resolved an issue where issue statuses were not updated correctly during failure retry processing after a previously unavailable Jira workflow transition became available.
 
# Documentation
## Jira Service Management
* Updated the Jira connector documentation to include the additional permissions required when configuring Jira Service Management as a source or target system.
{% endif %}
 
{% if "OM4ADO" === visitor.claims.unsigned.product %}
# Major Bug Fixes
* Resolved an issue where Area Path migration failed with the following error when the target Azure DevOps project name contained parentheses: `VS402485: The Area/Iteration name is not recognized: Demo Project (ID)`
* Resolved an issue where HTML fields in Azure DevOps Server 2020 and later versions were incorrectly processed as text fields during migration.
{% endif %}