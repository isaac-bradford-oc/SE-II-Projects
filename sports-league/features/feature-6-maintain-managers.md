# Feature: Maintain Managers

**Feature ID:** 6
**Branch pattern:** `feature/6-maintain-managers`
**Status:** Ready
**Created:** 2026-10-17
**Input:** Keep current list of managers' information updated.
**Depends on:** — 

---

## User Stories

### US-6.1: Add manager
**As a** owner
**I want to** add a manager to the database
**So that** the table of managers remains up-to-date

**Priority:** P1
**Independent test:** Add a manager to the database and view it in a database table
**Acceptance scenarios:** see ### US-6.1 under Acceptance Criteria

### US-6.2: Edit manager
**As a** owner
**I want to** edit a manager in the database
**So that** manager information remains up-to-date

**Priority:** P1
**Independent test:** Edit a manager in the database and view it in a database table
**Acceptance scenarios:** see ### US-6.2 under Acceptance Criteria

### US-6.3: Delete manager
**As a** owner
**I want to** delete a manager from the database
**So that** the table of managers remains up-to-date

**Priority:** P1
**Independent test:** Remove a manager from the database and see that it is not in a database table
**Acceptance scenarios:** see ### US-6.3 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST allow owners to manage individual managers.
- **FR-002**: System MUST validate user form input before saving to database.
- **FR-003**: System MUST provide the user with visual confirmation of action taken after attempting to save input.

### Screen Requirements

- **SR-001**: Add and Edit operations should each have one corresponding screen.
- **SR-002**: Add screen should have input fields for all required database columns, a create button, and cancel button.
- **SR-003**: Edit screen should have input fields for all required database columns, a save button, and cancel button.

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

### US-6.1 — Add manager

#### Scenario: User adds manager successfully
* **Given** an owner fills in the "add manager" form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "add manager" form with invalid information (e.g. too many characters)
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-6.2 — Edit manager

#### Scenario: User edits manager successfully
* **Given** an owner fills in the "edit manager" form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "edit manager" form with invalid information
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-6.3 — Delete manager

#### Scenario: User deletes manager successfully
* **Given** an owner clicks the "delete manager" button
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner clicks the "delete manager" button
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation