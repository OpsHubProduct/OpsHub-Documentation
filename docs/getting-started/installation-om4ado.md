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

# Launching Installer

Double-click the `OM4ADO<version>.exe` file. User requires Administrator privileges to start the installer.

> **Note:** If any version of <code class="expression">space.vars.OM4ADO</code> is already installed, you will receive a notification. Click **Yes** to continue with the installation. This will overwrite the previous installation with the current version.

<p align="center">
  <img src="../assets/Installation1.png" width="1000"/>
</p>

## Read License Agreement

This is the End User License Agreement window. Read the license agreement and, if you agree with the terms, select **I acknowledge and agree with the above** to continue with the installation.

<p align="center">
  <img src="../assets/Installation2.png" width="1000"/>
</p>

# Installation

## Select Installation Path

Select the installation directory. Before selecting a directory, make sure it is empty. All log files, configuration files, and servers are placed in this directory. If the directory does not exist, you can create one as per your requirements.

<p align="center">
  <img src="../assets/Installation3.png" width="1000"/>
</p>

## Registration

Each installation must be registered with <code class="expression">space.vars.OM4ADO</code>. Registration can be completed either in Online or Offline mode.

Please refer to the [Registration](registration.md) page for more details.

## Database Selection

{% include "Database_Selection.md" %}

## Advanced Installation

* If you want to create databases manually, select the checkbox **Check this if you will be creating databases manually**. The instructions to create databases are provided in the [Manual Creation of Databases](#manual-creation-of-databases) section.
* If the checkbox is not selected, enter the names of the databases that you want to configure. Based on the selected database type (MySQL, MS SQL/Azure SQL, PostgreSQL, or Oracle), the databases/schemas will be created automatically.
* Database names can contain `$`, `_`, `#`, alphabets, and numbers without spaces.
* Make sure to use unique database names for each installation of <code class="expression">space.vars.OM4ADO</code>.

<p align="center">
  <img src="../assets/Installation4.png" width="1000"/>
</p>

## Installation Progress

Once this window appears, the installation process has started. The installation may take approximately 45 minutes to complete.

<p align="center">
  <img src="../assets/Installation5.png" width="1000"/>
</p>

## Installation Success

The screenshot below indicates that the installation has completed successfully. There is an additional step to set up the shortcut. Click **Next** to continue.

<p align="center">
  <img src="../assets/Installation6.png" width="1000"/>
</p>

## Setup Shortcut

This step adds the application to the Windows program list and creates the <code class="expression">space.vars.OM4ADO</code> Launcher.

<p align="center">
  <img src="../assets/Installation7.png" width="1000"/>
</p>

## Successful Installation

Clicking **Next** displays the following screen, indicating that the installation is complete.

<p align="center">
  <img src="../assets/Installation8.png" width="1000"/>
</p>

Once the installation is complete, refer to [Launching OpsHub Migrator for Microsoft Azure DevOps](Launching_OpsHub_Migrator_for_Microsoft_Azure_DevOps.md) for more details.

# Appendix

## Manual Creation of Databases

## Queries for MySQL database
{% include "../.gitbook/includes/manual-mysqldatabase-creation.md" %}

## Queries for MS SQL/Azure SQL Database
{% include "../.gitbook/includes/manual-mssqldatabase-creation.md" %}

## Queries for Oracle Database
{% include "../.gitbook/includes/manual-oracledatabase-creation.md" %}

## Queries for PostgreSQL Database
{% include "../.gitbook/includes/manual-postgresdatabase-creation.md" %}

## Collation Change of MS SQL/Azure SQL Databases

{% include "../.gitbook/includes/collation-change.md" %}