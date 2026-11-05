# Feature: Maintain Rates

**Feature ID:** 3
**Branch pattern:** `feature/3-maintain-rates`
**Status:** Ready
**Created:** 2026-11-05
**Input:** Maintain billing rates per role per project.
**Depends on:** — [Feature 2 — Maintain Roles](feature-2-maintain-roles.md), [Feature 4 — Maintain Projects](feature-4-maintain-projects.md)

---

## User Stories

### US-3.1: Add rate
**As a** PM or accounting member
**I want to** establish a billing rate for a specific role on a project
**So that** project work is billed at the contracted rate

**Priority:** P1
**Independent test:** Add a project-role rate entry and confirm it is stored in the rates table
**Acceptance scenarios:** see ### US-3.1 under Acceptance Criteria

### US-3.2: Edit rate
**As a** PM or accounting member
**I want to** update the hourly rate for a role on a project
**So that** changes in contract or SLA terms are reflected in billing

**Priority:** P1
**Independent test:** Modify an existing rate value and verify the updated rate in the database
**Acceptance scenarios:** see ### US-3.2 under Acceptance Criteria

### US-3.3: Delete rate
**As a** PM or accounting member
**I want to** delete an invalid or discontinued rate entry
**So that** inaccurate rates are not applied to project timesheets or invoices

**Priority:** P1
**Independent test:** Remove a rate entry from the database and verify it no longer exists
**Acceptance scenarios:** see ### US-3.3 under Acceptance Criteria

---

## Acceptance Criteria (Gherkin)

### US-3.1 — Add rate

#### Scenario: User creates a rate successfully
* **Given** an accounting member or PM fills in the "add rate" form with a valid project, role, and positive hourly rate
* **When** the user clicks save
* **Then** the system saves the rate record to the database
* **And** the user receives visual confirmation of success

#### Scenario: Negative or zero rate entered
* **Given** a user inputs a rate value of 0 or a negative number
* **When** the user submits the form
* **Then** the system throws an InvalidRateValueException
* **And** the user receives a validation error message

#### Scenario: Duplicate role rate for project
* **Given** a rate already exists for the selected project and role combination
* **When** the user attempts to add the duplicate rate
* **Then** the system throws a DuplicateRateException
* **And** the user is informed that a rate is already configured for this role and project

### US-3.2 — Edit rate

#### Scenario: User updates rate successfully
* **Given** a PM or accounting member modifies the hourly rate with an acceptable value
* **When** the user clicks update
* **Then** the system updates the rate in the database
* **And** the user receives visual confirmation

#### Scenario: User enters non-positive rate during edit
* **Given** an authorized user modifies an existing rate to 0 or a negative amount
* **When** the user attempts to save changes
* **Then** the system throws an InvalidRateValueException
* **And** the changes are rejected with a validation error message

### US-3.3 — Delete rate

#### Scenario: User deletes rate successfully
* **Given** an authorized user selects delete on an unused rate
* **When** the deletion is confirmed
* **Then** the system removes the rate from the database
* **And** the user receives confirmation of removal

#### Scenario: Deletion blocked due to existing timesheets
* **Given** an authorized user attempts to delete a rate that has already been billed on timesheets
* **When** the deletion is confirmed
* **Then** the system throws a RateInUseException
* **And** the system prevents deletion to maintain billing audit integrity

