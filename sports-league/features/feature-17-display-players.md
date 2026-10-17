# Feature: Display Players

**Feature ID:** 17
**Branch pattern:** `feature/17-display-players`
**Status:** Ready
**Created:** 2026-10-15
**Input:** Display players and access individual player information on a webpage.
**Depends on:** — [Feature 7 — Maintain Players](feature-7-maintain-players.md)

---

## User Stories

### US-17.1: View player
**As a** user
**I want to** be able to view all available players
**So that** I access individual players

**Priority:** P1
**Independent test:** View all players on the teams?{team_id} page
**Acceptance scenarios:** see ### US-17.1 under Acceptance Criteria

### US-17.2: Access a player's information
**As a** user
**I want to** be able to access a player's information
**So that** I can stay informed about that player

**Priority:** P1
**Independent test:** Access a given player's information from the teams?{team_id} page
**Acceptance scenarios:** see ### US-17.2 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST display players on the teams?{team_id} page in card elements.
- **FR-002**: System MUST display all information for each player such that it is all visible to the user at the same time.

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

### US-17.1 — View player

#### Scenario: User views player successfully
* **Given** a user is on the website
* **When** the user goes to the teams?{team_id} page
* **Then** the system displays the teams?{team_id} page with each player and its information

#### Scenario: No players exist in database
* **Given** a user is on the website
* **When** the user goes to the teams?{team_id} page
* **Then** the system displays the teams?{team_id} page with a NoPlayersExistException

### US-17.2 — Access a player's information

#### Scenario: User views player successfully
* **Given** the system displays the teams?{team_id} page with each player and its information
* **When** the user attempts to access a given player's information
* **Then** the system displays the players?{player_id} page with corresponding information

#### Scenario: Player does not have information
* **Given** the system displays the teams?{team_id} page with each player and its information
* **When** the user attempts to access a given player's information
* **Then** the system displays the players?{player_id} page with a NoPlayerInformationException