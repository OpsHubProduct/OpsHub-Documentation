{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}

# Enhancements
## Codebeamer / Codebeamer X
* Enhanced reference field synchronization support to provide more comprehensive synchronization capabilities. Please refer to the [post-upgrade](../manage/upgrade/post-migration-checklist#migrating-version-to-7.229-or-above) steps for  required actions when Codebeamer is one of the integration endpoints and advanced logic is configured on reference field mappings.

## GitHub
* Added support for GitHub App. Refer to [this](../connectors/github.md#github-app-installation) section for more details.

## Jira Service Management [Jira Plugin]
* Added bidirectional synchronization support for the Requestor Type field.

# Major Bug Fixes
## Common
* Resolved an issue where SAML-based logins to OIM failed when user attributes received from the identity provider (IdP) were  missing, resulting in a "500 internal server" error and preventing user access.

## Aras Innovator
* Resolved an issue where link synchronization failed when Aras item types did not contain the `item_number` field or when multiple items shared the same Part Number value.

## Azure DevOps Server/Services
* Resolved an issue where Test Run synchronization failed with a global failure error message  "NullPointerException" when processing Test Results containing missing Configuration information.
* Resolved an issue where Test Result's "Duration" field value was synchronized with incorrect execution times, resulting in higher duration values in the target system.
* Resolved an issue where Test Result's "Completed Date" field value was not synchronized to the target system.

## IBM Engineering Test Management
* Resolved an issue where Test Case synchronization failed with a "Requested object not found due to 404 Not Found" error in IBM HTTP Server-fronted ETM deployments.

## Jira Align
* Resolved an issue where synchronization of Feature entity failed with a global failure where integrations configured with Jira align's Portfolio projects.

## Monday.com
* Resolved an issue where duplicate groups with the same name created in Monday.com when synchronizing multiple child entities belonging to the same parent. Items are now correctly associated with the existing target group.

{% endif %}

{% if "OM4ADO" === visitor.claims.unsigned.product %}

# Major Bug Fixes
* Resolved an issue where Test Run migration failed with a "NullPointerException" error when processing Test Results containing missing configuration information.
* Resolved an issue where Test Result's "Duration" field value was migrated with incorrect execution times, resulting in higher duration values in the target system.
* Resolved an issue where Test Result's "Completed Date" was not migrated to the target system.
* Resolved an issue where Test Run migration failed with a "NullPointerException" error when processing Test Results that did not contain associated Test Suite information.

{% endif %}