# Feature: Email Referees

**Feature ID:** 23
**Branch pattern:** `feature/23-email-referees`
**Status:** Ready
**Created:** 2026-10-17
**Input:** Email referees to notify them of schedule changes and other updates.
**Depends on:** — [Feature 10 — Maintain Referees](feature-10-maintain-referees.md)

---

## User Stories

### US-23.1: Email referee
**As a** owner
**I want to** email referee(s)
**So that** referees are in the loop on relevant updates

**Priority:** P1
**Independent test:** Email referee(s) and verify that email(s) were sent to the corresponding addresses
**Acceptance scenarios:** see ### US-23.1 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST allow owners to email all referees or a subset of referees.
- **FR-002**: System MUST optionally allow owners to filter the referee subset based on sport, league, or team.
- **FR-003**: System MUST validate email recipients before sending email.
- **FR-004**: System MUST provide the user with visual confirmation of action taken after attempting to send email.

---

## Key Entities

- **referee**: a referee with name, email, sports, and positions.

---

## Data Model Requirements

### referees

| Column | Notes |
|--------|-------|
| id | PK, int |
| name | nvarchar(100), required |
| email | nvarchar(254), required |

### referee_positions

| Column | Notes |
|--------|-------|
| id | PK, int |
| referee_id | FK, int |
| sport_id | FK, int |
| position_id | FK, int |

---

## Acceptance Criteria (Gherkin)

### US-23.1 — Email referee

#### Scenario: User emails referee(s) successfully
* **Given** an owner fills in the "email referee" form with acceptable information
* **When** the user submits the form
* **Then** the system emails referee(s)
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "email referee" form with invalid information (e.g. too many characters)
* **When** the user submits the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation
