{% if "OpsHub Integration Manager" === space.vars.SITENAME %}  

***

# New Connector(s)
* [**Zephyr Enterprise**](../connectors/zephyr-enterprise.md)
  * Supported Version: 8.6.0
  * Supported Entities: Folder, Phase, Test Case, Test Execution

# New Version(s)
* ServiceNow: Australia
* Tricentis Tosca: 2025.1.x

# Enhancements

## Common
* Added support for inline content and attachments in complex fields such as test steps.
* Added documentation for the [API Capability Matrix](../manage/api/api_capability_matrix.md).
  * The document outlines the features and functionalities supported through REST APIs.

## GitHub
* Improved synchronization performance in GitHub by approximately 40%.  

## Jira Data Center
* Added support for providing input in the system form when the Xray plugin is selected and entity names are updated in the end system from the default values.
  * please refer to the post migration checklist in case Xray plugin entity names are updated in the endsystem.

## ReadyOne
* Added support for Reference fields.

## Windchill PLM
* Added support for Library as a container (project) in Windchill PLM.

# Major Bugs

## Common
* Resolved an issue where missing fields in REST APIs for system type templates were not incorporated correctly.
* Resolved an issue where installation of <code class="expression">space.vars.SITENAME</code> failed due to incorrect JAR detection with Windows Authentication on MSSQL Server.
* Resolved an issue where daylight saving time changes impacted integration edit operations.

## Aha
* Resolved an issue where table-type fields merged rows when cells were empty across different rows.

## Azure DevOps Server/Services
* Resolved an issue where synchronization for Azure DevOps Services was impacted due to incorrect API rate limit header values.
* Resolved an issue where a global failure occurred with a Null Pointer Exception for Test Suite entities when inaccessible test cases were present in missing work item fields.
* Resolved an issue where processing failures occurred because of invalid characters generated while looking up release pipelines in the target system.
* Resolved an issue where attachment processing failures occurred when attachments were not found in Azure DevOps Server/Services as the source system.

## GitHub
* Resolved an issue where high RAM utilization warnings were observed on the VM hosting <code class="expression">space.vars.SITENAME</code>.

## Jira Data Center
* Resolved an issue where the system could not be saved when the Xray plugin was enabled for Jira Data Center versions above 9.

## Windchill
* Resolved an issue where <code class="expression">space.vars.SITENAME</code> incorrectly associated linked release entities even when they were synchronized through <code class="expression">space.vars.SITENAME</code>.

{% endif %}  

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}  

# Major Bugs
* Resolved an issue where OpsHub TFS Service crashed during migration of Test Runs after the initial 2–3 hours of execution.
* Resolved an issue where processing failures occurred during release pipeline migration due to invalid release pipeline encoding.
* Resolved an issue where attachment processing failures occurred when attachments were not found in the source system.

{% endif %}