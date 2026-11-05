# Feature: Submit Timesheets

**Feature ID:** 16
**Branch pattern:** `feature/16-submit-timesheets`
**Status:** Ready
**Created:** 2026-11-05
**Input:** Submit timesheet hours for review by project managers.
**Depends on:** — [Feature 5 — Maintain Timesheets](feature-5-maintain-timesheets.md), [Feature 1 — Maintain Workers](feature-1-maintain-workers.md), [Feature 4 — Maintain Projects](feature-4-maintain-projects.md)

---

## User Stories

### US-16.1: Submit timesheet entries for a period
**As a** worker (team member or contractor)
**I want to** submit my logged timesheet entries for a work period to my PM
**So that** my hours can be officially reviewed and approved for billing

**Priority:** P1
**Independent test:** Select unreviewed/draft timesheet entries and submit them; verify status remains 'not reviewed' and submission timestamp is recorded
**Acceptance scenarios:** see ### US-16.1 under Acceptance Criteria

### US-16.2: Bulk submit weekly timesheet
**As a** worker
**I want to** submit all logged entries for a selected week in a single action
**So that** I do not have to submit individual entries one by one

**Priority:** P1
**Independent test:** Click "Submit Week", confirm submission, and verify all entries for that week are locked against worker edits
**Acceptance scenarios:** see ### US-16.2 under Acceptance Criteria

---

## Acceptance Criteria (Gherkin)

### US-16.1 — Submit timesheet entries for a period

#### Scenario: Worker successfully submits weekly timesheet
* **Given** a worker has logged 40 hours across the current week with status 'not reviewed'
* **When** the worker clicks "Submit Timesheet" and confirms
* **Then** the system marks the entries as submitted with the current timestamp
* **And** locks the entries from arbitrary worker editing
* **And** displays visual confirmation "Timesheet submitted for review"

#### Scenario: Submitting with zero hours logged
* **Given** a worker has not logged any hours for the selected period
* **When** the worker attempts to submit
* **Then** the system throws an EmptyTimesheetSubmissionException
* **And** alerts the worker that at least one entry with hours is required

### US-16.2 — Bulk submit weekly timesheet

#### Scenario: Worker successfully submits full week timesheets
* **Given** a worker has logged daily hours for Monday through Friday of the current week
* **When** the worker clicks "Submit Week" and confirms
* **Then** the system submits all timesheet entries for that entire week simultaneously
* **And** locks the entire weekly block against edits
* **And** displays confirmation "Weekly timesheet submitted successfully"

#### Scenario: Attempting to bulk submit an already submitted week
* **Given** a worker has already submitted all timesheets for the current week
* **When** the worker attempts to click "Submit Week" again
* **Then** the system throws a TimesheetAlreadySubmittedException
* **And** disables further submission for that period

