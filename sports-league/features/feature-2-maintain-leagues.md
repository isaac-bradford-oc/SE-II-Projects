# Feature: Maintain Leagues

**Feature ID:** 2
**Branch pattern:** `feature/2-maintain-leagues`
**Status:** Ready
**Created:** 2026-10-11
**Input:** Keep current list of leagues' information updated.
**Depends on:** — [Feature 1 — Maintain Sports](feature-1-maintain-sports.md)

---

## User Stories

### US-2.1: Add league
**As a** owner
**I want to** add a league to the database
**So that** the table of leagues remains up-to-date

**Priority:** P1
**Independent test:** Add a league to the database and view it in a database table
**Acceptance scenarios:** see ### US-2.1 under Acceptance Criteria

### US-2.2: Edit league
**As a** owner
**I want to** edit a league in the database
**So that** league information remains up-to-date

**Priority:** P1
**Independent test:** Edit a league in the database and view it in a database table
**Acceptance scenarios:** see ### US-2.2 under Acceptance Criteria

### US-2.3: Delete league
**As a** owner
**I want to** delete a league from the database
**So that** the table of leagues remains up-to-date

**Priority:** P1
**Independent test:** Remove a league from the database and see that it is not in a database table
**Acceptance scenarios:** see ### US-2.3 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST allow owners to manage individual leagues.
- **FR-002**: System MUST validate user form input before saving to database.
- **FR-003**: System MUST provide the user with visual confirmation of action taken after attempting to save input.

---

## Key Entities

- **League**: a league with sport and name.

---

## Data Model Requirements

### leagues

| Column | Notes |
|--------|-------|
| id | PK, int |
| sport_id | FK, int |
| name | nvarchar(100), required |

---

## Acceptance Criteria (Gherkin)

### US-2.1 — Add league

#### Scenario: User adds league successfully
* **Given** an owner fills in the "add league" form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "add league" form with invalid information (e.g. too many characters)
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-2.2 — Edit league

#### Scenario: User edits league successfully
* **Given** an owner fills in the "edit league" form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "edit league" form with invalid information
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-2.3 — Delete league

#### Scenario: User deletes league successfully
* **Given** an owner clicks the "delete league" button
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner clicks the "delete league" button
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation