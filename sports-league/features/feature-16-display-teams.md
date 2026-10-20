# Feature: Display Teams

**Feature ID:** 16
**Branch pattern:** `feature/16-display-teams`
**Status:** Ready
**Created:** 2026-10-15
**Input:** Display teams and access individual team information on a webpage.
**Depends on:** — [Feature 5 — Maintain Teams](feature-5-maintain-teams.md)

---

## User Stories

### US-16.1: View team on leagues page
**As a** user
**I want to** be able to view all available teams
**So that** I access individual teams

**Priority:** P1
**Independent test:** View all teams on the leagues?{league_id} page
**Acceptance scenarios:** see ### US-16.1 under Acceptance Criteria

### US-16.2: View team on seasons page
**As a** user
**I want to** be able to view all available teams
**So that** I access individual teams

**Priority:** P1
**Independent test:** View all teams on the seasons?{season_id} page
**Acceptance scenarios:** see ### US-16.2 under Acceptance Criteria

### US-16.3: View team on games page
**As a** user
**I want to** be able to view all available teams
**So that** I access individual teams

**Priority:** P1
**Independent test:** View all teams on the games?{game_id} page
**Acceptance scenarios:** see ### US-16.3 under Acceptance Criteria

### US-16.4: Access a team's information
**As a** user
**I want to** be able to access a team's information
**So that** I can stay informed about that team

**Priority:** P1
**Independent test:** Access a given team's information from the leagues?{league_id}, seasons?{season_id}, or games?{game_id} page
**Acceptance scenarios:** see ### US-16.4 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST display teams on the leagues, seasons, and games pages in card elements.
- **FR-002**: System MUST display all information for each team such that it is all visible to the user at the same time.

### Screen Requirements

- **SR-001**: Each team should have CRUD operations.
- **SR-002**: Add and Edit operations should each have one corresponding button which leads user to appropriate screen.
- **SR-003**: Delete button should open a confirmation dialog.

---

## Key Entities

- **Team**: a team with name and seasons.

---

## Data Model Requirements

### teams

| Column | Notes |
|--------|-------|
| id | PK, int |
| name | nvarchar(100), required |

### season_teams

| Column | Notes |
|--------|-------|
| id | PK, int |
| season_id | FK, int |
| team_id | FK, int |

---

## Acceptance Criteria (Gherkin)

### US-16.1 — View team on leagues page

#### Scenario: User views team successfully
* **Given** a user is on the website
* **When** the user goes to the leagues?{league_id} page
* **Then** the system displays the leagues?{league_id} page with each team and its information

#### Scenario: No teams exist in database
* **Given** a user is on the website
* **When** the user goes to the leagues?{league_id} page
* **Then** the system displays the leagues?{league_id} page with a NoTeamsExistException

### US-16.2 — View team on seasons page

#### Scenario: User views team successfully
* **Given** a user is on the website
* **When** the user goes to the seasons?{season_id} page
* **Then** the system displays the seasons?{season_id} page with each team and its information

#### Scenario: No teams exist in database
* **Given** a user is on the website
* **When** the user goes to the seasons?{season_id} page
* **Then** the system displays the seasons?{season_id} page with a NoTeamsExistException

### US-16.3 — View team on games page

#### Scenario: User views team successfully
* **Given** a user is on the website
* **When** the user goes to the games?{game_id} page
* **Then** the system displays the games?{game_id} page with each team and its information

#### Scenario: No teams exist in database
* **Given** a user is on the website
* **When** the user goes to the games?{game_id} page
* **Then** the system displays the games?{game_id} page with a NoTeamsExistException

### US-16.4 — Access a team's information

#### Scenario: User views team successfully
* **Given** the system displays the leagues?{league_id}, seasons?{season_id}, or games?{game_id} page with each team and its information
* **When** the user attempts to access a given team's information
* **Then** the system displays the teams?{team_id} page with corresponding information

#### Scenario: Team does not have information
* **Given** the system displays the leagues?{league_id}, seasons?{season_id}, or games?{game_id} page with each team and its information
* **When** the user attempts to access a given team's information
* **Then** the system displays the teams?{team_id} page with a NoTeamInformationException