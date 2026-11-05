# Feature: Maintain Projects

**Feature ID:** 4
**Branch pattern:** `feature/4-maintain-projects`
**Status:** Ready
**Created:** 2026-11-05
**Input:** Maintain projects including client, estimated completion date, PM, assigned workers, timesheets, and invoices.
**Depends on:** — [Feature 1 — Maintain Workers](feature-1-maintain-workers.md), [Feature 6 — Maintain Clients](feature-6-maintain-clients.md)

---

## User Stories

### US-4.1: Add project
**As an** owner or PM
**I want to** create a new project associated with a client, designated PM, and estimated completion date
**So that** consulting engagements can be organized, staffed, and tracked

**Priority:** P1
**Independent test:** Create a project in the database and verify its presence in the projects list
**Acceptance scenarios:** see ### US-4.1 under Acceptance Criteria

### US-4.2: Edit project
**As an** owner or PM
**I want to** edit project details including estimated completion date, assigned PM, and project status
**So that** schedule or staffing changes are properly kept up-to-date

**Priority:** P1
**Independent test:** Edit an existing project's estimated completion date and verify changes in the database
**Acceptance scenarios:** see ### US-4.2 under Acceptance Criteria

### US-4.3: Assign workers to project
**As a** PM
**I want to** assign or remove workers on a project
**So that** team members and contractors can log timesheets against the project

**Priority:** P1
**Independent test:** Assign a worker to a project and verify their association in the project_workers table
**Acceptance scenarios:** see ### US-4.3 under Acceptance Criteria

### US-4.4: Delete project
**As an** owner
**I want to** delete an unstarted or cancelled project
**So that** inactive or erroneous project entries are removed from active operations

**Priority:** P1
**Independent test:** Delete a project and confirm its removal from the database
**Acceptance scenarios:** see ### US-4.4 under Acceptance Criteria

---

## Acceptance Criteria (Gherkin)

### US-4.1 — Add project

#### Scenario: User creates project successfully
* **Given** an owner or PM fills in the "add project" form with valid details (name, client, PM, dates)
* **When** the user clicks save
* **Then** the system records the new project in the database
* **And** the user receives confirmation of project creation

#### Scenario: Missing required fields
* **Given** a user leaves the client or estimated completion date blank
* **When** the user submits the form
* **Then** the system throws a MissingRequiredFieldsException
* **And** the user receives visual validation feedback

### US-4.2 — Edit project

#### Scenario: User updates project successfully
* **Given** a PM updates the estimated completion date on an active project
* **When** the user saves the changes
* **Then** the system updates the project record in the database
* **And** the user receives confirmation of successful update

#### Scenario: Invalid completion date entered
* **Given** a PM attempts to set an estimated completion date that is earlier than the project start date
* **When** the user clicks save
* **Then** the system throws an InvalidProjectDateException
* **And** displays visual validation feedback indicating the date conflict

### US-4.3 — Assign workers to project

#### Scenario: Worker assigned to project
* **Given** a PM selects one or more workers to add to a project team
* **When** the user clicks "assign workers"
* **Then** the system adds corresponding entries to `project_workers`
* **And** the assigned workers appear on the project roster

#### Scenario: Worker already assigned to project
* **Given** a selected worker is already assigned to the project
* **When** the PM attempts to assign the worker again
* **Then** the system throws a DuplicateAssignmentException
* **And** notifies the user that the worker is already on the project team

### US-4.4 — Delete project

#### Scenario: Project deleted successfully
* **Given** an owner initiates deletion for a project that has no associated timesheets or invoices
* **When** deletion is confirmed
* **Then** the system deletes the project record from the database
* **And** the user receives visual confirmation

#### Scenario: Deletion blocked due to existing timesheets or invoices
* **Given** an owner attempts to delete a project with recorded timesheets or generated invoices
* **When** deletion is initiated
* **Then** the system throws a ProjectInUseException
* **And** the system notifies the user that projects with financial records cannot be deleted

