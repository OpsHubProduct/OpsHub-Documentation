{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}

# Enhancements
## Jama
* Added support for synchronization of locked items in Jama.
  * Users can now configure OpsHub Integration Manager to automatically unlock items, perform updates, and re-lock them - eliminating failures and manual intervention.

  > **Note**: If an item is locked by another OpsHub integration user, only a Jama user with similar permissions or a super admin can unlock it, due to Jama’s permission model. Refer to the OpsHub documentation for [Jama connector](../connectors/jama.md#lock-handling-configuration) for more details.

* Added support for "No Storage" criteria type. Users can now define criteria in OIM to control sync in below way:
  * When an entity meets the criteria - it is synchronized
  * When it goes out of scope - synchronization automatically stops

## Monday.com
* Improved synchronization performance for Monday.com integrations:
  * **31% improvement** when used as source
  * **14% improvement** when used as target

## Azure DevOps Server/Services
* Added support for synchronization of **process parameters** for Release Pipeline entities.

## Aha
* Added support for **soft delete synchronization**. When the source entity is deleted, the corresponding entity in Aha (as target) can now be deleted in addition to logical delete [marking any field with deleted].

# Major Bug Fixes
## Common
* Fixed an issue where advanced configurations were not applied correctly across multiple paths in rule-based routing scenarios.
  * **Use Case:**  Rule-based routing is used to connect one source entity to multiple target entities (for example, Jama Requirement → Jira Epic, Story, Task). Advanced workflow configurations were applied from Jira to Jama system flow.
  * This issue is now resolved. Advanced configurations are applied consistently across all routed entity mappings.

# Documentation
* Enhanced documentation for the **Manage License** page:
  * Clarified behavior when multiple active licenses are present
  * Documented that OIM considers the **latest license features** to ensure consistency and avoid confusion.

{% endif %}    
{% if "OM4ADO" === visitor.claims.unsigned.product %}

# Major Bug Fixes
* Resolved an issue where service principal–based service connections were migrated as Managed Identity, causing authentication failures in Release Pipelines migration.
* Added support for migration of **process parameters** for Release Pipeline entities.

{% endif %}