# Feature: Display Home

**Feature ID:** 8
**Branch pattern:** `feature/8-display-home`
**Status:** Ready
**Created:** 2026-11-05
**Input:** Display consulting system home dashboard with system overview, active projects, pending timesheets, and recent invoices.
**Depends on:** — [Feature 4 — Maintain Projects](feature-4-maintain-projects.md), [Feature 5 — Maintain Timesheets](feature-5-maintain-timesheets.md), [Feature 7 — Maintain Invoices](feature-7-maintain-invoices.md)

---

## User Stories

### US-8.1: View home dashboard
**As a** user (owner, PM, team member, accounting, contractor)
**I want to** view a central home dashboard upon logging in
**So that** I get an immediate overview of active consulting activities, key metrics, and navigation shortcuts

**Priority:** P1
**Independent test:** Navigate to the home route `/` and verify dashboard metrics and summary widgets load
**Acceptance scenarios:** see ### US-8.1 under Acceptance Criteria

### US-8.2: View action items and pending tasks
**As a** PM or accounting member
**I want to** see counts and quick links for timesheets awaiting review and overdue invoices
**So that** I can promptly act on pending operational workflows

**Priority:** P1
**Independent test:** View the pending items widget and verify correct counts corresponding to database records
**Acceptance scenarios:** see ### US-8.2 under Acceptance Criteria

---

## Acceptance Criteria (Gherkin)

### US-8.1 — View home dashboard

#### Scenario: User navigates to home page successfully
* **Given** an authenticated user is on the consulting application
* **When** the user navigates to the home page
* **Then** the system displays the overview KPI cards with active project counts, pending timesheets, and recent invoices
* **And** displays navigation quick links to all primary entities

#### Scenario: No records exist in database
* **Given** the database is newly initialized with zero active records
* **When** the user visits the home page
* **Then** the system displays empty state indicators with 0 counts without error

### US-8.2 — View action items and pending tasks

#### Scenario: PM views pending timesheet approvals on dashboard
* **Given** there are unreviewed timesheet entries submitted by workers
* **When** a PM opens the home dashboard
* **Then** the pending timesheets notification counter indicates the exact number of unreviewed entries
* **And** clicking the notification navigates directly to the timesheet review view

#### Scenario: No pending actions exist for current user
* **Given** all timesheets have been reviewed and no invoices are overdue
* **When** a PM or owner visits the dashboard
* **Then** the action items widget displays "All tasks completed - no pending reviews"
* **And** badge counter indicates 0 pending actions

