{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}
# New Entities
* IBM Engineering Requirements Management DOORS Next: File Artifact Format
* IBM Engineering Test Management: Test Suite Results

# Enhancements
## DoorsNG
* Enhanced DNG comment synchronization to support comments shared across base and module artifacts, with the option to control base artifact comment synchronization using the Skip base artifact comments flag at the integration level.

## IBM Engineering Test Management
* Enhanced the ETM connector to support additional fields and link types:
    * Test Plan: Entry Criteria, Exit Criteria, Development Plan Links, Test Environments, Team Area, and Test Suites.
    * Test Suite: Team Area.
    * Test Case: Formal Review Comments, Post-Condition, Team Area, and Development Items.
    * Test Case Result: Formal Review Comments, Team Area, and Defects.
    * Test Script: Review Comments, Team Area, and Requirement.
    * Test Case Execution Record: Blocking Defects, Team Area, and Previous Result Details.
    * Test Suite Execution Record: Previous Result Details.

# Major Bug Fixes
## IBM Engineering Workflow Management
* Resolved an issue where incomplete iteration path values were retrieved from EWM, causing migration failures.

## IBM Engineering Requirements Management DOORS Next
* Resolved an issue where the Status field was not synchronized for artifacts created before a DNG 7.x upgrade, resulting in empty values in the target system.

## IBM Engineering Test Management
* Resolved an issue where Change Request link types were not visible in Test Suites.

## Jira
* Resolved an issue where, with Xray configured as the target, synchronization of Test Cases containing Call to Test Case steps failed with the following error: `invalid: one of 'action' or 'callTestIssueId' is required!`
* Resolved an issue in Zephyr Scale where updates made to entities created by OIM were skipped during bidirectional synchronization, preventing changes from syncing back to the source project.
* Resolved an issue in Zephyr Scale where inaccessible cross-project linked items caused synchronization to fail with a global failure stating: `linked_entity_type must not be null or empty`
* Resolved an issue in Zephyr Scale where updating a Test Case could clear the existing Component field value, even when the field was not mapped.
* Resolved an issue in the Xray Cloud connector where attachment synchronization failed with a 403 Forbidden error.

## Jama
* Resolved an issue where synchronization of items with populated Reference fields, such as Release, resulted in a global failure with a ClassCastException.

## ServiceNow
* Resolved an issue where updates were not synchronized correctly when multiple users' changes were recorded together, resulting in the following error: `OpsHub-012078: Processing blocked for this event, Event is not constructed with corresponding revision updates for entity`
{% endif %}

{% if "OM4ADO" === visitor.claims.unsigned.product %}
# Major Bug Fixes
* Resolved an issue in the Azure DevOps connector where Test Suite synchronization failed with the following error when the tester or configuration of a test case was updated in the source suite, but the test case was not yet linked to the target suite: `OH-Connector-0052: Item not updated successfully in target entity {Target Entity ID}`
{% endif %}