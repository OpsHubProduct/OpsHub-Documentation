---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---
# Product Security

OpsHub is committed to ensuring that <code class="expression">space.vars.OIM</code> is designed, developed, and delivered following industry-standard security practices. Our approach includes secure development practices, application security testing, third-party component monitoring, vulnerability management, and continuous patching of security issues.

Our security practices are aligned with widely accepted standards and frameworks such as OWASP and CWE, and security validation is incorporated throughout the product development lifecycle.

---

## Security Update

#### Resolved Vulnerabilities
 
<table>
    <thead>
        <tr>
            <th width="100">Category</th>
            <th width="60">Severity</th>
            <th>Summary</th>
            <th width="150">Impacted Area</th>
            <th width="90">Reported In Release</th>
            <th width="90">Fixed In Release</th>
        </tr>
    </thead>
    <tbody>
 <tr>
            <td>Third party</td>
            <td>Critical</td>
            <td>Apache Tomcat: Authentication Bypass by Alternate Name in Apache Tomcat for WebSocket based endpoints. (<a href="https://github.com/advisories/GHSA-pc63-qcmh-9cmg">GHSA-pc63-qcmh-9cmg</a>)</td>
            <td>Not directly impacted as we do not expose template-mapped WebSocket endpoints.</td>
            <td>7.241</td>
            <td>7.241</td>
        </tr>
        <tr>
            <td>Third party</td>
            <td>High</td>
            <td>jsoup XmlTreeBuilder vulnerable to memory exhaustion through deeply nested namespace declarations (<a href="https://github.com/advisories/GHSA-65r4-943x-97jj">GHSA-65r4-943x-97jj</a>)</td>
            <td>Not directly impacted as usage is limited to XML generated automatically by the product. User-provided XML is not parsed by this library.</td>
            <td>7.238</td>
            <td>7.241</td>
        </tr>
        <tr>
            <td>Third party</td>
            <td>High</td>
            <td>Google Guava: CompactHashMap/CompactHashSet/MapMakerInternalMap deserialization triggers uncontrolled memory allocation. (<a href="https://github.com/advisories/GHSA-xxph-c9ww-hj94">GHSA-xxph-c9ww-hj94</a>)</td>
            <td>Not directly impacted as we do not use the affected classes and methods.</td>
            <td>7.238</td>
            <td>7.241</td>
        </tr>
        <tr>
            <td>Application</td>
            <td>High</td>
            <td>External Control of File Name or Path allowing access to unauthorized server files through manipulated file paths.</td>
            <td>File Upload</td>
            <td>7.234</td>
            <td>7.241</td>
        </tr>
        <tr>
            <td>Application</td>
            <td>High</td>
            <td>ORM Query Injection through legacy JSON-RPC endpoints using user-controlled query input.</td>
            <td>Legacy JSON-RPC API</td>
            <td>7.234</td>
            <td>7.241</td>
        </tr>
        <tr>
            <td>Application</td>
            <td>High</td>
            <td>Insecure Deserialization could cause excessive memory consumption and potential denial-of-service conditions.</td>
            <td>Import Mapping</td>
            <td>7.234</td>
            <td>7.241</td>
        </tr>
        <tr>
            <td>Application</td>
            <td>High</td>
            <td>Code Injection risk through workflow upload capable of executing unauthorized code in the application context.</td>
            <td>Workflow Upload/Update</td>
            <td>7.234</td>
            <td>7.241</td>
        </tr>
        <tr>
            <td>Third party</td>
            <td>High</td>
            <td>OpenJDK HotSpot heap buffer overflow in the AVX-512 Base64 decoder ("Java4Shell") that may allow remote code execution, disclosure of JVM memory, or denial of service (<a href="https://nvd.nist.gov/vuln/detail/CVE-2026-114938">CVE-2026-114938</a>)</td>
            <td>Bundled JRE. Affects only x86_64 servers with AVX-512 capable CPUs.</td>
            <td>7.240</td>
            <td>7.241</td>
        </tr>
    </tbody>
</table>

 
### Open Vulnerabilities
 
<table>
    <thead>
        <tr>
            <th width="100">Category</th>
            <th width="60">Severity</th>
            <th>Summary</th>
            <th width="250">Impacted Area</th>
            <th width="90">Reported In Release</th>
            <th width="80">ETA</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Third party</td>
            <td>Critical</td>
            <td>Spring Framework Improper Path Limitation in XsltView (<a href="https://github.com/advisories/GHSA-pc63-qcmh-9cmg">GHSA-pc63-qcmh-9cmg</a>)</td>
            <td>Not directly impacted as we do not use XsltView in our product.</td>
            <td>7.238</td>
            <td>Nov 2026</td>
        </tr>
        <tr>
            <td>Third party</td>
            <td>Critical</td>
            <td>Spring Framework Server Sent Event stream corruption while rendering fragments (<a href="https://github.com/advisories/GHSA-j9f9-w8pj-32f8">GHSA-j9f9-w8pj-32f8</a>)</td>
            <td>Not directly impacted as we do not use the affected classes in our product.</td>
            <td>7.238</td>
            <td>Nov 2026</td>
        </tr>
    </tbody>
</table>

## Application Security

OpsHub applies a multi-layered approach to ensure the security of OpsHub Integration Manager.

- Application vulnerability testing is conducted for every release using an industry-leading web application security testing provider.
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
 
---

## Security Issue Patching Policy

OpsHub continuously monitors publicly disclosed vulnerabilities related to core platform components used by the product.

- Security advisories related to Apache Tomcat and Java are actively monitored and patches are applied when required.
- If a severe security issue is reported by a customer or discovered internally by OpsHub, it is patched as soon as reasonably feasible.