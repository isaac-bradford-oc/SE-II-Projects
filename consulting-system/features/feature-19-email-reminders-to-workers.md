# Feature: Email Reminders to Workers

**Feature ID:** 19
**Branch pattern:** `feature/19-email-reminders-to-workers`
**Status:** Ready
**Created:** 2026-11-05
**Input:** Email timesheet submission reminders to workers (team members and contractors) with unsubmitted or missing timesheets.
**Depends on:** — [Feature 1 — Maintain Workers](feature-1-maintain-workers.md), [Feature 5 — Maintain Timesheets](feature-5-maintain-timesheets.md), [Feature 4 — Maintain Projects](feature-4-maintain-projects.md)

---

## User Stories

### US-19.1: Send timesheet reminder emails to workers
**As a** PM or accounting member
**I want to** email reminder notifications to workers who have unsubmitted timesheets or missing hours for the current period
**So that** workers submit their hours on time before the billing cycle closes

**Priority:** P1
**Independent test:** Trigger reminder email to workers with missing hours and verify dispatch to worker email addresses
**Acceptance scenarios:** see ### US-19.1 under Acceptance Criteria

### US-19.2: Filter reminder recipients by project or worker type
**As a** PM
**I want to** filter workers needing reminders by specific project or worker type (team members vs. contractors)
**So that** I can send targeted follow-up reminders

**Priority:** P1
**Independent test:** Filter by contractor worker type and verify reminder recipients list updates accordingly
**Acceptance scenarios:** see ### US-19.2 under Acceptance Criteria

---

## Acceptance Criteria (Gherkin)

### US-19.1 — Send timesheet reminder emails to workers

#### Scenario: PM sends reminder to workers with unsubmitted timesheets
* **Given** 3 workers have unsubmitted timesheets for the current week
* **When** the PM selects the workers and clicks "Send Reminders"
* **Then** the system sends personalized reminder emails to each of the 3 workers
* **And** records entries in the `email_logs` table
* **And** displays visual confirmation "3 reminder emails sent successfully"

#### Scenario: Worker has invalid or missing email address
* **Given** a selected worker has a malformed email address
* **When** the reminder email process executes
* **Then** the system flags the invalid email with an InvalidRecipientEmailException
* **And** continues processing remaining valid recipients while reporting the error

### US-19.2 — Filter reminder recipients

#### Scenario: Filter by project
* **Given** workers on multiple projects have pending timesheets
* **When** the user selects "Project Phoenix" from the project filter
* **Then** the recipient list displays only workers assigned to "Project Phoenix" who have not submitted time

#### Scenario: All filtered workers have already submitted on time
* **Given** all workers assigned to "Project Phoenix" have already submitted timesheets for the period
* **When** the user filters reminder recipients by "Project Phoenix"
* **Then** the system displays "No workers require reminders for the selected project"
* **And** disables the "Send Reminders" action button

