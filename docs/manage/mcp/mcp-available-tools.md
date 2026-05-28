---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

This page lists all tools exposed by the <code class="expression">space.vars.OIM</code> MCP server. Your AI assistant uses these tools to perform operations on your <code class="expression">space.vars.OIM</code> instance.

> **Note**: You do not invoke these tools directly. Your AI assistant selects and calls the appropriate tools based on your natural language prompt. This reference helps you understand what is available and what each tool does.

> **Note**: Delete operations are not supported via any MCP tool. See [Known Behaviours and Limitations](mcp-known-limitations.md) for details.

---

## Planner tools

Planner tools guide the AI assistant through the correct sequence of steps before performing complex operations. The AI assistant calls the relevant planner automatically before executing create, update, or action operations on the corresponding resource.

| Tool | Description |
|------|-------------|
| `system_planner` | Provides a step-by-step execution plan for system operations (create, update, list, get). Ensures the AI assistant gathers all required inputs before calling system API tools. |
| `mapping_planner` | Provides a step-by-step execution plan for mapping operations (create, update, list, get). Ensures field metadata, entity types, and transformation requirements are resolved before creating or updating a mapping. |
| `integration_planner` | Provides a step-by-step execution plan for integration operations (create, update, list, get, activate, inactivate, execute). |
| `folder_planner` | Provides a step-by-step execution plan for folder operations (create, update, list, get). |
| `schedules_planner` | Provides a step-by-step execution plan for schedule operations (create, update, list, get). |
| `health_checkup_planner` | Guides the AI assistant through a comprehensive multi-stage health checkup of the <code class="expression">space.vars.OIM</code> instance — covering integrations, systems, mappings, failures, and instance resource parameters. Produces a visual dashboard with colour-coded health status and prioritised recommendations. |
| `failure_resolution_planner` | Guides the AI assistant through a structured diagnostic process to identify the root cause of integration failures. Covers integration configuration, mapping, system connectivity, and permissions, and produces a step-by-step resolution plan. |

---

## System tools

| Tool | Description |
|------|-------------|
| `getSystemTypes` | Lists all supported system types available in <code class="expression">space.vars.OIM</code> with their system type IDs. Supports search by system name and pagination. |
| `getSystemTypeTemplate` | Retrieves the required fields and configuration template for a given system type. Used by the AI assistant to understand what inputs are needed before creating or updating a system. |
| `get_systems_list` | Lists all systems configured in the <code class="expression">space.vars.OIM</code> instance with search, filter, and sort capabilities. |
| `get_system` | Retrieves full details of a specific system by its ID. |
| `create_system` | Creates a new system (endpoint) in <code class="expression">space.vars.OIM</code>.|
| `update_system` | Updates an existing system's configuration by its ID.|

---

## Metadata tools

Metadata tools retrieve structural information about systems — such as available projects, entity types, fields, and lookup values. These are used by the AI assistant when building or validating mappings.

| Tool | Description |
|------|-------------|
| `get_projects` | Retrieves the list of projects available in a specific system. |
| `get_entities` | Retrieves the list of entity types (e.g., issues, defects, stories) available for a given system and project. |
| `get_fields_meta` | Retrieves field metadata for a given system and entity type, including field names, types, and whether they are required or read-only. |
| `get_lookup_values` | Retrieves the allowed values for a specific lookup-type field in a system (e.g., status values, priority values). |
| `get_complex_fields_meta` | Retrieves internal metadata for complex field types — comments, links, and attachments — for both systems in a mapping. Used to configure advanced field-level transformations. |

---

## Mapping tools

| Tool | Description |
|------|-------------|
| `get_mappings_list` | Lists all mappings configured in the instance with search, filter, and sort capabilities. |
| `get_mapping` | Retrieves the full configuration of a specific mapping by its ID, including all field mappings and transformation rules. |
| `create_mapping` | Creates a new mapping between two entity types.|
| `update_mapping` | Updates an existing mapping by its ID. |
| `get_advanced_transformation_comment` | Retrieves the advanced XSLT transformation scripts for comment field mapping, including user mention, entity mention, and comment XSLT scripts. Called after a base mapping is created when comment field mapping requires advanced configuration. |

---

## XSLT tools

XSLT tools provide reference guidance that the AI assistant uses when generating or validating advanced field-level transformations in mappings.

| Tool | Description |
|------|-------------|
| `Advanced_XSLT_Transformation_Guidelines` | Provides the strict rules and constraints that the AI assistant must follow when generating or updating advanced XSLT used in field mappings. |
| `Core_Utility_Methods_Reference_for_advanced_XSLT` | Provides the library of available utility method definitions that can be used within XSLT transformations for field mappings. |

---

## Integration tools

| Tool | Description                                                                                                                                                                                                                                     |
|------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `get_integrations_list` | Lists all integrations configured in the instance with search, filter, and sort capabilities.                                                                                                                                                   |
| `get_integration` | Retrieves the full configuration of a specific integration by its ID, including project pairs, entity pairs, sync directions, and settings.                                                                                                     |
| `create_integration` | Creates a new integration.                                                                                                                                                                                                                      |
| `update_integration` | Updates an existing integration by its ID.                                                                             |
| `execute_status_change` | Changes the execution status of one or more integrations. Supports three actions: **activate** (enable the integration for scheduled sync), **inactivate** (disable the integration), and **execute** (trigger an immediate on-demand sync cycle). |
| `get_advanced_config_settings_integration` | Retrieves all advanced configuration settings available for a given integration and direction — including override parameters for read/write operations and criteria configuration.                |

---

## Folder tools

| Tool | Description |
|------|-------------|
| `get_folders_list` | Lists all folders in the instance with search, filter, and sort capabilities. |
| `get_folder` | Retrieves details of a specific folder by its ID. |
| `create_folder` | Creates a new folder. The parent folder must exist. |
| `update_folder` | Updates an existing folder by its ID. |

---

## Schedule tools

| Tool | Description |
|------|-------------|
| `get_schedules_list` | Lists all schedules configured in the instance. Supports filtering by schedule type, status, and name. |
| `get_schedule` | Retrieves details of a specific schedule by its ID, including type, configuration, status, and next execution time. |
| `create_schedule` | Creates a new schedule for automating integration execution.  |
| `update_schedule` | Updates an existing schedule by its ID.  |

---

## Workflow tools

| Tool | Description |
|------|-------------|
| `get_workflows` | Lists all workflows available in the instance with search, filter, and sort capabilities. Workflows can be referenced when configuring integration settings. |

---

## Failure tools

| Tool | Description |
|------|-------------|
| `get_global_failures_list` | Lists global failures across all integrations with search, filter, and sort capabilities. Global failures indicate errors that stopped an entire integration cycle. |
| `get_global_failure` | Retrieves full details of a specific global failure by its ID, including the stack trace. |
| `get_processing_failures_list` | Lists processing failures with search, filter, and sort capabilities. Processing failures are record-level failures where a specific item failed to sync. |
| `get_processing_failure` | Retrieves full details of a specific processing failure by its ID. Can optionally include dependent failure records. |
| `retry_processing_failures` | Retries one or more processing failures, re-queuing the failed records for synchronization. |

---

## Health & diagnostics tools

| Tool | Description |
|------|-------------|
| `get_oim_system_information` | Retrieves complete details about the <code class="expression">space.vars.OIM</code> instance — including OS, heap memory usage, disk space, database connection pool utilisation, HTTP thread pool usage, active thread count, log folder size, and global log level. Used during health checkup to assess instance resource health. |
