{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}

# New Entities

* **IBM Rational DOORS:** Module

# Enhancements

## MBSE

* Improved MBSE service stability and troubleshooting with enhanced logging and log rotation, making issues easier to identify and helping manage server log size.

## Codebeamer

* Added the **OH Folder Path** field for Codebeamer, allowing users to select the target folder where entities are created or updated.

# Major Bug Fixes

## Common

* Fixed an export failure where sync reports containing more than 2,100 records could not be exported to a file.

* Fixed an issue where OIM automatically started an upgrade to the same version after restarting the Docker container.

## Jira (Jira Service Management)

* Resolved an issue where the mapping failed to load when Asset field values in Jira Service Management contained large datasets.

## Azure DevOps Server/Services

* Resolved a global failure where build synchronization could stop with a **"Git commit does not exist"** error when the commit associated with a build could not be found.

## Subversion

* Resolved an issue where integrations could not be created when Subversion Commit Information was mapped due to a NullPointerException.

## MBSE

* Resolved an issue that could cause a global failure when processing a large number of changed entities.

{% endif %}

{% if "OM4ADO" === visitor.claims.unsigned.product %}

# Major Bug Fixes
* Resolved an issue where **Mentions (User and Entity)** were migrated in plain text form only when field mappings were updated through the API.

{% endif %}