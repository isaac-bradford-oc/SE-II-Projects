# Feature: Approve Timesheets

**Feature ID:** 17
**Branch pattern:** `feature/17-approve-timesheets`
**Status:** Ready
**Created:** 2026-11-05
**Input:** Approve or reject submitted timesheets (transition status from 'not reviewed' to 'reviewed').
**Depends on:** — [Feature 5 — Maintain Timesheets](feature-5-maintain-timesheets.md), [Feature 16 — Submit Timesheets](feature-16-submit-timesheets.md), [Feature 4 — Maintain Projects](feature-4-maintain-projects.md)

---

## User Stories

### US-17.1: Approve timesheet entry
**As a** PM or owner
**I want to** review and approve timesheets submitted for my projects
**So that** hours are validated for invoicing and the status is changed from 'not reviewed' to 'reviewed'

**Priority:** P1
**Independent test:** Approve a timesheet entry and verify its status updates to 'reviewed' in the database
**Acceptance scenarios:** see ### US-17.1 under Acceptance Criteria

### US-17.2: Bulk approve timesheets
**As a** PM
**I want to** select multiple submitted timesheets and approve them in batch
**So that** I can efficiently process team timesheets at the end of a billing cycle

**Priority:** P1
**Independent test:** Select multiple 'not reviewed' entries, execute bulk approve, and verify all change to 'reviewed'
**Acceptance scenarios:** see ### US-17.2 under Acceptance Criteria

### US-17.3: Reject timesheet entry with feedback
**As a** PM
**I want to** reject an erroneous timesheet entry with an explanatory reason
**So that** the worker can correct the discrepancy and resubmit

**Priority:** P1
**Independent test:** Reject a timesheet entry with comments and verify the worker is alerted and status allows edits
**Acceptance scenarios:** see ### US-17.3 under Acceptance Criteria

---

## Acceptance Criteria (Gherkin)

### US-17.1 — Approve timesheet entry

#### Scenario: PM approves a single timesheet
* **Given** a timesheet entry has status 'not reviewed'
* **When** the PM clicks "Approve"
* **Then** the system updates the status to 'reviewed'
* **And** sets `reviewed_by` to the PM's ID and `reviewed_at` to the current time
* **And** displays visual confirmation "Timesheet approved"

#### Scenario: PM attempts to approve an already invoiced timesheet
* **Given** a timesheet entry already has status 'invoiced'
* **When** a user attempts to approve it
* **Then** the system throws a TimesheetAlreadyProcessedException
* **And** blocks status modification

### US-17.2 — Bulk approve timesheets

#### Scenario: PM bulk approves multiple timesheet entries
* **Given** 5 timesheets with status 'not reviewed' are selected
* **When** the PM clicks "Bulk Approve"
* **Then** all 5 timesheets update to status 'reviewed'
* **And** a summary confirmation displays "5 timesheets approved"

#### Scenario: PM triggers bulk approve with no entries selected
* **Given** zero timesheet checkboxes are checked in the review queue
* **When** the PM clicks "Bulk Approve"
* **Then** the system throws a NoTimesheetsSelectedException
* **And** displays a warning message "Please select at least one timesheet to approve"

### US-17.3 — Reject timesheet entry with feedback

#### Scenario: PM rejects timesheet entry
* **Given** a timesheet has incorrect role or hours
* **When** the PM enters a rejection note "Incorrect role selected" and clicks "Reject"
* **Then** the system saves the rejection note and returns the entry to the worker
* **And** notifies the worker of the rejection

#### Scenario: PM attempts rejection without required feedback note
* **Given** a PM attempts to reject a timesheet entry without entering a reason
* **When** the PM clicks "Confirm Rejection"
* **Then** the system throws a MissingRejectionReasonException
* **And** prompts the user that a rejection explanation is required

