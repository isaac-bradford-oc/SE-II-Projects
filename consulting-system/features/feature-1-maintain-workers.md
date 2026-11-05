# Feature: Maintain Workers

**Feature ID:** 1
**Branch pattern:** `feature/1-maintain-workers`
**Status:** Ready
**Created:** 2026-11-05
**Input:** Maintain list of both internal and external workers (owner, PM, team members, accounting, contractor).
**Depends on:** — 

---

## User Stories

### US-1.1: Add worker
**As an** owner
**I want to** add a worker to the database
**So that** worker profiles and organizational assignments remain up-to-date

**Priority:** P1
**Independent test:** Add a worker to the database and view the worker in the workers table
**Acceptance scenarios:** see ### US-1.1 under Acceptance Criteria

### US-1.2: Edit worker
**As an** owner
**I want to** edit an existing worker's details
**So that** worker contact information and organizational roles stay accurate

**Priority:** P1
**Independent test:** Edit a worker in the database and verify the updated information in the database table
**Acceptance scenarios:** see ### US-1.2 under Acceptance Criteria

### US-1.3: Delete worker
**As an** owner
**I want to** delete or deactivate a worker from the database
**So that** former workers are no longer active in the system

**Priority:** P1
**Independent test:** Remove a worker from the database and confirm they no longer appear in the active workers list
**Acceptance scenarios:** see ### US-1.3 under Acceptance Criteria

---

## Acceptance Criteria (Gherkin)

### US-1.1 — Add worker

#### Scenario: User adds worker successfully
* **Given** an owner fills in the "add worker" form with valid information
* **When** the user submits the form
* **Then** the system saves the worker to the database
* **And** the user receives visual confirmation of success

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "add worker" form with invalid information (e.g., invalid email or missing name)
* **When** the user submits the form
* **Then** the system prevents saving and throws an exception
* **And** the user receives visual confirmation of the validation error

### US-1.2 — Edit worker

#### Scenario: User edits worker successfully
* **Given** an owner fills in the "edit worker" form with valid updated information
* **When** the user saves the changes
* **Then** the system updates the worker record in the database
* **And** the user receives visual confirmation of success

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "edit worker" form with invalid information
* **When** the user saves the changes
* **Then** the system throws an exception
* **And** the user receives visual confirmation of the error

### US-1.3 — Delete worker

#### Scenario: User deletes worker successfully
* **Given** an owner selects the delete button for a worker and confirms the action
* **When** the deletion is confirmed
* **Then** the system removes or deactivates the worker in the database
* **And** the user receives visual confirmation of successful deletion

#### Scenario: Deletion fails due to associated records
* **Given** an owner attempts to delete a worker who is associated with existing projects or timesheets
* **When** the deletion is initiated
* **Then** the system prevents deletion and throws a DependencyConstraintException
* **And** the user receives an appropriate error notification

