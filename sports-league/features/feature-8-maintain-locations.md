# Feature: Maintain Locations

**Feature ID:** 8
**Branch pattern:** `feature/8-maintain-locations`
**Status:** Ready
**Created:** 2026-10-11
**Input:** Keep current list of locations updated.
**Depends on:** — 

---

## User Stories

### US-8.1: Add location
**As a** owner
**I want to** add a location to the database
**So that** the table of locations remains up-to-date

**Priority:** P1
**Independent test:** Add a location to the database and view it in a database table
**Acceptance scenarios:** see ### US-8.1 under Acceptance Criteria

### US-8.2: Edit location
**As a** owner
**I want to** edit a location in the database
**So that** location information remains up-to-date

**Priority:** P1
**Independent test:** Edit a location in the database and view it in a database table
**Acceptance scenarios:** see ### US-8.2 under Acceptance Criteria

### US-8.3: Delete location
**As a** owner
**I want to** delete a location from the database
**So that** the table of locations remains up-to-date

**Priority:** P1
**Independent test:** Remove a location from the database and see that it is not in a database table
**Acceptance scenarios:** see ### US-8.3 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST allow owners to manage individual locations.
- **FR-002**: System MUST validate user form input before saving to database.
- **FR-003**: System MUST provide the user with visual confirmation of action taken after attempting to save input.

---

## Key Entities

- **Location**: a location with name and address.

---

## Data Model Requirements

### locations

| Column | Notes |
|--------|-------|
| id | PK, int |
| name | nvarchar(100), required |
| address | nvarchar(255), required |

---

## Acceptance Criteria (Gherkin)

### US-8.1 — Add location

#### Scenario: User adds location successfully
* **Given** an owner fills in the "add location" form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "add location" form with invalid information (e.g. too many characters)
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-8.2 — Edit location

#### Scenario: User edits location successfully
* **Given** an owner fills in the "edit location" form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "edit location" form with invalid information
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-8.3 — Delete location

#### Scenario: User deletes location successfully
* **Given** an owner clicks the "delete location" button
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner clicks the "delete location" button
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation