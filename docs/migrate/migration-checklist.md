## Permissions

Before starting the migration, ensure that the required permissions are configured.

For more details, refer to the [Permission Prerequisites](../connectors/azure-devops.md#prerequisites).

---

## Projects in Target System

<code class="expression">space.vars.OM4ADO</code> does not create projects in the target system (**TFS / Azure DevOps**). It only migrates data between matching projects in the source and target systems.

### Project Creation Requirements

Before starting migration:

- Create the project(s) manually in the target system.
- Ensure the **project name matches exactly** with the source project, including:
    - Spaces
    - Numeric characters
    - Special characters
- Ensure the **same process template** is used in both systems:
    - Agile
    - CMMI
    - Scrum

### Correct Examples

| Source Project | Template | Target Project | Template |
|---|---|---|---|
| Project A | Agile | Project A | Agile |
| ProjectA1 | CMMI | ProjectA1 | CMMI |
| Project_A_1 | Scrum | Project_A_1 | Scrum |
| Project A.1 | Agile | Project A.1 | Agile |

### Incorrect Examples

| Source Project | Template | Target Project | Template |
|---|---|---|---|
| Project A | Agile | ProjectA | Agile |
| ProjectA1 | CMMI | Project_A1 | CMMI |
| Project_A_1 | Scrum | Project_A_1 | Agile |
| Project A.1 | Agile | Project A.1 | Scrum |

### Why Incorrect Configurations Cause Issues

#### Project Name Mismatch

If the project name in the target system does not exactly match the source system:

- Migration will fail to proceed.
- The required project must be created manually with the correct name.

#### Template Mismatch

Example:

```text
Project_A_1 (Scrum) → Project_A_1 (Agile)
```

Migration may continue, but the following issues can occur:

##### Entity Mismatch

If an entity available in the source template does not exist in the target template:

- The entity will not be migrated.

##### Field Mismatch

If required fields are unavailable in the target system:

- Those fields will not be migrated.

##### Value Mismatch

If field value mappings are incompatible:

- Migration may result in missing or incorrect values.

> To avoid migration issues, ensure project names and templates are consistent between source and target systems.

### Prerequisite for Changeset Migration

For migrations involving **Changesets**:

- The endpoint user must have **Basic access**.
- **Stakeholder access** is not supported.

Otherwise, the following error may appear:

```text
<<Your Project>> is using Git Version Control
```

---

## Customization (Entity / Field / Value)

The **Premium Edition of** <code class="expression">space.vars.OM4ADO</code> supports migration of customized source systems.

However:

- <code class="expression">space.vars.OM4ADO</code> does **not create customizations** in the target system.
- Custom entities, fields, and values must be created manually in the target project before migration.

### Validation Warnings

During validation, <code class="expression">space.vars.OM4ADO</code> checks for customization mismatches.

Warnings may appear when:

- A custom entity is missing
- A field is unavailable
- A value mapping is incompatible

You can:

- Review mismatches from the validation dropdown
- Export mismatches using **Export Template Mismatch**

### Query-Based Suite Migration

If query-based suite migration is supported and the custom field **Source Workitem ID** is missing for the **Test Case** entity in the target system, <code class="expression">space.vars.OM4ADO</code> will show a validation warning.

To migrate query-based suites successfully:

1. Create a custom field named **Source Workitem ID** in the target system.
2. Ensure the field type is **Integer**.
3. Retry migration configuration.

If the field is not created:

- Query-based suites will be migrated as **Static Suites**.

> **Note:** Validation is performed after the **User Mapping** step. If customized data is not required in the target system, validation warnings may be ignored.

---

## User Mapping

User mapping is mandatory for all users in the source system.

<code class="expression">space.vars.OM4ADO</code> will not proceed until every source user is mapped to one or more users in the target system.

### Automatic Mapping

<code class="expression">space.vars.OM4ADO</code> automatically maps users that exist in both:

- Source system
- Target system

### Manual Mapping Options

For unmapped users, you can:

- Create matching users in the target system and rerun migration
- Map users individually
- Map multiple users to a single target account
- Use **Default User Mapping** for deleted users

For more information, refer to [Provide User Mapping](migration-configuration.md#user-mapping).

---

## Meta Entities Migration

The **Ultimate Edition of** <code class="expression">space.vars.OM4ADO</code> supports migration of the following meta entities:

- Area
- Iteration
- Group
- Team
- User

### Group Migration Prerequisites

When migrating **Groups**:

- Source and target systems should use the **same Active Directory**, or
- Both systems must contain **Active Directory groups with identical names**

Additionally:

- All AD groups in the source system should be added to a native group in the target system.

---

## Delivery Plan Migration

The **Ultimate Edition of** <code class="expression">space.vars.OM4ADO</code> supports migration of the Delivery Plan entity.

To synchronize the Delivery Plan entity, the OpsHub integration user must be a member of both the **Project Collection Administrators** group and the **Project Administrators** group.
  * Note: Membership in the **Project Collection Administrators** group is required to synchronize the teams associated with the Delivery Plan

For migrating the Delivery Plans in Azure DevOps Server version 2020 and below, the Delivery Plan Market Place Extension must be installed on the instance in order to perform delivery plans related operations. 

Link to the extension: [Delivery Plan Market Place Extension](https://marketplace.visualstudio.com/items?itemName=ms.vss-plans)

### Dependent Entities

Before migrating release pipelines, migrate the Team entity first. Migrating these dependencies first helps prevent synchronization failures.

---

## Release Pipeline Migration

To migrate **Release Pipelines**, certain dependencies must already exist in the target project.

### Required Pre-existing Resources

Ensure required resources are available in the target system before migration.

Refer to the **Release Pipeline Pre-requisites** documentation for details.

### Dependent Entities

Before migrating release pipelines, migrate the following entities first:

- Service Connections
- Agent Pools
- Task Groups

Migrating these dependencies first helps prevent synchronization failures.

For more information, refer to the **Release Pipeline dependent entities** section.