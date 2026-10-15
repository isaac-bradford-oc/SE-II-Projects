# Feature: Display Games

**Feature ID:** 14
**Branch pattern:** `feature/14-display-games`
**Status:** Ready
**Created:** 2026-10-15
**Input:** Keep current list of games updated.
**Depends on:** — [Feature 1 — Maintain Sports](feature-1-maintain-sports.md), [Feature 2 — Maintain Leagues](feature-2-maintain-leagues.md), [Feature 3 — Maintain Seasons](feature-3-maintain-seasons.md), [Feature 4 — Maintain Games](feature-4-maintain-games.md), [Feature 5 — Maintain Teams](feature-5-maintain-teams.md), [Feature 8 — Maintain Locations](feature-8-maintain-locations.md)

---

## User Stories

### US-14.1: View game
**As a** user
**I want to** be able to view all available games
**So that** I access individual games

**Priority:** P1
**Independent test:** View all games on the seasons?{season_id} page
**Acceptance scenarios:** see ### US-14.1 under Acceptance Criteria

### US-14.2: Access a game's information
**As a** user
**I want to** be able to access a game's information
**So that** I can stay informed about that game

**Priority:** P1
**Independent test:** Access a given game's information from the seasons?{season_id} page
**Acceptance scenarios:** see ### US-14.2 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST display games on the seasons?{season_id} page in card elements.
- **FR-002**: System MUST display all information for each game such that it is all visible to the user at the same time.

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

### US-14.1 — View game

#### Scenario: User views game successfully
* **Given** a user is on the website
* **When** the user goes to the seasons?{season_id} page
* **Then** the system displays the seasons?{season_id} page with each game and its information

#### Scenario: No games exist in database
* **Given** a user is on the website
* **When** the user goes to the seasons?{season_id} page
* **Then** the system displays the seasons?{season_id} page with a NoGamesExistException

### US-14.2 — Access a game's information

#### Scenario: User views game successfully
* **Given** the system displays the seasons?{season_id} page with each game and its information
* **When** the user attempts to access a given game's information
* **Then** the system displays the games?{game_id} page with corresponding information

#### Scenario: Game does not have information
* **Given** the system displays the seasons?{season_id} page with each game and its information
* **When** the user attempts to access a given game's information
* **Then** the system displays the games?{game_id} page with a NoGameInformationException