{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}   
 
# New Versions
* GitHub Enterprise: 3.18.10
 
# Enhancements
 
## TestRail
 
* Enhanced the TestRail integration to support changes introduced in TestRail.
  * Added support for TestRail fields updated from Markdown to Rich Text, ensuring formatted content continues to synchronize correctly.
 
## Jira Zephyr Scale Cloud
 
* Added support for configurable API base URLs in the Zephyr Scale Cloud plugin for Jira, allowing regional-specific endpoints to be configured and ensuring API tokens work correctly with those endpoints.
* For more details, refer to the [Zephyr Scale Cloud](https://docs.opshub.com/connectors/jirazephyrscale#system-configuration "https://docs.opshub.com/connectors/jirazephyrscale#system-configuration") documentation.
 
# Major Bug Fixes
 
## Common
 
* Improved OIM UI usability by resolving issues with alignment, button visibility, and audit log display.
* Resolved an issue where an integration remained in an **Active** state after being deactivated, resulting in a **"Job is not associated with this integration"** error when the integration was explicitly executed.
 
## MSDynamics
 
* Resolved an issue where status updates were not synchronized to the target system when MS Dynamics was configured as the source and the status was updated immediately after adding a comment.
 
## ReadyOne
 
* For ReadyOne as the source system, resolved an issue where a global failure stating **"Entity type information is missing"** occurred when a reference field pointed to a Poly Item that referenced a Requirement.
 
{% endif %}

{% if "OM4ADO" === visitor.claims.unsigned.product %}
 
* No product-specific updates in this release.
 
{% endif %}