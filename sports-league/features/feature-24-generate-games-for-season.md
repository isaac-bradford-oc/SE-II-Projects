# Feature: Generate Games For Season

**Feature ID:** 24
**Branch pattern:** `feature/24-generate-games-for-season`
**Status:** Ready
**Created:** 2026-10-17
**Input:** Generate a season schedule based off of owner-selected days of the week.
**Depends on:** — [Feature 1 — Maintain Sports](feature-1-maintain-sports.md), [Feature 2 — Maintain Leagues](feature-2-maintain-leagues.md), [Feature 3 — Maintain Seasons](feature-3-maintain-seasons.md), [Feature 4 — Maintain Games](feature-4-maintain-games.md), [Feature 5 — Maintain Teams](feature-5-maintain-teams.md), [Feature 9 — Maintain Locations](feature-9-maintain-locations.md)

---

## User Stories

### US-24.1: Generate games for season
**As a** owner
**I want to** be able to select start and end dates, the days of the week games will be played, and to generate a season schedule that aligns with those date restraints
**So that** I don't have to manually create season schedules

**Priority:** P1
**Independent test:** Generate schedule and view all generated games on the seasons?{season_id} page
**Acceptance scenarios:** see ### US-24.1 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST generate (n_teams-1)*2 games for every schedule.
- **FR-002**: System MUST display either a confirmation of schedule creation or an error to user

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

### US-24.1 — Generate games for season

#### Scenario: System successfully generates games for a season
* **Given** a user has entered start and end dates and days of the week for games to be played
* **When** the user submits the form
* **Then** the system generates (n_teams-1)*2 games and saves them to the database

#### Scenario: User enters invalid start or end dates
* **Given** a user has entered start and end dates which are out of bounds
* **When** the user submits the form
* **Then** the system throws an error
* **And** the system displays error to user