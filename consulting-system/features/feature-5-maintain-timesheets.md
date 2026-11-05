# Feature: Maintain Timesheets

**Feature ID:** 5
**Branch pattern:** `feature/5-maintain-timesheets`
**Status:** Ready
**Created:** 2026-11-05
**Input:** Maintain timesheet entries per worker per role (project, role, date, hours, status [not reviewed, reviewed, invoiced], worker).
**Depends on:** — [Feature 1 — Maintain Workers](feature-1-maintain-workers.md), [Feature 2 — Maintain Roles](feature-2-maintain-roles.md), [Feature 4 — Maintain Projects](feature-4-maintain-projects.md)

---

## User Stories

### US-5.1: Add timesheet entry
**As a** worker or PM
**I want to** log timesheet hours for a specific project, role, and date
**So that** billable and non-billable consulting hours are accurately recorded

**Priority:** P1
**Independent test:** Add a timesheet record with project, role, date, and hours, and verify it appears in the timesheets table
**Acceptance scenarios:** see ### US-5.1 under Acceptance Criteria

### US-5.2: Edit timesheet entry
**As a** worker or PM
**I want to** edit hours, role, or description on an unreviewed timesheet entry
**So that** mistakes or updated work descriptions can be corrected

**Priority:** P1
**Independent test:** Modify the hours and notes on an existing unreviewed timesheet entry and verify the update
**Acceptance scenarios:** see ### US-5.2 under Acceptance Criteria

### US-5.3: Delete timesheet entry
**As a** worker or PM
**I want to** delete an incorrect unreviewed timesheet entry
**So that** erroneous time records do not propagate to client invoicing

**Priority:** P1
**Independent test:** Delete a timesheet entry and confirm it no longer appears in the database
**Acceptance scenarios:** see ### US-5.3 under Acceptance Criteria

---

## Acceptance Criteria (Gherkin)

### US-5.1 — Add timesheet entry

#### Scenario: Worker logs timesheet entry successfully
* **Given** a worker inputs valid project, role, date, and hours worked
* **When** the user submits the timesheet entry
* **Then** the system saves the entry with status 'not reviewed'
* **And** the user receives visual confirmation of the saved time entry

#### Scenario: User enters invalid hours
* **Given** a worker enters 0 or negative hours, or hours greater than 24
* **When** the user submits the timesheet entry
* **Then** the system throws an InvalidTimesheetHoursException
* **And** the user receives visual validation feedback

### US-5.2 — Edit timesheet entry

#### Scenario: Worker edits unreviewed timesheet successfully
* **Given** a worker updates hours on a timesheet entry whose status is 'not reviewed'
* **When** the user saves the changes
* **Then** the system updates the record in the database
* **And** the user receives confirmation of update

#### Scenario: User attempts to edit a reviewed or invoiced timesheet
* **Given** a worker attempts to modify a timesheet entry whose status is 'reviewed' or 'invoiced'
* **When** the user attempts to submit changes
* **Then** the system throws a TimesheetLockedException
* **And** the modification is rejected

### US-5.3 — Delete timesheet entry

#### Scenario: Worker deletes unreviewed timesheet successfully
* **Given** a worker selects delete on a timesheet entry with status 'not reviewed'
* **When** deletion is confirmed
* **Then** the system removes the entry from the database
* **And** the user receives visual confirmation

#### Scenario: Attempting to delete an invoiced timesheet
* **Given** a user attempts to delete a timesheet entry with status 'invoiced'
* **When** deletion is attempted
* **Then** the system blocks the deletion and throws a LockedRecordException

