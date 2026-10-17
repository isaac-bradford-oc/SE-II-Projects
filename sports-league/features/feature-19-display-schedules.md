# Feature: Display Schedules

**Feature ID:** 19
**Branch pattern:** `feature/19-display-schedules`
**Status:** Ready
**Created:** 2026-10-15
**Input:** Display schedules and access individual schedule information on a webpage.
**Depends on:** — [Feature 1 — Maintain Sports](feature-1-maintain-sports.md), [Feature 2 — Maintain Leagues](feature-2-maintain-leagues.md), [Feature 3 — Maintain Seasons](feature-3-maintain-seasons.md), [Feature 4 — Maintain Games](feature-4-maintain-games.md), [Feature 5 — Maintain Teams](feature-5-maintain-teams.md), [Feature 9 — Maintain Locations](feature-9-maintain-locations.md)

---

## User Stories

### US-19.1: View season's schedule
**As a** user
**I want to** be able to view a given season's schedule
**So that** I access a season schedule

**Priority:** P1
**Independent test:** View season schedule on the seasons?{season_id} page
**Acceptance scenarios:** see ### US-19.1 under Acceptance Criteria

### US-19.2: Access a season's schedule information
**As a** user
**I want to** be able to access a season's schedule information
**So that** I can stay informed about that season's schedule

**Priority:** P1
**Independent test:** Access a given season schedule's information from the seasons?{season_id} page
**Acceptance scenarios:** see ### US-19.2 under Acceptance Criteria

### US-19.3: View team's schedule
**As a** user
**I want to** be able to a view a given team's schedule for the current season
**So that** I access a team's schedule

**Priority:** P1
**Independent test:** View team schedule on the teams?{team_id} page
**Acceptance scenarios:** see ### US-19.3 under Acceptance Criteria

### US-19.4: Access a team's schedule information
**As a** user
**I want to** be able to access a team's schedule information
**So that** I can stay informed about that team's schedule

**Priority:** P1
**Independent test:** Access a given team schedule's information from the teams?{team_id} page
**Acceptance scenarios:** see ### US-19.4 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST display season schedules on the seasons?{season_id} page in card elements.
- **FR-002**: System MUST display team schedules on the teams?{team_id} page in card elements.
- **FR-003**: System MUST display all information for each schedule such that it is all visible to the user at the same time.

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

### US-19.1 — View season's schedule

#### Scenario: User views season's schedule successfully
* **Given** a user is on the website
* **When** the user goes to the seasons?{season_id} page
* **Then** the system displays the seasons?{season_id} page with the season schedule and its information

#### Scenario: No season schedules exist in database
* **Given** a user is on the website
* **When** the user goes to the seasons?{season_id} page
* **Then** the system displays the seasons?{season_id} page with a NoSeasonSchedulesExistException

### US-19.2 — Access a season's schedule information

#### Scenario: User views season's schedule successfully
* **Given** the system displays the seasons?{season_id} page with each season schedule and its information
* **When** the user attempts to access a given season's schedule information
* **Then** the system displays the schedules?{schedule_id} page with corresponding information

#### Scenario: Season's schedule does not have information
* **Given** the system displays the seasons?{season_id} page with each season schedule and its information
* **When** the user attempts to access a given season's schedule information
* **Then** the system displays the schedules?{schedule_id} page with a NoSeasonScheduleInformationException

### US-19.3 — View team's schedule

#### Scenario: User views team's schedule successfully
* **Given** a user is on the website
* **When** the user goes to the teams?{team_id} page
* **Then** the system displays the teams?{team_id} page with the team schedule and its information

#### Scenario: No team schedules exist in database
* **Given** a user is on the website
* **When** the user goes to the teams?{team_id} page
* **Then** the system displays the teams?{team_id} page with a NoTeamSchedulesExistException

### US-19.4 — Access a team's schedule information

#### Scenario: User views team's schedule successfully
* **Given** the system displays the teams?{team_id} page with each team schedule and its information
* **When** the user attempts to access a given team's schedule information
* **Then** the system displays the schedules?{schedule_id} page with corresponding information

#### Scenario: Team's schedule does not have information
* **Given** the system displays the teams?{team_id} page with each team schedule and its information
* **When** the user attempts to access a given team's schedule information
* **Then** the system displays the schedules?{schedule_id} page with a NoTeamScheduleInformationException