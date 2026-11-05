# Feature: Display Roles

**Feature ID:** 10
**Branch pattern:** `feature/10-display-roles`
**Status:** Ready
**Created:** 2026-11-05
**Input:** Display consulting roles and SLA role definitions.
**Depends on:** — [Feature 2 — Maintain Roles](feature-2-maintain-roles.md)

---

## User Stories

### US-10.1: View all roles
**As a** PM or owner
**I want to** view a list of all defined roles in the system
**So that** I can review available job roles and their governance source (client SLA or PM managed)

**Priority:** P1
**Independent test:** Navigate to `/roles` and verify all roles appear in the table
**Acceptance scenarios:** see ### US-10.1 under Acceptance Criteria

### US-10.2: Filter roles by source
**As a** PM
**I want to** filter roles by whether they are client SLA-defined or PM-managed
**So that** I can quickly identify SLA contractual roles

**Priority:** P1
**Independent test:** Filter by "Client SLA" and verify only SLA-sourced roles are shown
**Acceptance scenarios:** see ### US-10.2 under Acceptance Criteria

---

## Acceptance Criteria (Gherkin)

### US-10.1 — View all roles

#### Scenario: User views roles list successfully
* **Given** roles exist in the database
* **When** the user visits the `/roles` page
* **Then** all roles are displayed with name, description, source type, and SLA reference

#### Scenario: No roles defined
* **Given** no roles exist in the database
* **When** the user visits the `/roles` page
* **Then** the page displays an empty state with a prompt to add a new role

### US-10.2 — Filter roles by source

#### Scenario: User filters by Client SLA
* **Given** roles with various sources exist
* **When** the user selects "Client SLA" from the source filter
* **Then** the system displays only roles where source_type is 'Client SLA'

#### Scenario: Filter yields zero results
* **Given** only 'PM Managed' roles exist in the database
* **When** the user filters by "Client SLA"
* **Then** the system displays an empty table state with message "No roles found matching selected source criteria"

