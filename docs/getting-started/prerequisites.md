---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# Deployment Options

* **On Premise**: Can be deployed on local virtual machine or local server
* **On OpsHub Cloud**: Can be deployed on Azure environment provided by OpsHub. This will come at an additional cost, which can be discussed with your point of contact in the support or sales team.
* **On Customer Cloud**: Can be deployed on cloud service hosted by customer. Supported cloud service on which it can be deployed are:
  * Amazon EC2
  * Azure

Following are the Operating System (OS) and hardware pre-requisites for server or VM where <code class="expression">space.vars.OIM</code> is installed.

# Supported Operating Systems

## Windows

* Windows 11 and Windows Server 2016 and above (64 bit)
* For Windows specific configuration, refer [Windows specific configuration](prerequisites.md#windows-specific-configuration)

## Linux

* RHEL 5.2 and above (64 bit)
  * RHEL includes Cent OS and Fedora
* Ubuntu 22.04 and above

# Hardware Prerequisites

1. RAM - 8 GB & above
2. Disk space - 50 GB (Recommended)
3. Database Disk Space - 15 GB (Recommended)
4. Cores - Quadcore (Recommended)

# Database Prerequisites

<code class="expression">space.vars.OIM</code> can be deployed with an embedded database; however, for production deployment or anything other than functional testing, our experts highly recommend using an external database. <code class="expression">space.vars.OIM</code> supports the following database.
Note: If the database is hosted on a separate Windows machine, the operating system must be Windows 11 or Windows Server 2016 and later.

## 1. MySQL Server

{% include "../.gitbook/includes/mysql-preq.md" %}

## 2. MS SQL/Azure SQL Server

{% include "../.gitbook/includes/mssql-preq.md" %}

## 3. Oracle

{% include "../.gitbook/includes/oracle-preq.md" %}

## 4. PostgreSQL Server

{% include "../.gitbook/includes/posgres-preq.md" %}

> **Note**: If default connection timeout parameter is changed for any database server, then it must be confirmed that sufficient connection timeout has been set. For example, for MySQL the default server-side connection timeout is 8 hours. If it is changed and set to, say, 5 minutes, then the default server-side connection timeout must be updated accordingly. **<code class="expression">space.vars.OIM</code>** maintains connection pools that keep connections alive for 8 hours. Based on the need, this parameter can be tuned at both the application and database-server levels.**Generally, the recommended timeout is between 6-8 hours.**

# Download Database Connector jar

| Database Type  | Database Version | Download Link                                                                                                               |
| -------------- | ---------------- | --------------------------------------------------------------------------------------------------------------------------- |
| **MySQL**      | All              | [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j)                                                            |
|  **MSSQL**     | 2012 and lower   | [Download Link](https://www.microsoft.com/en-in/download/details.aspx?id=11774)                                             |
|  | 2014 onward      | [Release Notes](https://learn.microsoft.com/en-us/sql/connect/jdbc/release-notes-for-the-jdbc-driver?view=sql-server-ver16) |
| **Oracle**     | 19c              | [Oracle JDBC 19c](https://www.oracle.com/database/technologies/appdev/jdbc-ucp-19c-downloads.html)                         |
| **PostgreSQL** | All              | [PostgreSQL JDBC](https://jdbc.postgresql.org/download/)                                                                    |

# HostName for <code class="expression">space.vars.OIM</code>

* If machine/instance where <code class="expression">space.vars.OIM</code> deployed is binded with any hostname (Net, Host, Gateway, or Domain name) then please make sure the hostname (Net, Host, Gateway, or Domain name) is a text string up to 24 characters drawn from the alphabet (A-Z), digits (0-9), minus sign (-), and period (.). Note that periods are only allowed when they serve to delimit components of "domain style names". For more details, read the memo [RFC-921](https://tools.ietf.org/html/rfc921) and [RFC-952](https://tools.ietf.org/html/rfc952).

Once you have downloaded the application and configured the pre-requisite, click [Installation Steps](installation.md) to see how to get started.

# Port Prerequisites

For successful installation/upgradation of <code class="expression">space.vars.OIM</code>, following ports are required to be available as per the chosen configuration and database.

## Connection Protocol Selection
Choosing the right protocol depends on your network environment and security needs.

1. **HTTP (Port 8989)**
   * **Usage:** Supported mainly for on-premise deployments where the <code class="expression">space.vars.OIM</code> is hosted within a trusted, customer-controlled network and protected by internal firewall rules or a reverse proxy.
   * **Security Consideration:** Network isolation, firewall enforcement, and controlled access are expected to be in place to mitigate exposure risks and vulnerable attacks.

2. **HTTPS (Port 8443) – Recommended**
   * **Usage:** Required for cloud-based, or internet-facing public deployments of <code class="expression">space.vars.OIM</code>.
   * **Security Benefit:** HTTPS provides encrypted communication, ensuring data confidentiality, integrity, and authenticity.
## Database Port

* **9001**: If you are installing <code class="expression">space.vars.OIM</code> with HSQL database.

> **Note**: Apart from the above ports, some connectors require certain ports to be available. Please refer the [Connectors](../connectors/connectors.md) section to check ports used by specific connectors.

# Appendix
## Windows specific configuration

{% include "../.gitbook/includes/windows-specific-configuration.md" %}
