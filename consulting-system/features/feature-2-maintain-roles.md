# Feature: Maintain Roles

**Feature ID:** 2
**Branch pattern:** `feature/2-maintain-roles`
**Status:** Ready
**Created:** 2026-11-05
**Input:** Maintain consulting roles pulled from client SLA and/or managed by PMs.
**Depends on:** — 

---

## User Stories

### US-2.1: Add role
**As a** PM or owner
**I want to** add a new consulting role
**So that** project tasks can be properly staffed and billed according to project SLAs

**Priority:** P1
**Independent test:** Add a role to the system and verify it appears in the roles database table
**Acceptance scenarios:** see ### US-2.1 under Acceptance Criteria

### US-2.2: Edit role
**As a** PM or owner
**I want to** edit an existing role
**So that** role definitions, source SLA mappings, and responsibilities remain accurate

**Priority:** P1
**Independent test:** Edit a role's name or source and verify the updated data persists
**Acceptance scenarios:** see ### US-2.2 under Acceptance Criteria

### US-2.3: Delete role
**As a** PM or owner
**I want to** delete an obsolete role
**So that** unused roles do not clutter staffing and billing options

**Priority:** P1
**Independent test:** Delete a role from the database and confirm it no longer appears in the roles list
**Acceptance scenarios:** see ### US-2.3 under Acceptance Criteria

---

## Acceptance Criteria (Gherkin)

### US-2.1 — Add role

#### Scenario: User adds role successfully
* **Given** a PM or owner fills in the "add role" form with valid role information
* **When** the user clicks save
* **Then** the system inserts the role into the database
* **And** the user receives visual confirmation of success

#### Scenario: Duplicate role name provided
* **Given** a user inputs a role name that already exists in the database
* **When** the user clicks save
* **Then** the system throws a DuplicateRoleException
* **And** the user is notified that the role name must be unique

### US-2.2 — Edit role

#### Scenario: User edits role successfully
* **Given** a PM or owner modifies an existing role with valid information
* **When** the user saves the changes
* **Then** the system updates the role in the database
* **And** the user receives confirmation that the role has been updated

#### Scenario: User inputs invalid role details
* **Given** a user attempts to update a role with an empty name
* **When** the user saves the changes
* **Then** the system throws a ValidationException
* **And** the changes are not saved

### US-2.3 — Delete role

#### Scenario: User deletes role successfully
* **Given** a PM or owner initiates deletion for a role with no associated project rates or timesheets
* **When** the user confirms deletion
* **Then** the system removes the role from the database
* **And** the user receives confirmation of deletion

#### Scenario: Role has existing dependencies
* **Given** a user initiates deletion for a role currently assigned in active rates or timesheets
* **When** the user confirms deletion
* **Then** the system throws a RoleInUseException
* **And** the user is notified that active roles cannot be deleted

