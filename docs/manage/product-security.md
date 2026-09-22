---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---
# Product Security

OpsHub is committed to ensuring that <code class="expression">space.vars.OIM</code> is designed, developed, and delivered following industry-standard security practices. Our approach includes secure development practices, Application security testing, third-party component monitoring, vulnerability management, and continuous patching of security issues.

Our security practices are aligned with widely accepted standards and frameworks such as OWASP and CWE, and security validation is incorporated throughout the product development lifecycle.
 
---

## Application security

OpsHub applies a multi-layered approach to ensure the security of OpsHub Integration Manager.

- Application vulnerability testing is conducted for every release using an industry-leading web Application security testing provider.
- Security testing ensures that OpsHub Integration Manager and its deployment environment are protected against external attacks.
- Secure coding practices and validation are implemented in accordance with OWASP guidelines.

Security scans are performed regularly and it is ensured that no high or critical vulnerability exists in the product at the time of release.
 
---

## Code Security Audits

OpsHub conducts a security audit of the entire code base as part of every release.

The audit includes:

- Analysis for high and critical vulnerabilities
- Coverage of OWASP Top 10 vulnerabilities
- Validation against CWE security guidelines

Any high or critical vulnerabilities identified during the audit are resolved prior to release.
 
---

## Third-Party Library Security

OpsHub products include certain third-party libraries bundled with the product. These components do not require additional licenses or installation and are monitored as part of our product security program.
 
---

### Vulnerability Scanning

OpsHub uses **Grype**, a software composition analysis (SCA) tool, to scan builds and container images for vulnerabilities in third-party libraries.

Grype identifies dependencies within software artifacts and compares them against authoritative vulnerability databases to detect known security issues.
 
---

### Remediation Timeframes

Vulnerabilities identified through scanning are remediated according to the following timelines, measured from the date a fix becomes available in the affected third-party library.

| Severity | Remediation Timeframe |
|---|---|
| Critical | 10 business days |
| High | 20 business days |
 
---

## Security Reports and Artifacts

For each release, OpsHub publishes security documentation and artifacts to a shared document repository.

These include:

- Software Bill of Materials (SBOM)
- Security scan reports
- False positive reports with documented explanations

All release-related security artifacts are available here:

[Security Reports Repository](https://opshubtrial-my.sharepoint.com/:f:/g/personal/support_opshub_com/IgD2uaOzmshMT7EV7ULZBVSKAeJvTIW5Qs-hY3pzQlP605U?e=CsAdEx)

Each release has a dedicated folder containing the corresponding reports.

## Release 7.234 Security Update


| Category | Count |
|---|---|
| Vulnerabilities Resolved | 7 |
| Open / In Progress Vulnerabilities | 8 |


### Vulnerabilities Resolved in Release 7.234

| Category | Severity | Summary | Impacted Area | Reported In Release | Fixed In Release |
|---|---|---|---|---|---|
| Third party security | High | Spring Framework Denial of Service via Versioned Resources in Spring MVC and WebFlux ([CVE-2026-41842](https://github.com/advisories/GHSA-x23c-287f-qqv5)) | Not directly impacted | 7.232 | 7.234 |
| Third party security | High | Spring Framework Cross-site Scripting via JavaScriptUtils ([CVE-2026-41845](https://github.com/advisories/GHSA-3chg-m5w7-qfv5)) | Not directly impacted | 7.232 | 7.234 |
| Application security | High | File upload endpoint did not require authentication | Not directly impacted | 7.228 | 7.234 |
| Application security | High | An endpoint that could modify files on the server did not properly enforce authorization | Not directly impacted | 7.228 | 7.234 |
| Application security | High | Certain administrative functions could be accessed without authorization | Not directly impacted | 7.228 | 7.234 |
| Application security | High | Certain database queries did not adequately validate input, which could allow SQL/HQL injection | Not directly impacted | 7.228 | 7.234 |
| Application security | High | Pathway existed that could allow unauthorized commands to run on the server | Not directly impacted | 7.228 | 7.234 |

### Open / In Progress Vulnerabilities

| Category | Severity | Summary | Impacted Area | Reported In Release | ETA |
|---|---|---|---|---|---|
| Third party security | High | Hibernate vulnerable to SQL Injection | Not directly impacted | 7.234 | Sep 2026 |
| Third party security | High | Apache cxf-core: No restriction on attachment headers per message | Not directly impacted | 7.234 | Sep 2026 |
| Third party security | High | Apache HttpComponents Core HTTP/1 header parsing can cause memory-exhaustion denial of service | Not directly impacted | 7.234 | Sep 2026 |
| Third party security | High | Spring Security SAML2 Service Provider: unbounded writer inflates the compressed SAML payload into memory (DoS) | Not directly impacted | 7.234 | Sep 2026 |
| Third party security | High | Spring Security SAML2 Service Provider: RelyingPartyRegistration may run arbitrary code on HTML forms generated by Spring Security filters | Not directly impacted | 7.234 | Sep 2026 |
| Third party security | High | Little CMS (lcms2) through 2.18: integer overflow in CubeSize in cmslut.c | Not directly impacted | 7.234 | Sep 2026 |
| Third party security | High | Vulnerability in Oracle Java SE / Oracle GraalVM for JDK / Oracle GraalVM Enterprise Edition (Libraries component) | Not directly impacted | 7.234 | Sep 2026 |
| Third party security | High | mchange-commons-java susceptible to abuse via JNDI injection and deserialization gadgets | Not directly impacted | 7.234 | Sep 2026 |
 
---

## Security Issue Patching Policy

OpsHub continuously monitors publicly disclosed vulnerabilities related to core platform components used by the product.

- Security advisories related to Apache Tomcat and Java are actively monitored and patches are applied when required.
- If a severe security issue is reported by a customer or discovered internally by OpsHub, it is patched as soon as reasonably feasible.
 
---