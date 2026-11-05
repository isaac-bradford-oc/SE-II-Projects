# Feature: Display Projects

**Feature ID:** 12
**Branch pattern:** `feature/12-display-projects`
**Status:** Ready
**Created:** 2026-11-05
**Input:** Display consulting projects including client, estimated completion date, PM, assigned workers, timesheets, and invoices.
**Depends on:** — [Feature 4 — Maintain Projects](feature-4-maintain-projects.md), [Feature 6 — Maintain Clients](feature-6-maintain-clients.md), [Feature 1 — Maintain Workers](feature-1-maintain-workers.md)

---

## User Stories

### US-12.1: View all projects
**As a** user
**I want to** view a list of all consulting projects
**So that** I can track active, completed, and upcoming engagements

**Priority:** P1
**Independent test:** Navigate to `/projects` and verify project listings show client, PM, dates, and status
**Acceptance scenarios:** see ### US-12.1 under Acceptance Criteria

### US-12.2: View project details and associations
**As a** PM or owner
**I want to** drill down into a project's detailed view
**So that** I can see assigned workers, logged timesheets, and generated invoices for that project

**Priority:** P1
**Independent test:** Click a project and verify assigned workers, timesheets tab, and invoices tab
**Acceptance scenarios:** see ### US-12.2 under Acceptance Criteria

### US-12.3: Filter projects by client or status
**As a** user
**I want to** filter projects by client or status (Active, Completed, On Hold)
**So that** I can focus on projects requiring attention

**Priority:** P1
**Independent test:** Apply status filter 'Active' and verify only active projects appear
**Acceptance scenarios:** see ### US-12.3 under Acceptance Criteria

---

## Acceptance Criteria (Gherkin)

### US-12.1 — View all projects

#### Scenario: User views projects list successfully
* **Given** projects exist in the database
* **When** the user navigates to `/projects`
* **Then** the system displays all projects with client name, PM, estimated completion date, and status

#### Scenario: No projects exist
* **Given** no projects have been created
* **When** the user navigates to `/projects`
* **Then** the system displays a message indicating no projects are found with an option to create one

### US-12.2 — View project details and associations

#### Scenario: PM views project details
* **Given** a project exists with assigned workers, timesheets, and invoices
* **When** the user clicks on the project name
* **Then** the system renders the project details page showing the assigned workers roster, timesheets list, and invoice summary

#### Scenario: Project details accessed for invalid project ID
* **Given** a user attempts to navigate to a non-existent project page `/projects/999`
* **When** the page request is processed
* **Then** the system throws a ProjectNotFoundException
* **And** displays an error notification to the user

### US-12.3 — Filter projects by client or status

#### Scenario: User filters projects by status
* **Given** active and completed projects exist in the system
* **When** the user selects status filter 'Active'
* **Then** the projects list updates to show only active projects

#### Scenario: Filter criteria matches no projects
* **Given** no projects have status 'On Hold'
* **When** the user filters projects by 'On Hold'
* **Then** the system displays an empty table state with message "No projects match the selected filter criteria"

