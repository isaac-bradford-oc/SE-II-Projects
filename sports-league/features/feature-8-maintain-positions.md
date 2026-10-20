# Feature: Maintain Positions

**Feature ID:** 8
**Branch pattern:** `feature/8-maintain-positions`
**Status:** Ready
**Created:** 2026-10-11
**Input:** Keep current list of positions updated.
**Depends on:** — [Feature 1 — Maintain Sports](feature-1-maintain-sports.md)

---

## User Stories

### US-8.1: Add position
**As a** owner
**I want to** add a position to the database
**So that** the table of positions remains up-to-date

**Priority:** P1
**Independent test:** Add a position to the database and view it in a database table
**Acceptance scenarios:** see ### US-8.1 under Acceptance Criteria

### US-8.2: Edit position
**As a** owner
**I want to** edit a position in the database
**So that** position information remains up-to-date

**Priority:** P1
**Independent test:** Edit a position in the database and view it in a database table
**Acceptance scenarios:** see ### US-8.2 under Acceptance Criteria

### US-8.3: Delete position
**As a** owner
**I want to** delete a position from the database
**So that** the table of positions remains up-to-date

**Priority:** P1
**Independent test:** Remove a position from the database and see that it is not in a database table
**Acceptance scenarios:** see ### US-8.3 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST allow owners to manage individual positions.
- **FR-002**: System MUST validate user form input before saving to database.
- **FR-003**: System MUST provide the user with visual confirmation of action taken after attempting to save input.

### Screen Requirements

- **SR-001**: Add and Edit operations should each have one corresponding screen.
- **SR-002**: Add screen should have input fields for all required database columns, a create button, and cancel button.
- **SR-003**: Edit screen should have input fields for all required database columns, a save button, and cancel button.

---

## Key Entities

- **Position**: a position with sport, name, and abbreviation.

---

## Data Model Requirements

### positions

| Column | Notes |
|--------|-------|
| id | PK, int |
| sport_id | FK, int |
| name | nvarchar(100), required |
| abbreviation | char(3), required |

---

## Acceptance Criteria (Gherkin)

### US-8.1 — Add position

#### Scenario: User adds position successfully
* **Given** an owner fills in the "add position" form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "add position" form with invalid information (e.g. too many characters)
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-8.2 — Edit position

#### Scenario: User edits position successfully
* **Given** an owner fills in the "edit position" form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "edit position" form with invalid information
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-8.3 — Delete position

#### Scenario: User deletes position successfully
* **Given** an owner clicks the "delete position" button
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner clicks the "delete position" button
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation