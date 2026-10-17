# Feature: Maintain Referees

**Feature ID:** 10
**Branch pattern:** `feature/10-maintain-referees`
**Status:** Ready
**Created:** 2026-10-11
**Input:** Keep current list of referees' information updated.
**Depends on:** — 

---

## User Stories

### US-10.1: Add referee
**As a** owner
**I want to** add a referee to the database
**So that** the table of referees remains up-to-date

**Priority:** P1
**Independent test:** Add a referee to the database and view it in a database table
**Acceptance scenarios:** see ### US-10.1 under Acceptance Criteria

### US-10.2: Edit referee
**As a** owner
**I want to** edit a referee in the database
**So that** referee information remains up-to-date

**Priority:** P1
**Independent test:** Edit a referee in the database and view it in a database table
**Acceptance scenarios:** see ### US-10.2 under Acceptance Criteria

### US-10.3: Delete referee
**As a** owner
**I want to** delete a referee from the database
**So that** the table of referees remains up-to-date

**Priority:** P1
**Independent test:** Remove a referee from the database and see that it is not in a database table
**Acceptance scenarios:** see ### US-10.3 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST allow owners to manage individual referees.
- **FR-002**: System MUST validate user form input before saving to database.
- **FR-003**: System MUST provide the user with visual confirmation of action taken after attempting to save input.

---

## Key Entities

- **Referee**: a referee with name, email, sports, and positions.

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

### US-10.1 — Add referee

#### Scenario: User adds referee successfully
* **Given** an owner fills in the "add referee" form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "add referee" form with invalid information (e.g. too many characters)
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-10.2 — Edit referee

#### Scenario: User edits referee successfully
* **Given** an owner fills in the "edit referee" form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "edit referee" form with invalid information
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-10.3 — Delete referee

#### Scenario: User deletes referee successfully
* **Given** an owner clicks the "delete referee" button
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner clicks the "delete referee" button
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation