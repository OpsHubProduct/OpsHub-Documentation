{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}

# New Versions

* EWM: 7.0.3

# New Entities

* MBSE: Project
* Polarion: Plan and Test Run

# Enhancements

## GitHub

* Added support for GitHub Pull Request state history, enabling synchronization of state changes with their corresponding timestamps and user information.

## Aras Innovator

* Added configurable versioning control for Aras synchronization through the new **OH_Version** mapping field.
    * This field allows users to skip creating new versions and update the current version based on custom mapping conditions.
    * Reference documentation: [OH_Version](../connectors/aras.md#version-control-of-aras-innovator-items-oh_version)

## IBM Engineering Requirements Management DOORS Next

* Added support to synchronize the hierarchy and ordering of artifacts in DOORS Next Modules, enabling the structure and artifact order to be preserved in the target system.

## MBSE

* Improved MBSE tag and link synchronization performance by approximately 91% by reducing redundant API calls.

# Major Bug Fixes

## IBM Engineering Test Management

* Improved synchronization performance when entities contain multiple lookup fields.

## Jira

* Resolved a global failure where synchronization failed with an **ArrayIndexOutOfBoundsException** when Jira history contained sprint names with commas.

## qTest

* Resolved a processing failure stating **"Module does not exist"**, where synchronization to qTest as a target system failed while updating the qTest Module hierarchy when a source Folder containing Requirements was moved to a different parent Folder.

# Documentation

## IBM Rational ClearQuest

* Added documentation for the ClearQuest API character limit on multi-line text fields.
    * Reference: [ClearQuest Documentation](../connectors/ibm-rational-clearquest.md#api-response-length-setting-for-multiline-text-fields)

{% endif %}

{% if "OM4ADO" === visitor.claims.unsigned.product %}

# Major Bug Fixes

* Resolved an issue where changes to numeric-looking values in plain text fields, such as 1 to 01, 1.0, or values with leading spaces, were not synchronized correctly.

{% endif %}