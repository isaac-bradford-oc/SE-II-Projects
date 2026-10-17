# Feature: Maintain Players

**Feature ID:** 7
**Branch pattern:** `feature/7-maintain-players`
**Status:** Ready
**Created:** 2026-10-11
**Input:** Keep current list of players' information updated.
**Depends on:** — 

---

## User Stories

### US-7.1: Add player
**As a** manager
**I want to** add a player to the database
**So that** the table of players remains up-to-date

**Priority:** P1
**Independent test:** Add a player to the database and view it in a database table
**Acceptance scenarios:** see ### US-7.1 under Acceptance Criteria

### US-7.2: Edit player
**As a** manager
**I want to** edit a player in the database
**So that** player information remains up-to-date

**Priority:** P1
**Independent test:** Edit a player in the database and view it in a database table
**Acceptance scenarios:** see ### US-7.2 under Acceptance Criteria

### US-7.3: Delete player
**As a** manager
**I want to** delete a player from the database
**So that** the table of players remains up-to-date

**Priority:** P1
**Independent test:** Remove a player from the database and see that it is not in a database table
**Acceptance scenarios:** see ### US-7.3 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST allow managers to manage individual players.
- **FR-002**: System MUST validate user form input before saving to database.
- **FR-003**: System MUST provide the user with visual confirmation of action taken after attempting to save input.

---

## Key Entities

- **Player**: a player with name, jersey number, email, sports, positions, seasons, and teams.

---

## Data Model Requirements

### players

| Column | Notes |
|--------|-------|
| id | PK, int |
| name | nvarchar(100), required |
| jersey_number | nchar(2), required |
| email | nvarchar(254), required |

### player_positions

| Column | Notes |
|--------|-------|
| id | PK, int |
| player_id | FK, int |
| sport_id | FK, int |
| position_id | FK, int |

### rosters

| Column | Notes |
|--------|-------|
| id | PK, int |
| season_id | FK, int |
| team_id | FK, int |
| player_id | FK, int |

---

## Acceptance Criteria (Gherkin)

### US-7.1 — Add player

#### Scenario: User adds player successfully
* **Given** an manager fills in the "add player" form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an manager fills in the "add player" form with invalid information (e.g. too many characters)
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-7.2 — Edit player

#### Scenario: User edits player successfully
* **Given** an manager fills in the "edit player" form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an manager fills in the "edit player" form with invalid information
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-7.3 — Delete player

#### Scenario: User deletes player successfully
* **Given** an manager clicks the "delete player" button
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an manager clicks the "delete player" button
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation