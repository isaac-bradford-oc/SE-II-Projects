# Feature: Maintain Seasons

**Feature ID:** 3
**Branch pattern:** `feature/3-maintain-seasons`
**Status:** Ready
**Created:** 2026-10-11
**Input:** Keep current list of seasons' information updated.
**Depends on:** — [Feature 1 — Maintain Sports](feature-1-maintain-sports.md), [Feature 2 — Maintain Leagues](feature-2-maintain-leagues.md)

---

## User Stories

### US-3.1: Add season
**As a** owner
**I want to** add a season to the database
**So that** the table of seasons remains up-to-date

**Priority:** P1
**Independent test:** Add a season to the database and view it in a database table
**Acceptance scenarios:** see ### US-3.1 under Acceptance Criteria

### US-3.2: Edit season
**As a** owner
**I want to** edit a season in the database
**So that** season information remains up-to-date

**Priority:** P1
**Independent test:** Edit a season in the database and view it in a database table
**Acceptance scenarios:** see ### US-3.2 under Acceptance Criteria

### US-3.3: Delete season
**As a** owner
**I want to** delete a season from the database
**So that** the table of seasons remains up-to-date

**Priority:** P1
**Independent test:** Remove a season from the database and see that it is not in a database table
**Acceptance scenarios:** see ### US-3.3 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST allow owners to manage individual seasons.
- **FR-002**: System MUST validate user form input before saving to database.
- **FR-003**: System MUST provide the user with visual confirmation of action taken after attempting to save input.

---

## Key Entities

- **Season**: a season with league and name.

---

## Data Model Requirements

### seasons

| Column | Notes |
|--------|-------|
| id | PK, int |
| league_id | FK, int |
| year | nchar(4), required |

---

## Acceptance Criteria (Gherkin)

### US-3.1 — Add season

#### Scenario: User adds season successfully
* **Given** an owner fills in the "add season" form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "add season" form with invalid information (e.g. too many characters)
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-3.2 — Edit season

#### Scenario: User edits season successfully
* **Given** an owner fills in the "edit season" form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "edit season" form with invalid information
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-3.3 — Delete season

#### Scenario: User deletes season successfully
* **Given** an owner clicks the "delete season" button
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner clicks the "delete season" button
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation