# Feature: Display Timesheets

**Feature ID:** 13
**Branch pattern:** `feature/13-display-timesheets`
**Status:** Ready
**Created:** 2026-11-05
**Input:** Display timesheets tracked per worker per role (project, role, date, hours, status [not reviewed, reviewed, invoiced], worker).
**Depends on:** — [Feature 5 — Maintain Timesheets](feature-5-maintain-timesheets.md), [Feature 1 — Maintain Workers](feature-1-maintain-workers.md), [Feature 2 — Maintain Roles](feature-2-maintain-roles.md), [Feature 4 — Maintain Projects](feature-4-maintain-projects.md)

---

## User Stories

### US-13.1: View all timesheets
**As a** PM, owner, or accounting member
**I want to** view a comprehensive list of all logged timesheet entries
**So that** I can monitor hours logged across all projects and workers

**Priority:** P1
**Independent test:** Navigate to `/timesheets` and verify entries display with worker, project, role, date, hours, and status
**Acceptance scenarios:** see ### US-13.1 under Acceptance Criteria

### US-13.2: Filter timesheets by status, worker, or project
**As a** user
**I want to** filter timesheets by status ('not reviewed', 'reviewed', 'invoiced'), by worker, or by project
**So that** I can isolate entries needing review or ready for invoicing

**Priority:** P1
**Independent test:** Filter by status 'not reviewed' and verify only unreviewed entries appear
**Acceptance scenarios:** see ### US-13.2 under Acceptance Criteria

### US-13.3: Worker views personal timesheet history
**As a** worker
**I want to** view my own timesheet history for a given week or pay period
**So that** I can track my logged hours and review status

**Priority:** P1
**Independent test:** Log in as a worker, view personal timesheets, and verify only personal entries appear
**Acceptance scenarios:** see ### US-13.3 under Acceptance Criteria

---

## Acceptance Criteria (Gherkin)

### US-13.1 — View all timesheets

#### Scenario: User views timesheet list successfully
* **Given** timesheet entries exist in the database
* **When** an authorized user opens the timesheets page
* **Then** the table displays entries showing worker, project, role, date, hours, and status

#### Scenario: No timesheets exist in database
* **Given** no timesheet records exist in the database
* **When** an authorized user opens the timesheets page
* **Then** the system displays an empty table state with message "No timesheet entries found"

### US-13.2 — Filter timesheets by status

#### Scenario: User filters by 'not reviewed'
* **Given** timesheets exist with 'not reviewed', 'reviewed', and 'invoiced' statuses
* **When** the user selects status filter 'not reviewed'
* **Then** only timesheets with status 'not reviewed' are shown
* **And** the total hours counter reflects the sum of displayed entries

#### Scenario: Filter criteria yields zero timesheet matches
* **Given** there are no timesheets with status 'invoiced' for a selected project
* **When** the user applies the filter for status 'invoiced'
* **Then** the system displays "No timesheets match the selected criteria"
* **And** total hours counter displays 0.00

### US-13.3 — Worker views personal timesheet history

#### Scenario: Team member views personal log
* **Given** a team member logs in
* **When** they view the timesheets screen
* **Then** the view defaults to their own timesheets
* **And** displays status indicators for each entry

#### Scenario: Worker has no logged time for selected period
* **Given** a newly hired contractor has logged no hours for the current week
* **When** the contractor navigates to their personal timesheets screen
* **Then** the system displays "No hours logged for this period" with an option to "Log Time"

