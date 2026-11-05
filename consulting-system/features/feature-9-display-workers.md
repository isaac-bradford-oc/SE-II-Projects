# Feature: Display Workers

**Feature ID:** 9
**Branch pattern:** `feature/9-display-workers`
**Status:** Ready
**Created:** 2026-11-05
**Input:** Display all workers and access individual worker information.
**Depends on:** — [Feature 1 — Maintain Workers](feature-1-maintain-workers.md)

---

## User Stories

### US-9.1: View all workers
**As an** owner, PM, or accounting member
**I want to** view a list of all workers with their contact details and worker types
**So that** I can see the organization's workforce and staffing roster

**Priority:** P1
**Independent test:** Navigate to `/workers` and verify all registered workers appear in the table
**Acceptance scenarios:** see ### US-9.1 under Acceptance Criteria

### US-9.2: Filter and search workers
**As a** user
**I want to** filter workers by type (owner, PM, team member, accounting, contractor) or search by name
**So that** I can quickly locate specific workers

**Priority:** P1
**Independent test:** Apply a worker type filter and verify only matching workers are listed
**Acceptance scenarios:** see ### US-9.2 under Acceptance Criteria

### US-9.3: Access worker details
**As a** user
**I want to** click on a worker to view their assigned projects and profile
**So that** I can understand their assignments and workload

**Priority:** P1
**Independent test:** Click a worker entry and view their details page
**Acceptance scenarios:** see ### US-9.3 under Acceptance Criteria

---

## Acceptance Criteria (Gherkin)

### US-9.1 — View all workers

#### Scenario: User views workers list successfully
* **Given** registered workers exist in the database
* **When** the user navigates to the workers page
* **Then** the system displays all workers with their name, type, and contact info

#### Scenario: No workers exist in database
* **Given** no workers have been registered in the database
* **When** the user visits the workers page
* **Then** the system displays an empty table state with a message "No workers found"

### US-9.2 — Filter and search workers

#### Scenario: Filter workers by worker type
* **Given** a list of workers with various worker types
* **When** the user selects the filter for "contractor"
* **Then** the table updates to display only workers with worker type 'contractor'

#### Scenario: Search query returns zero matches
* **Given** registered workers exist in the database
* **When** the user searches for a name that does not exist (e.g. "NonExistentName")
* **Then** the system displays an empty table state with message "No workers match the specified search criteria"

### US-9.3 — Access worker details

#### Scenario: User navigates to worker details
* **Given** the workers list is displayed
* **When** the user clicks on a specific worker's row
* **Then** the system displays the worker details page with their contact information and project assignments

#### Scenario: Worker details requested for invalid ID
* **Given** a user navigates directly to `/workers/99999` where ID 99999 does not exist
* **When** the page loads
* **Then** the system throws a WorkerNotFoundException
* **And** displays an error message indicating the worker profile does not exist

