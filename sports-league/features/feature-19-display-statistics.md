# Feature: Display Statistics

**Feature ID:** 19
**Branch pattern:** `feature/19-display-statistics`
**Status:** Ready
**Created:** 2026-10-15
**Input:** Keep current list of statistics updated.
**Depends on:** — [Feature 1 — Maintain Sports](feature-1-maintain-sports.md), [Feature 2 — Maintain Leagues](feature-2-maintain-leagues.md), [Feature 3 — Maintain Seasons](feature-3-maintain-seasons.md), [Feature 4 — Maintain Games](feature-4-maintain-games.md), [Feature 5 — Maintain Teams](feature-5-maintain-teams.md), [Feature 8 — Maintain Locations](feature-8-maintain-locations.md)

---

## User Stories

### US-19.1: View game statistic
**As a** user
**I want to** be able to view all available game statistics
**So that** I access individual game statistics

**Priority:** P1
**Independent test:** View all game statistics on the games?{game_id} page
**Acceptance scenarios:** see ### US-19.1 under Acceptance Criteria

### US-19.2: View player statistic
**As a** user
**I want to** be able to view all available player statistics
**So that** I access individual player statistics

**Priority:** P1
**Independent test:** View all player statistics on the players?{player_id} page
**Acceptance scenarios:** see ### US-19.2 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST display game statistics on the games?{game_id} page in card elements.
- **FR-002**: System MUST display player statistics on the players?{player_id} page in card elements.
- **FR-003**: System MUST display all information for each statistic such that it is all visible to the user at the same time.

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

### US-19.1 — View game statistic

#### Scenario: User views game statistic successfully
* **Given** a user is on the website
* **When** the user goes to the games?{game_id} page
* **Then** the system displays the games?{game_id} page with each game statistic and its information

#### Scenario: No game statistics exist in database
* **Given** a user is on the website
* **When** the user goes to the games?{game_id} page
* **Then** the system displays the games?{game_id} page with a NoGameStatisticsExistException

### US-19.2 — View player statistic

#### Scenario: User views player statistic successfully
* **Given** a user is on the website
* **When** the user goes to the players?{player_id} page
* **Then** the system displays the players?{player_id} page with each player statistic and its information

#### Scenario: No player statistics exist in database
* **Given** a user is on the website
* **When** the user goes to the players?{player_id} page
* **Then** the system displays the players?{player_id} page with a NoPlayerStatisticsExistException