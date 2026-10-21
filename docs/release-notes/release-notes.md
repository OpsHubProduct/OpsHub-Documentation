{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}

# Critical Updates & Actions Required

MySQL versions earlier than 8.0 (e.g., 5.6 and 5.7) and Oracle versions earlier than 19c (e.g., 11g and 12c) are no longer supported by OIM, as they have reached end of life (EOL).

**Actions:**
* Upgrade MySQL to version 8.0 or later, or Oracle to version 19c.
* Take a full backup of the OIM database and verify that it can be restored before upgrading.
* Please refer to [Pre-Migration Checklist](../manage/upgrade/pre-migration-checklist.md#migrating-s-version-to-7.238-or-above) for more details.

# New Versions

* Jira Zephyr Scale: 15.6.0

# New Entities

* DoorsNG: Module Artifact Format

# Enhancements

## Common

* Added support for downloading usage reports for a configurable period of 1-12 months.
    * Added an optional **months** parameter to the UI, Admin API, and MCP tool to specify the reporting period.
    * By default, the report includes data for the last 6 months and the last 12 months.
    * Reference documentation: [Usage Reports](../manage/advanced-utilities/usage-reports.md)

## Codebeamer

* Added OAuth 2.0 (Client Credentials) authentication support using Microsoft Entra.

## Zendesk

* Added automatic OAuth token renewal for Confidential OAuth client authentication, eliminating the need for manual token renewal.
    * Reference documentation: [Creating Confidential OAuth Client and Generating Client ID and Client Secret](../connectors/zendesk.md#creating-confidential-oauth-client-and-generating-client-id-and-client-secret)

## MBSE

* Improved MBSE synchronization when a very large number of elements (for example, over 100,000) have changed between two revisions.
* Added support for MBSE remote links for model elements and projects, enabling synchronized links to open the corresponding element or project in the MBSE desktop client.

## qTest

* Aligned qTest integration behavior with qTest Cloud by removing inline image support in Rich Text fields. Images are synchronized as attachments using the supported qTest functionality.

# Major Bug Fixes

## Common

* Resolved a global failure that occurred after an OIM upgrade to versions 7.235, 7.236, and 7.237 on MS SQL Server that prevented users from viewing synchronization failures.
* Resolved an issue where MBSE connectors could not be configured, or failed if already configured, under restricted systems licenses that included the SDK add-on.
* Resolved an issue where integration dump export failed when an end system configured in the integration was inaccessible.
* Resolved an issue where entities from ServiceNow, CASDM, Aras, Remedy, and Zendesk were synchronized to the first configured target project at the integration level instead of the correctly mapped project in integrations with multiple project mappings.

## Aha

* Resolved a NullPointerException in Aha! integrations that occurred when a user entered incorrect metadata in the Aha system configuration, such as a value that does not exist in Aha or blank spaces.

## Doors

* Resolved an issue where synchronization failed with a **NoSuchMethodError** due to outdated JAR files remaining in OIM after an upgrade to version 7.212 or later.

## Documentation

* Enhanced Product Security documentation to improve vulnerability visibility across releases by listing open and resolved vulnerabilities with their severity, impacted area, reported release, and expected or actual fix release.
* Updated the Azure DevOps connector documentation to mention that only revisions made within the work item's current project or entity scope are synchronized to the target.

{% endif %}

{% if "OM4ADO" === visitor.claims.unsigned.product %}

# Major Bug Fixes

* Resolved an issue where migrated comment timestamps differed from the source timestamps by one second due to inconsistent comment author resolution.
* Resolved an issue where comments generated during cloning of test plans after migration to target displayed Microsoft.VisualStudio.Services.TFS as author instead of the initiating user's name as the author after migration.
* Resolved an issue where Release Pipeline Overview widgets migrated from TFS to Azure DevOps retained source pipeline IDs instead of being associated with the corresponding target release pipelines.
* Resolved issues in query migration where Parent IDs were not converted to target work item IDs and team references in Iteration Path and Area Path conditions were not mapped to the corresponding target teams.

{% endif %}