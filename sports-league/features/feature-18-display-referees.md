# Feature: Display Referees

**Feature ID:** 18
**Branch pattern:** `feature/18-display-referees`
**Status:** Ready
**Created:** 2026-10-15
**Input:** Display referees and access individual referee information on a webpage.
**Depends on:** — [Feature 10 — Maintain Referees](feature-10-maintain-referees.md)

---

## User Stories

### US-18.1: View referee
**As a** user
**I want to** be able to view all available referees
**So that** I access individual referees

**Priority:** P1
**Independent test:** View all referees on the games?{game_id} page
**Acceptance scenarios:** see ### US-18.1 under Acceptance Criteria

### US-18.2: Access a referee's information
**As a** user
**I want to** be able to access a referee's information
**So that** I can stay informed about that referee

**Priority:** P1
**Independent test:** Access a given referee's information from the games?{game_id} page
**Acceptance scenarios:** see ### US-18.2 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST display referees on the games?{game_id} page in card elements.
- **FR-002**: System MUST display all information for each referee such that it is all visible to the user at the same time.

### Screen Requirements

- **SR-001**: Each referee should have CRUD operations.
- **SR-002**: Add and Edit operations should each have one corresponding button which leads user to appropriate screen.
- **SR-003**: Delete button should open a confirmation dialog.

---

## Key Entities

- **Referee**: a referee with name, email, sports, and positions.

---

## Data Model Requirements

### referees

| Column | Notes |
|--------|-------|
| id | PK, int |
| name | nvarchar(100), required |
| email | nvarchar(254), required |

### referee_positions

| Column | Notes |
|--------|-------|
| id | PK, int |
| referee_id | FK, int |
| sport_id | FK, int |
| position_id | FK, int |

---

## Acceptance Criteria (Gherkin)

### US-18.1 — View referee

#### Scenario: User views referee successfully
* **Given** a user is on the website
* **When** the user goes to the games?{game_id} page
* **Then** the system displays the games?{game_id} page with each referee and its information

#### Scenario: No referees exist in database
* **Given** a user is on the website
* **When** the user goes to the games?{game_id} page
* **Then** the system displays the games?{game_id} page with a NoRefereesExistException

### US-18.2 — Access a referee's information

#### Scenario: User views referee successfully
* **Given** the system displays the games?{game_id} page with each referee and its information
* **When** the user attempts to access a given referee's information
* **Then** the system displays the referees?{referee_id} page with corresponding information

#### Scenario: Referee does not have information
* **Given** the system displays the games?{game_id} page with each referee and its information
* **When** the user attempts to access a given referee's information
* **Then** the system displays the referees?{referee_id} page with a NoRefereeInformationException