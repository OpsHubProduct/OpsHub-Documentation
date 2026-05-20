---
if: >-
   visitor.claims.unsigned.product === "OM4ADO"
layout:
  width: wide
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: false
  pagination:
    visible: false
  metadata:
    visible: false
---

# Deployment Options

* **On Premise:** Can be deployed on a local virtual machine or local server.
* **On Customer Cloud:** Can be deployed on a cloud service hosted by the customer. Supported cloud services include Amazon EC2 and Microsoft Azure.

# Installation Prerequisites

## Supported Operating Systems  
* Windows 11 and Windows Server 2016 and above (64 bit)
* For Windows specific configuration, refer [Windows specific configuration](prerequisites.md#windows-specific-configuration)

## Hardware Prerequisites

1. RAM - Minimum 8 GB (recommended)
2. Disk Space - Minimum `2x GB` free space on the drive where <code class="expression">space.vars.OM4ADO</code> will be installed (recommended).

    * Here, `x` represents the total database size of the repositories for which the change sets are to be migrated in parallel.
    * If migrations are performed sequentially for multiple repositories, `x` can be considered as the maximum repository size among the repository list.

> **Note:** The disk space prerequisite applies only to users migrating Version Control data and not to users migrating only work item data.

## Ports Prerequisites

<code class="expression">space.vars.OM4ADO</code> uses ports `8989` and `9090`.

> **Note:** Ensure that these ports are open and available.

## .NET Framework Prerequisites

Installation of <code class="expression">space.vars.OM4ADO</code> requires Microsoft .NET Framework `4.7.2` or higher on the machine where OM4ADO will be installed.

## Database Prerequisites

<code class="expression">space.vars.OIM</code> can be deployed with an embedded database; however, for production deployment or anything other than functional testing, our experts highly recommend using an external database. <code class="expression">space.vars.OIM</code> supports the following database.
Note: If the database is hosted on a separate Windows machine, the operating system must be Windows 11 or Windows Server 2016 and later.

### 1. MySQL Server

{% include "../.gitbook/includes/mysql-preq.md" %}

### 2. MS SQL/Azure SQL Server

{% include "../.gitbook/includes/mssql-preq.md" %}

### 3. Oracle

{% include "../.gitbook/includes/oracle-preq.md" %}

### 4. PostgreSQL Server

{% include "../.gitbook/includes/posgres-preq.md" %}

> **Note**: If default connection timeout parameter is changed for any database server, then it must be confirmed that sufficient connection timeout has been set. For example, for MySQL the default server-side connection timeout is 8 hours. If it is changed and set to, say, 5 minutes, then the default server-side connection timeout must be updated accordingly. **<code class="expression">space.vars.OIM</code>** maintains connection pools that keep connections alive for 8 hours. Based on the need, this parameter can be tuned at both the application and database-server levels.**Generally, the recommended timeout is between 6-8 hours.**

## Download Database Connector jar

| Database Type  | Database Version | Download Link                                                                                                               |
| -------------- | ---------------- | --------------------------------------------------------------------------------------------------------------------------- |
| **MySQL**      | All              | [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j)                                                            |
|  **MSSQL**     | 2012 and lower   | [Download Link](https://www.microsoft.com/en-in/download/details.aspx?id=11774)                                             |
|  | 2014 onward      | [Release Notes](https://learn.microsoft.com/en-us/sql/connect/jdbc/release-notes-for-the-jdbc-driver?view=sql-server-ver16) |
| **Oracle**     | 11g              | [Oracle JDBC 11g](https://www.oracle.com/jp/technical-resources/articles/features/jdbc/jdbc.html)                           |
|                | 12c              | [Oracle JDBC 12c](https://www.oracle.com/technetwork/database/features/jdbc/jdbc-drivers-12c-download-1958347.html)         |
|                | 19c              | [Oracle JDBC 19c](https://www.oracle.com/database/technologies/appdev/jdbc-ucp-19c-downloads.html)                          |
| **PostgreSQL** | All              | [PostgreSQL JDBC](https://jdbc.postgresql.org/download/)                                                                    |


## Team Foundation Server/Azure DevOps Prerequisites

{% include "TFS_Prerequisites.md" %}

# Proxy Configuration

{% include "Proxy_Configuration.md" %}

# Appendix

## Windows Specific Configuration

{% include "Windows_Specific_Configuration.md" %}