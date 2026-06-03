{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}   

# New Version(s)
* Angular: 16.x

# New Entities(s)
* Windchill PLM: Subtypes for Problem reports

# Enhancements

## Common
* Improved Transitions & Dependencies to ensure dependent field validations are enforced during item updates.

## GitHub
* Enhanced the Pull Request entity synchronization process.

# Major Bug Fixes

## Common
* Resolved an issue where upgrading <code class="expression">space.vars.OIM</code> to 7.225 failed on PostgreSQL databases when only an administrator account with full permissions was configured.
* Resolved a performance issue that caused mapping configurations with more than 60 mapped fields to load slower than expected.
* Resolved an issue where APIRequestLocker generated the error: "java.lang.IllegalArgumentException: Start value must be smaller or equal to end value".

## Aha
* When Aha is configured as the source: 
  * Resolved an issue where user mentions were not correctly identified for deleted Aha users.
  * Resolved an issue where history records for the same field were automatically grouped when updates occurred within a five-minute interval.
  * Resolved a Null Pointer Exception that occurred when retrieving projects without receiving a successful response from Aha.

## Azure DevOps Server/Services
* Resolved an issue where Owner details were not synchronized correctly in Release Pipeline entities.
* Resolved an issue where Start Date and Finish Date values were not updated correctly for Test Plan entities.

## Broadcom Rally Software
* Resolved an issue where a recovery failure triggered duplicate milestone creation requests.

{% endif %}  

{% if "OM4ADO" === visitor.claims.unsigned.product %}  

# Major Bug Fixes
* Resolved an issue where Owner details were not migrated correctly in Release Pipeline entities.
* Resolved an issue where Start Date and Finish Date values were not migrated correctly for Test Plan entities.

{% endif %}