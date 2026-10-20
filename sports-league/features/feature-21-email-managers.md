# Feature: Email Managers

**Feature ID:** 21
**Branch pattern:** `feature/21-email-managers`
**Status:** Ready
**Created:** 2026-10-17
**Input:** Email managers to notify them of schedule changes and other updates.
**Depends on:** — [Feature 6 — Maintain Managers](feature-6-maintain-managers.md)

---

## User Stories

### US-21.1: Email manager
**As a** owner
**I want to** email manager(s)
**So that** managers are in the loop on relevant updates

**Priority:** P1
**Independent test:** Email manager(s) and verify that email(s) were sent to the corresponding addresses
**Acceptance scenarios:** see ### US-21.1 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST allow owners to email all managers or a subset of managers.
- **FR-002**: System MUST optionally allow owners to filter the manager subset based on sport, league, or team.
- **FR-003**: System MUST validate email recipients before sending email.
- **FR-004**: System MUST provide the user with visual confirmation of action taken after attempting to send email.

### Screen Requirements

- **SR-001**: Screen should have multi-select dropdowns for selecting managers, sports, leagues, and/or teams, subject and body text fields, and a send button.

---

## Key Entities

- **manager**: a manager with name, email, seasons, and teams.

---

## Data Model Requirements

### managers

| Column | Notes |
|--------|-------|
| id | PK, int |
| name | nvarchar(100), required |
| email | nvarchar(254), required |

### manager_teams

| Column | Notes |
|--------|-------|
| id | PK, int |
| season_id | FK, int |
| team_id | FK, int |
| manager_id | FK, int |

---

## Acceptance Criteria (Gherkin)

### US-21.1 — Email manager

#### Scenario: User emails manager(s) successfully
* **Given** an owner fills in the "email manager" form with acceptable information
* **When** the user submits the form
* **Then** the system emails managers(s)
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "add manager" form with invalid information (e.g. too many characters)
* **When** the user submits the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation