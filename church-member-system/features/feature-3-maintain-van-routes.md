# Feature: Maintain Van Routes

**Feature ID:** 3
**Branch pattern:** `feature/3-Maintain-Van-Routes`  
**Status:** Ready  
**Created:** 2026-09-04  
**Input:** This feature is for keeping van routes up-to-date.

---

## User Stories

### US-3.1: Add van route
**As an** authenticated user  
**I want to** add a new van route   
**So that** church leadership can keep track of van routes.

**Priority:** P1  
**Independent test:** can I enter a van route name, driver, and backup driver into a field and subsequently click a button to save the new route to the list of routes?
**Acceptance scenarios:** see ### US-3.1 under Acceptance Criteria

### US-3.2: Edit van route
**As an** authenticated user  
**I want to** edit any given van route
**So that** routes remain up-to-date.

**Priority:** P1  
**Independent test:** for any given van route, can I enter a name, driver, and backup driver into a field and subsequently click a button to save the new data?
**Acceptance scenarios:** see ### US-3.3 under Acceptance Criteria

### US-3.3: Delete van route
**As an** authenticated user  
**I want to** delete an existing van route from the list
**So that** the list does not contain routes that are no longer needed.

**Priority:** P1  
**Independent test:** for any given van route, can I click a remove button to remove the route from the list of all routes?
**Acceptance scenarios:** see ### US-3.3 under Acceptance Criteria

### US-3.4: Add travel time
**As an** authenticated user  
**I want to** add a travel time entry   
**So that** there is a record of travel times for each route.

**Priority:** P1  
**Independent test:** can I enter a departure and arrival time into fields, and subsequently click a button to save the new time to the list of times?
**Acceptance scenarios:** see ### US-3.4 under Acceptance Criteria

### US-3.5: Edit travel time
**As an** authenticated user  
**I want to** edit any given travel time
**So that** times are editable in case of input error.

**Priority:** P1  
**Independent test:** for any given travel time, can I enter new departure and arrival times, and subsequently click a button to save the new data?
**Acceptance scenarios:** see ### US-3.5 under Acceptance Criteria

### US-3.6: Delete travel time
**As an** authenticated user  
**I want to** delete an existing travel time from the list
**So that** the list does not contain times that were accidentally input.

**Priority:** P1  
**Independent test:** for any given travel time, can I click a remove button to remove the time from the list of all times?
**Acceptance scenarios:** see ### US-3.6 under Acceptance Criteria

### US-3.7: Calculate average travel time
**As an** automated process  
**I want to** calculate the average travel time of any given route
**So that** church leadership knows when to schedule the drivers.

**Priority:** P1  
**Independent test:** for any given route, can I average its list of travel times? 
**Acceptance scenarios:** see ### US-3.7 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST be available 24/7 with a 99.9% uptime.
- **FR-002**: System MUST be a maximum capacity of 12 authenticated users.
- **FR-003**: System MUST alert users if and when data pertaining to their session is modified.
- **FR-004**: Authenticated users MUST be able to edit fields.
- **FR-005**: System MUST require users to authenticate before accessing its data.

---

## Data Model Requirements

### `vanRoutes` table
| Field | Type | Rules |
|-------|------|-------|
| `id` | INTEGER PK | Auto-increment |
| `name` | STRING | Required; max 255 chars |
| `driver` | STRING | Required; max 255 chars |
| `backupDriver` | STRING | Required; max 255 chars |
| `travelTimes` | ARRAY | Required; default `[]` |

---

## Acceptance Criteria

### US-3.1 — Add van route

#### Scenario: User adds a van route.
*   **Given** I am authenticated
*   **When** I enter the name of the van route into a field and click the "Add Van Route" button
*   **Then** van route list gets updated accordingly
*   **And** user is notified of successful operation.

#### Scenario: User adds an identical van route at the same moment as another user.
*   **Given** I am authenticated
*   **When** I enter the name of the van route into a field and click the "Add Van Route" button at the same time as another authenticated user
*   **Then** van route list gets updated with a duplicate entry.

### US-3.2 — Edit van route

#### Scenario: User edits a van route.
*   **Given** I am authenticated
*   **When** I enter the name of the van route into an "Edit Route Name" field and click a save button
*   **Then** van route list gets updated accordingly
*   **And** user is notified of successful operation.

#### Scenario: User edits the van route at the same moment as another user.
*   **Given** I am authenticated
*   **When** I enter the name of the van route into an "Edit Route Name" field and click a save button at the same time as another authenticated user
*   **Then** the van route is edited twice, which may or may not be an issue depending on the data.

### US-3.3 — Delete van route

#### Scenario: User deletes a van route.
*   **Given** I am authenticated
*   **When** I click the "Delete Route" button for any given route
*   **Then** the route is removed from the van route list
*   **And** its database data is deleted
*   **And** user is notified of successful operation.

#### Scenario: User deletes a van route at the same moment as another user.
*   **Given** I am authenticated
*   **When** I click the "Delete Route" button for any given route at the same time as another authenticated user
*   **Then** the route is removed twice, throwing an exception.

### US-3.4 — Add travel time

#### Scenario: User adds an travel time.
*   **Given** I am authenticated
*   **When** I enter the travel time into a field and click the "Add Travel Time" button
*   **Then** travel time list gets updated accordingly
*   **And** user is notified of successful operation.

#### Scenario: User adds an identical van route at the same moment as another user.
*   **Given** I am authenticated
*   **When** I enter the travel time into a field and click the "Add Travel Time" button at the same time as another authenticated user
*   **Then** travel time list gets updated with a duplicate entry.

### US-3.5 — Edit travel time

#### Scenario: User edits an travel time.
*   **Given** I am authenticated
*   **When** I enter a new travel time into a field and click a save button
*   **Then** list gets updated accordingly
*   **And** user is notified of successful operation.

#### Scenario: User edits the travel time at the same moment as another user.
*   **Given** I am authenticated
*   **When** I enter a new travel time into a field and click a save button at the same time as another authenticated user
*   **Then** the list is edited twice, which may or may not be an issue depending on the data.

### US-3.6 — Remove travel time

#### Scenario: User deletes a travel time.
*   **Given** I am authenticated
*   **When** I click the "Delete Travel Time" button for any given class
*   **Then** the time is removed from the list
*   **And** its database data is deleted
*   **And** user is notified of successful operation.

#### Scenario: User deletes a travel time at the same moment as another user.
*   **Given** I am authenticated
*   **When** I click the "Delete Travel Time" button for any given class at the same time as another authenticated user
*   **Then** the time is removed twice, throwing an exception.