# Feature: Display Rates

**Feature ID:** 11
**Branch pattern:** `feature/11-display-rates`
**Status:** Ready
**Created:** 2026-11-05
**Input:** Display billing rates per role per project.
**Depends on:** — [Feature 3 — Maintain Rates](feature-3-maintain-rates.md), [Feature 2 — Maintain Roles](feature-2-maintain-roles.md), [Feature 4 — Maintain Projects](feature-4-maintain-projects.md)

---

## User Stories

### US-11.1: View all billing rates
**As a** PM, owner, or accounting member
**I want to** view a table of all billing rates organized by project and role
**So that** I can review contracted billing amounts across projects

**Priority:** P1
**Independent test:** Navigate to `/rates` and verify rate records display with project name, role name, and hourly rate
**Acceptance scenarios:** see ### US-11.1 under Acceptance Criteria

### US-11.2: Filter rates by project or role
**As an** accounting member or PM
**I want to** filter rates by specific project or specific role
**So that** I can verify rates applicable to a particular engagement

**Priority:** P1
**Independent test:** Filter rates by a chosen project and verify only rates for that project appear
**Acceptance scenarios:** see ### US-11.2 under Acceptance Criteria

---

## Acceptance Criteria (Gherkin)

### US-11.1 — View all billing rates

#### Scenario: Rates table displays successfully
* **Given** rates are configured for projects and roles
* **When** the user navigates to `/rates`
* **Then** the system displays all rates showing project, role, and hourly rate formatted as currency

#### Scenario: No rates exist
* **Given** no rates have been configured yet
* **When** the user visits `/rates`
* **Then** an informative message "No billing rates configured" is displayed

### US-11.2 — Filter rates by project

#### Scenario: User filters rates by selected project
* **Given** rates exist across multiple projects
* **When** the user selects "Project Alpha" from the project filter dropdown
* **Then** the table displays only the rate rows belonging to "Project Alpha"

#### Scenario: Filtered project has no configured rates
* **Given** a new project "Project Beta" has no role rates set up
* **When** the user filters rates by "Project Beta"
* **Then** the system displays "No billing rates configured for this project" with an "Add Rate" button

