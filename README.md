# MyMonitoredMorning

**MyMonitoredMorning** is a secure, multi-user web-based medical journal designed for individuals and caregivers to log and monitor health metrics, meals, activities, and events (e.g., blood glucose, seizure logs) through a highly flexible, organic tagging system.

---

## 🚀 Program & Management Overview

This repository is organized and tracked using professional Agile/Scrum practices. 

* **Product Requirements Document:** [docs/PRD.md](file:///docs/PRD.md)
* **Active Epic & Story Backlog:** Managed directly in [GitHub Issues](https://github.com/jeffvan1018/MyMonitoredMorning03/issues)
* **Initiative Tracking PR:** [PR #1 (docs: Product Requirements Document (PRD) for MyMonitoredMorning)](https://github.com/jeffvan1018/MyMonitoredMorning03/pull/1)

---

## 📋 Core Specifications

### 1. Flexible Log Schema
Rather than relying on rigid, condition-specific database structures, MyMonitoredMorning tracks all events under a single, extensible journal entry format:
* **Timestamp** (defaults to current time, editable)
* **Title / Event Type** (e.g., "Lunch", "Glucose Measurement", "Tonic-clonic Seizure")
* **Notes** (optional narrative text)
* **Numeric Value & Unit** (optional decimal + text fields for blood-sugar levels, event durations, etc.)
* **Tags** (array of organic, case-insensitive taxonomy tags)
* **Logged By & Logged For** (relational IDs to manage bi-directional delegated logging)

### 2. Bi-Directional Delegation
The program natively supports caregiver networks:
* **Invite/Approval Workflow:** Patients can delegate record logging to caregivers, who must explicitly accept.
* **Permission Tiers:**
  * **Log-Only (Write-Only):** Delegates can submit new logs but cannot view patient timeline history or dashboards.
  * **Caregiver (Read-Write):** Delegates have full view and write access.
* **Context Switching:** Delegates can switch active profiles from a unified dropdown menu to record logs on behalf of patients.
* **Audit Trail:** Every log displays clear accountability metrics (e.g., *"Logged by Caregiver John on behalf of Patient Jane"*).

### 3. Metric Visualizations & Export
* **Trends Dashboard:** Automatic generation of line graphs tracking numeric metrics over time (e.g., blood glucose trend tracking).
* **Physician Export:** Filter logs by custom date-ranges and tag groups, exporting them as CSV or a print-ready layout for healthcare visits.

---

## 🗂 Document Directory

All program, product, and functional specifications are maintained under the `/docs/` directory:
```
docs/
└── PRD.md   # Feature specifications, user personas, and acceptance criteria
```

---
*For development setups, environment variables, or architecture-adjacent guidelines, refer to the technical documents (under construction by the architecture team).*
