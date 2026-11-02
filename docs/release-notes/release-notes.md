{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}

# New Entities

* IBM Engineering Test Management: Test Suite Execution Record

# Enhancements

## Common

* Added a REST API (`/defaultXSLT`) to fetch default XSLT scripts for field mapping, supporting different field types and configurations, including default values and lookups.
* Resolved an issue where remote links could break for entities that contained spaces or special characters such as &, #, or % (e.g., ADO Variable Group names, Polarion Test Run IDs, Gerrit project paths, and MBSE element/project names).

## IBM Engineering Test Management

* Added the Test Environment field to Test Plan entities and the Test Environment and Iteration fields to Test Case Execution Record entities, enabling access to their details through advanced XSLT.

## ServiceNow

* Enhanced ServiceNow synchronization handling to prevent failures when the ServiceNow load balancer returns repeated HTTP 429 (Too Many Requests) responses.

# Major Bug Fixes

## Common

* Resolved an issue where purging integrations containing entity hierarchy information failed with a Hibernate **TransientObjectException**.
* Resolved an issue where global failures caused by multi-entity polling were visible only at the integration group level and not on the individual integrations.

## MBSE

* Resolved an issue where integration in current state failed to create entities with mandatory reference fields when the referenced entities had not yet been synchronized.
* Resolved an issue where elements that became eligible for synchronization after being moved to a selected package or meeting the integration criteria were not synchronized until a subsequent update.

## qTest

* Added support for qTest relationship mapping for Module-to-Test Case and Test Cycle-to-Test Suite relationships with reverse link options, enabling relationship synchronization from both entity perspectives.

## IBM Engineering Workflow Management

* Resolved an issue in the EWM connector where custom fields with names matching standard OSLC attributes caused incorrect project scope validation, preventing eligible work items from being synchronized.

## Jira

* Enhanced Jira synchronization to reduce memory consumption when processing large volumes of issues updated through bulk operations.

## HPQC

* Resolved an issue where the Release Full Path field was not synchronized during current-state synchronization.

## Codebeamer

* Resolved an issue in the Codebeamer connector where downstream reference links were unavailable for relationship configuration from the referred entity side.
    * Reference documentation: [Configure Downstream Reference Link Metadata](../connectors/codebeamer.md#configure-downstream-reference-link-metadata)

## Aha

* Resolved an issue where revision synchronization failed when multiple custom fields shared the same key but had different data types.

# Documentation

## GitHub

* Updated the GitHub connector documentation to include documentation for Milestone Entity, Custom Fields, and Attachment Synchronization.
    * Reference documentation: [GitHub Documentation](../connectors/github.md)

{% endif %}

{% if "OM4ADO" === visitor.claims.unsigned.product %}

# Major Bug Fixes

* Resolved an issue where Release Pipelines, Test Plans, and Test Suites created or updated by the integration user were excluded from migration, resulting in missing entities.
* Resolved an issue where failed Release Pipeline creation attempts could result in source pipelines being incorrectly linked to unrelated existing pipelines in the target project during recovery.

# Documentation

* Updated the Azure DevOps connector documentation to correct the Service Connection target lookup query placeholder from `@name@` to the case-sensitive `@Name@`.

{% endif %}