# Feature: Email Players

**Feature ID:** 22
**Branch pattern:** `feature/22-email-players`
**Status:** Ready
**Created:** 2026-10-17
**Input:** Email players to notify them of schedule changes and other updates.
**Depends on:** — [Feature 7 — Maintain Players](feature-7-maintain-players.md)

---

## User Stories

### US-22.1: Email player
**As a** owner
**I want to** email player(s)
**So that** players are in the loop on relevant updates

**Priority:** P1
**Independent test:** Email player(s) and verify that email(s) were sent to the corresponding addresses
**Acceptance scenarios:** see ### US-22.1 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST allow owners to email all players or a subset of players.
- **FR-002**: System MUST optionally allow owners to filter the player subset based on sport, league, or team.
- **FR-003**: System MUST validate email recipients before sending email.
- **FR-004**: System MUST provide the user with visual confirmation of action taken after attempting to send email.

### Screen Requirements

- **SR-001**: Screen should have multi-select dropdowns for selecting players, sports, leagues, and/or teams, subject and body text fields, and a send button.

---

## Key Entities

- **player**: a player with name, jersey number, email, sports, positions, seasons, and teams.

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

### US-22.1 — Email player

#### Scenario: User emails player(s) successfully
* **Given** an owner fills in the "email player" form with acceptable information
* **When** the user submits the form
* **Then** the system emails player(s)
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an owner fills in the "email player" form with invalid information (e.g. too many characters)
* **When** the user submits the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation
