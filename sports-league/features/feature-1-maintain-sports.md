# Feature: Maintain Sports

**Feature ID:** 1
**Branch pattern:** `feature/1-maintain-sports`
**Status:** Ready
**Created:** 2026-10-11
**Input:** Keep current list of sports updated.
**Depends on:** — 

---

## User Stories

### US-1.1: Add sport
**As a** owner
**I want to** add a sport to the database
**So that** the table of sports remains up-to-date

**Priority:** P1
**Independent test:** Add a sport to the database and view it in a database table
**Acceptance scenarios:** see ### US-1.1 under Acceptance Criteria

### US-1.2: Edit sport
**As a** owner
**I want to** edit a sport in the database
**So that** sport information remains up-to-date

**Priority:** P1
**Independent test:** Edit a sport in the database and view it in a database table
**Acceptance scenarios:** see ### US-1.2 under Acceptance Criteria

### US-1.3: Delete sport
**As a** owner
**I want to** delete a sport from the database
**So that** the table of sports remains up-to-date

**Priority:** P1
**Independent test:** Remove a sport from the database and see that it is not in a database table
**Acceptance scenarios:** see ### US-1.3 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST allow owners to manage individual sports.
- **FR-002**: System MUST validate user form input before saving to database.
- **FR-003**: System MUST provide the user with visual confirmation of action taken after attempting to save input.

---

## Key Entities

- **Sport**: a sport with name.

---

## Data Model Requirements

### sports

| Column | Notes |
|--------|-------|
| id | PK |
| name | nvarchar(100), unique, required |

---

## Acceptance Criteria (Gherkin)

### US-1.1 — Add sport

#### Scenario: User adds sport successfully
* **Given** an owner fills in the "add sport" form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "add sport" form with invalid information (e.g. too many characters)
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-1.2 — Edit sport

#### Scenario: User edits sport successfully
* **Given** an owner fills in the "edit sport" form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "edit sport" form with invalid information
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-1.3 — Delete sport

#### Scenario: User deletes sport successfully
* **Given** an owner clicks the "delete sport" button
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner clicks the "delete sport" button
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation