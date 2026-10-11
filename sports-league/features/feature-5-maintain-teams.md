# Feature: Maintain Teams

**Feature ID:** 5
**Branch pattern:** `feature/5-maintain-teams`
**Status:** Ready
**Created:** 2026-10-11
**Input:** Keep current list of teams' information updated.
**Depends on:** — 

---

## User Stories

### US-5.1: Add team
**As a** owner
**I want to** add a team to the database
**So that** the table of teams remains up-to-date

**Priority:** P1
**Independent test:** Add a team to the database and view it in a database table
**Acceptance scenarios:** see ### US-5.1 under Acceptance Criteria

### US-5.2: Edit team
**As a** owner
**I want to** edit a team in the database
**So that** team information remains up-to-date

**Priority:** P1
**Independent test:** Edit a team in the database and view it in a database table
**Acceptance scenarios:** see ### US-5.2 under Acceptance Criteria

### US-5.3: Delete team
**As a** owner
**I want to** delete a team from the database
**So that** the table of teams remains up-to-date

**Priority:** P1
**Independent test:** Remove a team from the database and see that it is not in a database table
**Acceptance scenarios:** see ### US-5.3 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST allow owners to manage individual teams.
- **FR-002**: System MUST validate user form input before saving to database.
- **FR-003**: System MUST provide the user with visual confirmation of action taken after attempting to save input.

---

## Key Entities

- **Team**: a team with name and seasons.

---

## Data Model Requirements

### teams

| Column | Notes |
|--------|-------|
| id | PK, int |
| name | nvarchar(100), required |

### season_teams

| Column | Notes |
|--------|-------|
| id | PK, int |
| season_id | FK, int |
| team_id | FK, int |

---

## Acceptance Criteria (Gherkin)

### US-5.1 — Add team

#### Scenario: User adds team successfully
* **Given** an owner fills in the "add team" form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "add team" form with invalid information (e.g. too many characters)
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-5.2 — Edit team

#### Scenario: User edits team successfully
* **Given** an owner fills in the "edit team" form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "edit team" form with invalid information
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-5.3 — Delete team

#### Scenario: User deletes team successfully
* **Given** an owner clicks the "delete team" button
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner clicks the "delete team" button
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation