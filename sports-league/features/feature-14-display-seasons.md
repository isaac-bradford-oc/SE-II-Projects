# Feature: Display Seasons

**Feature ID:** 14
**Branch pattern:** `feature/14-display-seasons`
**Status:** Ready
**Created:** 2026-10-15
**Input:** Display seasons and access individual season information on a webpage.
**Depends on:** — [Feature 1 — Maintain Sports](feature-1-maintain-sports.md), [Feature 2 — Maintain Leagues](feature-2-maintain-leagues.md), [Feature 3 — Maintain Seasons](feature-3-maintain-seasons.md)

---

## User Stories

### US-14.1: View season
**As a** user
**I want to** be able to view all available seasons
**So that** I access individual seasons

**Priority:** P1
**Independent test:** View all seasons on the leagues?{league_id} page
**Acceptance scenarios:** see ### US-14.1 under Acceptance Criteria

### US-14.2: Access a season's information
**As a** user
**I want to** be able to access a season's information
**So that** I can stay informed about that season

**Priority:** P1
**Independent test:** Access a given season's information from the leagues?{league_id} page
**Acceptance scenarios:** see ### US-14.2 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST display seasons on the leagues?{league_id} page in card elements.
- **FR-002**: System MUST display all information for each season such that it is all visible to the user at the same time.

---

## Key Entities

- **Season**: a season with league and name.

---

## Data Model Requirements

### seasons

| Column | Notes |
|--------|-------|
| id | PK, int |
| league_id | FK, int |
| year | nchar(4), required |

---

## Acceptance Criteria (Gherkin)

### US-14.1 — View season

#### Scenario: User views season successfully
* **Given** a user is on the website
* **When** the user goes to the leagues?{league_id} page
* **Then** the system displays the leagues?{league_id} page with each season and its information

#### Scenario: No seasons exist in database
* **Given** a user is on the website
* **When** the user goes to the leagues?{league_id} page
* **Then** the system displays the leagues?{league_id} page with a NoSeasonsExistException

### US-14.2 — Access a season's information

#### Scenario: User views season successfully
* **Given** the system displays the leagues?{league_id} page with each season and its information
* **When** the user attempts to access a given season's information
* **Then** the system displays the seasons?{season_id} page with corresponding information

#### Scenario: Season does not have information
* **Given** the system displays the leagues?{league_id} page with each season and its information
* **When** the user attempts to access a given season's information
* **Then** the system displays the seasons?{season_id} page with a NoSeasonInformationException