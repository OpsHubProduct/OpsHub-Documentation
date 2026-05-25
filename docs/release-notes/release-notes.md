{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}  

# New Version(s)
* IBM Engineering Requirements Management DOORS Next: 7.1.x
* Java Development Kit (JDK): 17.0.19

# Enhancements

## Common
* Introduced automatic user authentication via SAML without requiring user setup in <code class="expression">space.vars.OIM</code>.

## Aras Innovator
* Added support for Reference fields.

## Azure DevOps Server/Services
* Added support for skipping Automated Test Runs and Results.

## Zendesk
* Added support for Global OAuth as authentication type in Zendesk.

# Major Bug Fixes

## Common
* Resolved an issue where inline attachment URLs were truncated when attachment names contained special characters such as '&'.
* Resolved an issue causing inconsistent link synchronization behavior when the same target link type was configured for both default and non-default links.

## Aha
* Resolved an issue where the first revision was not retrieved from Aha while fetching revisions using advanced methods such as getEntityRevisions.

## Azure DevOps Server/Services
* Resolved an issue causing global failures for the testcase entity when the parameterMap value was found to be undefined.

## Jira Zephyr Essential
* Resolved an issue where TestStep entities were not synchronized to Zephyr Essential as targets. 

## ServiceNow/ServiceNow Quick Connect
* Resolved a Null Pointer Exception that occurred when the username value was null.

{% endif %}  

{% if "OM4ADO" === visitor.claims.unsigned.product %}  

# Major Bug Fixes
* Resolved an issue causing global failures during testcase entity migration when the parameterMap value was found to be undefined.

{% endif %}