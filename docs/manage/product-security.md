---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---
# Product Security

OpsHub is committed to ensuring that <code class="expression">space.vars.OIM</code> is designed, developed, and delivered following industry-standard security practices. Our approach includes secure development practices, application security testing, third-party component monitoring, vulnerability management, and continuous patching of security issues.

Our security practices are aligned with widely accepted standards and frameworks such as OWASP and CWE, and security validation is incorporated throughout the product development lifecycle.
 
---

## Security Update

### Resolved Vulnerabilities

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
            <td>High</td>
            <td>jackson-databind: Duration/XMLGregorianCalendar unbounded number parse. Oversized numbers in JSON strings bound to these types are passed to the JDK parser, letting a small unauthenticated request consume CPU for seconds to minutes. (<a href="https://github.com/advisories/GHSA-q4xh-88c3-wmh7">GHSA-q4xh-88c3-wmh7</a>)</td>
            <td>Not directly impacted as we do not deserialize JSON into these types as the Duration used in the product is java.time.Duration built from configuration values.</td>
            <td>7.238</td>
            <td>7.238</td>
        </tr>
        <tr>
            <td>Third party</td>
            <td>High</td>
            <td>jackson-core: ReDoS in NumberInput.PATTERN_FLOAT via looksLikeValidNumber(). A regex backtracks quadratically on long numeric-looking strings, so a single crafted input can tie up a CPU for over a minute. (<a href="https://github.com/advisories/GHSA-p6pp-m3f8-5c89">GHSA-p6pp-m3f8-5c89</a>)</td>
            <td>Potentially impacted, as Jackson is used for JSON parsing in the product. Fixed by upgrading to jackson-core 2.21.7.</td>
            <td>7.238</td>
            <td>7.238</td>
        </tr>
        <tr>
            <td>Third party</td>
            <td>High</td>
            <td>	jackson-core: UTF8DataInputJsonParser._reportInvalidToken() missing maxErrorTokenLength limit. Malformed tokens read through a DataInput-based parser can build an unbounded error message and cause an OutOfMemoryError. (<a href="https://github.com/advisories/GHSA-7hhh-6rmp-j9qf">GHSA-7hhh-6rmp-j9qf</a>)</td>
            <td>Not directly impacted as we do not parse JSON from a DataInput source.</td>
            <td>7.238</td>
            <td>7.238</td>
        </tr>
        <tr>
            <td>Third party</td>
            <td>High</td>
            <td>jackson-databind: quadratic forward-reference completion. A small JSON document using @JsonIdentityInfo object-ID references can trigger quadratic CPU work. (<a href="https://github.com/advisories/GHSA-cxp5-3px4-pw24">GHSA-cxp5-3px4-pw24</a>)</td>
            <td>Not directly impacted as we do not use @JsonIdentityInfo anywhere in the product.</td>
            <td>7.238</td>
            <td>7.238</td>
        </tr>
        <tr>
            <td>Third party</td>
            <td>High</td>
            <td>jackson-databind retains every unknown raw type ID. With polymorphic types and a defaultImpl fallback, each unique unknown type ID is cached forever, so memory grows until the service fails. (<a href="https://github.com/advisories/GHSA-wv8q-qhhj-9h54">GHSA-wv8q-qhhj-9h54</a>)</td>
            <td>Not directly impacted as we do not use @JsonTypeInfo anywhere in the product.</td>
            <td>7.238</td>
            <td>7.238</td>
        </tr>
        <tr>
            <td>Third party</td>
            <td>High</td>
            <td>Hibernate vulnerable to SQL Injection. Non-alphanumeric characters in stored ID values are later run as SQL, letting a low-privileged attacker read, alter or delete database data. (<a href="https://github.com/advisories/GHSA-2p5w-cvg5-gc5c">GHSA-2p5w-cvg5-gc5c</a>)</td>
            <td>Potentially impacted, as Hibernate is used in the product's persistence layer for database connections and data access. </td>
            <td>7.223</td>
            <td>7.238</td>
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
            <td>Oct 2026</td>
        </tr>
        <tr>
            <td>Third party</td>
            <td>Critical</td>
            <td>Spring Framework Server Sent Event stream corruption while rendering fragments (<a href="https://github.com/advisories/GHSA-j9f9-w8pj-32f8">GHSA-j9f9-w8pj-32f8</a>)</td>
            <td>Not directly impacted as we do not use the affected classes in our product.</td>
            <td>7.238</td>
            <td>Oct 2026</td>
        </tr>
        <tr>
            <td>Third party</td>
            <td>High</td>
            <td>jsoup XmlTreeBuilder vulnerable to memory exhaustion through deeply nested namespace declarations (<a href="https://github.com/advisories/GHSA-65r4-943x-97jj">GHSA-65r4-943x-97jj</a>)</td>
            <td>Not directly impacted as usage is limited to XML generated automatically by the product. User-provided XML is not parsed by this library.</td>
            <td>7.238</td>
            <td>Oct 2026</td>
        </tr>
    </tbody>
</table>
---

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