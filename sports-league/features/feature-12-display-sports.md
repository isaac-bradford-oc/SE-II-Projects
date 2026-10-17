# Feature: Display Sports

**Feature ID:** 12
**Branch pattern:** `feature/12-display-sports`
**Status:** Ready
**Created:** 2026-10-15
**Input:** Display sports and access individual sport information on a webpage.
**Depends on:** — [Feature 1 — Maintain Sports](feature-1-maintain-sports.md)

---

## User Stories

### US-12.1: View sport
**As a** user
**I want to** be able to view all available sports
**So that** I access individual sports

**Priority:** P1
**Independent test:** View all sports on the home page
**Acceptance scenarios:** see ### US-12.1 under Acceptance Criteria

### US-12.2: Access a sport's information
**As a** user
**I want to** be able to access a sport's information
**So that** I can stay informed about that sport

**Priority:** P1
**Independent test:** Access a given sport's information from the home page
**Acceptance scenarios:** see ### US-12.2 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST display sports on the sports page in card elements.
- **FR-002**: System MUST display all information for each sport such that it is all visible to the user at the same time.

---

## Key Entities

- **Sport**: a sport with name.

---

## Data Model Requirements

### sports

| Column | Notes |
|--------|-------|
| id | PK |
| name | nvarchar(100), unique, required |

---

## Acceptance Criteria (Gherkin)

### US-12.1 — View sport

#### Scenario: User views sport successfully
* **Given** a user is on the website
* **When** the user goes to the home page
* **Then** the system displays the home page with each sport and its information

#### Scenario: No sports exist in database
* **Given** a user is on the website
* **When** the user goes to the home page
* **Then** the system displays the home page with a NoSportsExistException

### US-12.2 — Access a sport's information

#### Scenario: User views sport successfully
* **Given** the system displays the home page with each sport and its information
* **When** the user attempts to access a given sport's information
* **Then** the system displays the sports?{sport_id} page with corresponding information

#### Scenario: Sport does not have information
* **Given** the system displays the home page with each sport and its information
* **When** the user attempts to access a given sport's information
* **Then** the system displays the sports?{sport_id} page with a NoSportInformationException