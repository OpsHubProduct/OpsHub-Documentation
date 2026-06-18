---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# API Capability Matrix - <code class="expression">space.vars.OIM</code>

This document provides an overview of API capabilities available in <code class="expression">space.vars.OIM</code>.
It outlines which operations (Get, Create, Update, Delete, List, Execute) are supported across Integration and Admin modules.

Use this matrix as a quick reference to understand API coverage.

---

## Legend

| Symbol | Meaning                 |
|--------|-------------------------|
| ✅     | Available in API        |
| ❌     | Not Available in API    |
| —      | Not Applicable          |

---

## Integration

| Feature / Module      | Get | Create | Update | Delete | List | Execute | Notes                                                     |
|----------------------|----|------|-----|------|----|---------|-----------------------------------------------------------|
| System               | ✅  | ✅    | ✅  | —    | ✅ | —       | —                                                         |
| System Type          |  —  |    —  |  —  |  —   | ✅ | —       | —                                                         |
| System Template      | ✅  | —     | —   | —    | —  | —       | —                                                         |
| Mapping              | ✅  | ✅    | ✅  | ✅   | ✅ | —       | —                                                         |
| Integration          | ✅  | ✅    | ✅  | ✅   | ✅ | ✅      | <span style="color:red;">API to get sync log files</span> |
| Workflow             | ✅  | ✅    | ✅  | ✅   | ✅ | —       | —                                                         |
| Folder               | ✅  | ✅    | ✅  | ✅   | ✅ | —       | —                                                         |
| Excel Upload         | ✅  | ✅    | ✅  | ✅   | ✅ | —       | —                                                         |
| Reconcile            | ✅  | —    | —   | —    | —  | ✅      | —                                                         |
| Processing Failure   | ✅  | —    | ✅  | ✅   | ✅ | ✅      | —                                                         |
| Global Failure       | ✅  | —    | —   | ✅   | ✅ | —       | —                                                         |
| Failure Notification | ✅  | ✅    | ✅  | ✅   | —  | —       | —                                                         |
| Sync Report          | —  | —    | —   | —    | ✅ | —       | —                                                         |
| Audits               | —  | —    | —   | —    | ❌ | —       | —                                                         |

---

## Admin

| Feature / Module        | Get | Create | Update | Delete | List | Execute | Notes               |
|-------------------------|-----|--------|--------|--------|------|---------|---------------------|
| System Information      | ❌  | —      | —      | —      | —    | —       | —                   |
| User                    | ❌  | ❌     | ❌     | —      | ✅   | —       | —                   |
| User-Role               | ✅  | —      | ✅     | —      | —    | —       | —                   |
| Role                    | ✅  | ✅     | ✅     | ✅     | ✅   | —       | —                   |
| SDK                     | ✅  | ✅     | ✅     | —      | ✅   | —       | —                   |
| Scheduler               | ✅  | ✅     | ✅     | ✅     | ✅   | —       | —                   |
| Log Setting             | ✅  | —      | ✅     | —      | —    | —       | —                   |
| Usage Report            | ✅  | —      | —      | —      | —    | —       | —                   |
| Trends Dashboard        | ✅  | —      | —      | —      | —    | —       | —                   |
| Login Server Management | ❌  | ❌     | ❌     | ❌     | ❌   | ❌      | —                   |
| License                 | —   | —      | —      | —      | —    | —       | Not there by design |
| Purge                   | —   | —      | —      | —      | —    | —       | Not there by design |
| Rules                   | —   | —      | —      | —      | —    | —       | Not there by design |

