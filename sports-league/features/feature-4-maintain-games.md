# Feature: Maintain Games

**Feature ID:** 4
**Branch pattern:** `feature/4-maintain-games`
**Status:** Ready
**Created:** 2026-10-11
**Input:** Keep current list of games' information updated.
**Depends on:** — [Feature 1 — Maintain Sports](feature-1-maintain-sports.md), [Feature 2 — Maintain Leagues](feature-2-maintain-leagues.md), [Feature 3 — Maintain Seasons](feature-3-maintain-seasons.md), [Feature 5 — Maintain Teams](feature-5-maintain-teams.md), [Feature 8 — Maintain Locations](feature-8-maintain-locations.md)

---

## User Stories

### US-4.1: Add game
**As a** owner
**I want to** add a game to the database
**So that** the table of games remains up-to-date

**Priority:** P1
**Independent test:** Add a game to the database and view it in a database table
**Acceptance scenarios:** see ### US-4.1 under Acceptance Criteria

### US-4.2: Edit game
**As a** owner
**I want to** edit a game in the database
**So that** game information remains up-to-date

**Priority:** P1
**Independent test:** Edit a game in the database and view it in a database table
**Acceptance scenarios:** see ### US-4.2 under Acceptance Criteria

### US-4.3: Delete game
**As a** owner
**I want to** delete a game from the database
**So that** the table of games remains up-to-date

**Priority:** P1
**Independent test:** Remove a game from the database and see that it is not in a database table
**Acceptance scenarios:** see ### US-4.3 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST allow owners to manage individual games.
- **FR-002**: System MUST validate user form input before saving to database.
- **FR-003**: System MUST provide the user with visual confirmation of action taken after attempting to save input.

---

## Key Entities

- **Game**: a game with season, location, home team, away team and datetime.

---

## Data Model Requirements

### games

| Column | Notes |
|--------|-------|
| id | PK, int |
| season_id | FK, int |
| location_id | FK, int |
| home_team_id | FK, int |
| away_team_id | FK, int |
| date_time | datetime |

---

## Acceptance Criteria (Gherkin)

### US-4.1 — Add game

#### Scenario: User adds game successfully
* **Given** an owner fills in the "add game" form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "add game" form with invalid information (e.g. too many characters)
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-4.2 — Edit game

#### Scenario: User edits game successfully
* **Given** an owner fills in the "edit game" form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "edit game" form with invalid information
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-4.3 — Delete game

#### Scenario: User deletes game successfully
* **Given** an owner clicks the "delete game" button
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner clicks the "delete game" button
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation