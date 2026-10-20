# Feature: Display Leagues

**Feature ID:** 13
**Branch pattern:** `feature/13-display-leagues`
**Status:** Ready
**Created:** 2026-10-15
**Input:** Display leagues and access individual league information on a webpage.
**Depends on:** — [Feature 1 — Maintain Sports](feature-1-maintain-sports.md), [Feature 2 — Maintain Leagues](feature-2-maintain-leagues.md)

---

## User Stories

### US-13.1: View league
**As a** user
**I want to** be able to view all available leagues
**So that** I access individual leagues

**Priority:** P1
**Independent test:** View all leagues on the sports?{sport_id} page
**Acceptance scenarios:** see ### US-13.1 under Acceptance Criteria

### US-13.2: Access a league's information
**As a** user
**I want to** be able to access a league's information
**So that** I can stay informed about that league

**Priority:** P1
**Independent test:** Access a given league's information from the sports?{sport_id} page
**Acceptance scenarios:** see ### US-13.2 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST display leagues on the sports?{sport_id} page in card elements.
- **FR-002**: System MUST display all information for each league such that it is all visible to the user at the same time.

### Screen Requirements

- **SR-001**: Each league should have CRUD operations.
- **SR-002**: Add and Edit operations should each have one corresponding button which leads user to appropriate screen.
- **SR-003**: Delete button should open a confirmation dialog.

---

## Key Entities

- **League**: a league with sport and name.

---

## Data Model Requirements

### leagues

| Column | Notes |
|--------|-------|
| id | PK, int |
| sport_id | FK, int |
| name | nvarchar(100), required |

---

## Acceptance Criteria (Gherkin)

### US-13.1 — View league

#### Scenario: User views league successfully
* **Given** a user is on the website
* **When** the user goes to the sports?{sport_id} page
* **Then** the system displays the sports?{sport_id} page with each league and its information

#### Scenario: No leagues exist in database
* **Given** a user is on the website
* **When** the user goes to the sports?{sport_id} page
* **Then** the system displays the sports?{sport_id} page with a NoLeaguesExistException

### US-13.2 — Access a league's information

#### Scenario: User views league successfully
* **Given** the system displays the sports?{sport_id} page with each league and its information
* **When** the user attempts to access a given league's information
* **Then** the system displays the leagues?{league_id} page with corresponding information

#### Scenario: League does not have information
* **Given** the system displays the sports?{sport_id} page with each league and its information
* **When** the user attempts to access a given league's information
* **Then** the system displays the leagues?{league_id} page with a NoLeagueInformationException