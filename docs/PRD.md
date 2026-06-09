# Product Requirements Document (PRD)

## Project: MyMonitoredMorning
**Document Version:** 1.0.0  
**Date:** June 9, 2026  
**Status:** Draft for Review  
**Lead PM:** Elrond (PM Agent)

---

## 1. Executive Summary & Vision

### 1.1 Objective
**MyMonitoredMorning** is a secure, multi-user web-based medical journal designed to help individuals and caregivers track and monitor healthcare metrics, activities, and events (e.g., blood glucose levels, meals, seizure activity).

### 1.2 Core Philosophy
* **Generic and Extensible:** Instead of building custom, rigid databases for every unique medical condition, the application uses a highly flexible, tag-based logging model.
* **Frictionless Entry:** Medical logging often happens during stressful or busy moments. Creating an entry must be fast, intuitive, and require minimal inputs.
* **Delegated Collaboration:** Healthcare is cooperative. The platform must natively support delegation, allowing family members, caregivers, or partners to record metrics on behalf of patients.

---

## 2. User Roles & Personas

| Role | Description | Core Capabilities |
| :--- | :--- | :--- |
| **Account Owner (Patient)** | The individual whose health data is being tracked. | Can log self-entries, view historical trends, and grant/revoke logging delegation to other users. |
| **Delegate Logger** | A trusted user (e.g., caregiver, partner, parent, nurse) who has been authorized to log on behalf of the Owner. | Can switch context to the Owner’s profile to view and/or write log entries, based on delegated permissions. |

---

## 3. Functional Requirements

### 3.1 User Management & Authentication
* **FR-1.1:** A user must be able to securely register, log in, and manage their profile.
* **FR-1.2:** All user session states must isolate health data, ensuring users can only access records they own or are authorized to view/edit.

### 3.2 Generic Logging System
* **FR-2.1:** Users must be able to create a new **Journal Entry**.
* **FR-2.2:** Each journal entry must consist of the following schema:
  * **ID:** Unique identifier.
  * **Timestamp:** Date and time of the event (defaults to current time but must be editable).
  * **Title/Event Type:** A short description of the event (e.g., "Breakfast", "Blood Glucose Check", "Absence Seizure").
  * **Notes/Details:** Optional rich text or plain text field for deep details.
  * **Numeric Value & Unit:** Optional decimal field and standard unit text (e.g., Value: `115`, Unit: `mg/dL`; Value: `3`, Unit: `mins`).
  * **Tags:** Array of string tags (e.g., `["diabetes", "fasting", "seizure", "grand-mal"]`).
  * **Logged By:** The ID of the user who physically wrote the entry (crucial for delegated accountability).
  * **Logged For:** The ID of the user whose profile the entry belongs to.

### 3.3 Flexible Tagging System
* **FR-3.1:** Tags must be entirely organic and case-insensitive.
* **FR-3.2:** The creation UI must offer **tag autocompletion** based on the user's previously used tags to ensure taxonomy consistency.
* **FR-3.3:** Users must be able to filter their timeline feed by single or multiple tags (using AND/OR logical operators).

### 3.4 Delegated Logging & Permissions
* **FR-4.1 (Bi-directional Delegation):** A user (User A) can invite another registered user (User B) to become a **Delegate** for their profile, and vice-versa.
* **FR-4.2 (Delegation Workflow):**
  1. **Request:** User A enters User B's email/username and sends a "Delegation Request" with a selected permission tier.
  2. **Approval:** User B receives a notification and must explicitly accept the request.
  3. **Establishment:** Once accepted, the delegation relationship is active.
* **FR-4.3 (Permission Tiers):**
  * **Write-Only (Log-Only):** The delegate can submit new log entries for the Owner but cannot view past logs or historical charts. (Ideal for school nurses, temporary sitters, or high-privacy situations).
  * **Read-Write (Full Caregiver):** The delegate can log new entries and view the Owner's full timeline and metrics.
* **FR-4.4 (Profile Switching):** If User B is a delegate for User A, User B must have a profile-switcher menu to shift their active view to "User A's Journal" before logging.
* **FR-4.5 (Audit Logging):** Every entry must clearly display: *"Logged by [Delegate Name] on behalf of [Owner Name]"* to maintain strict accountability.

### 3.5 Journal Feed & Data Visualization
* **FR-5.1 (Chronological Feed):** A unified feed showing entries in reverse-chronological order.
* **FR-5.2 (Metric Dashboard):** The UI must automatically detect numeric values associated with specific tags (e.g., `blood-glucose`) and display them in a **historical trend line chart**.
* **FR-5.3 (Medical Export):** Users must be able to export filtered log views (e.g., all entries with tag `seizure` over the last 30 days) into a clean, shareable **PDF or CSV report** for doctor appointments.

---

## 4. Non-Functional Requirements

### 4.1 Security & Data Isolation
* **NFR-1.1:** Secure transit of data via TLS.
* **NFR-1.2:** Strict server-side validation to ensure a Delegate cannot write to or read from a profile unless an active, approved delegation record exists.
* **NFR-1.3:** Encryption of sensitive data at rest.

### 4.2 Performance & Ease of Use
* **NFR-2.1:** Mobile-First Design. The interface must be fully responsive, ensuring medical details can easily be logged on-the-go via smartphones.
* **NFR-2.2:** Form inputs must support rapid entry (e.g., keyboard shortcuts, numeric-only pads for metrics, swipe actions to delete/edit).

---

## 5. Exclusions (Out of Scope for MVP)
* Offline-first local synchronization (planned for v2.0).
* Automatic AI-based anomaly detection or medical advice.
* Direct integration with hospital EHR (Electronic Health Record) systems.
