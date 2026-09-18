{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}

# Enhancements

## Common

* Improved the performance of the failure analysis view when handling a large number of failures.

## ReadyOne

* Added support to integrate with ReadyOne without service dependencies and with OAuth authentication.
    * Post-upgrade steps: [Migrating Version to 7.235 or Above](../manage/upgrade/post-migration-checklist.md#migrating-version-to-7.235-or-above)
* Enhanced ReadyOne reference field support to load lookup values, display reference names, unset references, and support references to the same entity type.

## HPQC

* Added support to preserve the rank/order of HPQC Requirements during synchronization.

# Major Bug Fixes

## Aha

* Fixed an issue where Aha To-Do display IDs were displayed instead of their display IDs in sync reports and the Remote ID field.
* Resolved an issue where Aha Goal parent-child ("Contains goals" / "Belongs to goal") relationships were not available for relationship mapping in OIM.

## Azure DevOps Server/Services

* Resolved an issue where synchronization failed with an **"Access is denied due to invalid credentials"** error when work item's rich text field contained attachments referenced from Azure DevOps Pull Requests.

## HPQC

* Resolved an issue where HPQC comments were duplicated during backdated synchronization and updates to existing comments were not synchronized correctly.

## ReadyOne

* Resolved an issue where ReadyOne synchronization failed when an entity was created or updated by a user with a blank or invalid email address.
* Resolved an issue where ReadyOne reference field synchronization failed when the referenced entity had been updated after synchronization.

{% endif %}

{% if "OM4ADO" === visitor.claims.unsigned.product %}

# Major Bug Fixes

* Resolved an issue where Test Case step-level attachments were not synchronized when attachments were added to existing steps without modifying the step content or when a step with an attachment was deleted.

{% endif %}