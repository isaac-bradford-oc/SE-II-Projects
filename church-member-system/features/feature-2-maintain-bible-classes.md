# Feature: Maintain Bible Classes

**Feature ID:** 2
**Branch pattern:** `feature/2-Maintain-Bible-Classes`  
**Status:** Ready  
**Created:** 2026-09-04  
**Input:** This feature is for keeping Bible class attendance logs up-to-date.

---

## User Stories

### US-2.1: Add Bible class
**As an** authenticated user  
**I want to** add a new Bible class to the list   
**So that** church leadership can keep track of its attendance log.

**Priority:** P1  
**Independent test:** can I enter a Bible class name into a field and subsequently click a button to save the new class to the list of classes?
**Acceptance scenarios:** see ### US-2.1 under Acceptance Criteria

### US-2.2: Edit Bible class
**As an** authenticated user  
**I want to** edit any given Bible class's name  
**So that** class names remain up-to-date.

**Priority:** P1  
**Independent test:** for any given class, can I enter a name into a field and subsequently click a button to save the new name?
**Acceptance scenarios:** see ### US-2.2 under Acceptance Criteria

### US-2.3: Remove Bible class
**As an** authenticated user  
**I want to** remove an existing Bible class from the list - this doesn't delete historical data, only the class's inclusion in modifiable classes
**So that** the list does not contain classes that are no longer needed.

**Priority:** P1  
**Independent test:** for any given class, can I click a remove button to remove the class from the list of all classes?
**Acceptance scenarios:** see ### US-2.3 under Acceptance Criteria

### US-2.4: Add attendance list
**As an** authenticated user  
**I want to** add new attendance lists to Bible classes
**So that** Bible class attendance logs remain up-to-date.

**Priority:** P1  
**Independent test:** for any given Bible class, can I select a date and click a button to add a new attendance list to that class? 
**Acceptance scenarios:** see ### US-2.4 under Acceptance Criteria

### US-2.5: Edit attendance list
**As an** authenticated user  
**I want to** edit existing attendance lists 
**So that** Bible class attendance logs remain up-to-date.

**Priority:** P1  
**Independent test:** for any given attendance list, can I fill a form with a date and name to change the respective values of the given list? 
**Acceptance scenarios:** see ### US-2.5 under Acceptance Criteria

### US-2.6 Delete attendance list
**As an** authenticated user  
**I want to** delete existing attendance lists from Bible classes   
**So that** the class does not contain attendance lists that are no longer needed.

**Priority:** P1  
**Independent test:** for any given attendance list, can I click a button to delete that list from the class? 
**Acceptance scenarios:** see ### US-2.6 under Acceptance Criteria

### US-2.7: Add attendee to attendance list
**As an** authenticated user  
**I want to** add new attendee to an attendance log
**So that** Bible class attendance logs remain up-to-date.

**Priority:** P1  
**Independent test:** for any given attendance log, can I enter a first and last name, and click a button to add a new attendee to that list? 
**Acceptance scenarios:** see ### US-2.7 under Acceptance Criteria

### US-2.8: Edit attendee in attendance list
**As an** authenticated user  
**I want to** edit existing attendance list entries 
**So that** Bible class attendance logs remain up-to-date.

**Priority:** P1  
**Independent test:** for any given attendance list entry, can I enter a first and last name to change the respective values of the given entry? 
**Acceptance scenarios:** see ### US-2.8 under Acceptance Criteria

### US-2.9 Delete attendee from attendance list
**As an** authenticated user  
**I want to** delete existing attendance list entries   
**So that** the list does not contain inaccurate data.

**Priority:** P1  
**Independent test:** for any given attendance list, can I click a button to delete any given entry from that list? 
**Acceptance scenarios:** see ### US-2.9 under Acceptance Criteria


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

### `bibleClasses` table
| Field | Type | Rules |
|-------|------|-------|
| `id` | INTEGER PK | Auto-increment |
| `name` | STRING | Required; max 255 chars |
| `attendanceLists` | ARRAY | Required; default `[]` |

### `attendanceLists` table
| Field | Type | Rules |
|-------|------|-------|
| `id` | INTEGER PK | Auto-increment |
| `name` | STRING | Required; max 255 chars |
| `date` | STRING | Required; max 255 chars |
| `members` | ARRAY | Required; default `[]` |

---

## Acceptance Criteria

### US-2.1 — Add Bible class

#### Scenario: User adds a Bible class.
*   **Given** I am authenticated
*   **When** I enter the name of the Bible class into a field and click the "Add Bible Class" button
*   **Then** class list gets updated accordingly
*   **And** user is notified of successful operation.

#### Scenario: User adds an identical Bible class at the same moment as another user.
*   **Given** I am authenticated
*   **When** I enter the name of the Bible class into a field and click the "Add Bible Class" button at the same time as another authenticated user
*   **Then** class list gets updated with a duplicate entry.

### US-2.2 — Edit Bible class

#### Scenario: User edits a Bible class.
*   **Given** I am authenticated
*   **When** I enter the name of the Bible class into an "Edit Class Name" field and click a save button
*   **Then** class list gets updated accordingly
*   **And** user is notified of successful operation.

#### Scenario: User edits the Bible class at the same moment as another user.
*   **Given** I am authenticated
*   **When** I enter the name of the Bible class into an "Edit Class Name" field and click a save button at the same time as another authenticated user
*   **Then** the class is edited twice, which may or may not be an issue depending on the data.

### US-2.3 — Remove Bible class

#### Scenario: User removes a Bible class.
*   **Given** I am authenticated
*   **When** I click the "Remove Class" button for any given class
*   **Then** the class is removed from the class list, but database data is retained
*   **And** user is notified of successful operation.

#### Scenario: User removes a Bible class at the same moment as another user.
*   **Given** I am authenticated
*   **When** I click the "Remove Class" button for any given class at the same time as another authenticated user
*   **Then** the class is removed twice, throwing an exception.

### US-2.4 — Add attendance list

#### Scenario: User adds an attendance list.
*   **Given** I am authenticated
*   **When** I enter the date of the attendance list into a field and click the "Add Attendance List" button
*   **Then** class gets updated accordingly
*   **And** user is notified of successful operation.

#### Scenario: User adds an identical Bible class at the same moment as another user.
*   **Given** I am authenticated
*   **When** I enter the date of the attendance list into a field and click the "Add Attendance List" button at the same time as another authenticated user
*   **Then** class gets updated with a duplicate entry.

### US-2.5 — Edit attendance list

#### Scenario: User edits an attendance list.
*   **Given** I am authenticated
*   **When** I enter a new date into a field and click a save button
*   **Then** list gets updated accordingly
*   **And** user is notified of successful operation.

#### Scenario: User edits the attendance list at the same moment as another user.
*   **Given** I am authenticated
*   **When** I enter a new date into a field and click a save button at the same time as another authenticated user
*   **Then** the list is edited twice, which may or may not be an issue depending on the data.

### US-2.6 — Remove attendance list

#### Scenario: User removes an attendance list.
*   **Given** I am authenticated
*   **When** I click the "Remove Attendance list" button for any given class
*   **Then** the list is removed from the class
*   **And** list's database data is deleted
*   **And** user is notified of successful operation.

#### Scenario: User removes an attendance list at the same moment as another user.
*   **Given** I am authenticated
*   **When** I click the "Remove Attendance list" button for any given class at the same time as another authenticated user
*   **Then** the list is removed twice, throwing an exception.

### US-2.7 — Add attendee to attendance list

#### Scenario: User adds a attendee to an attendance list.
*   **Given** I am authenticated
*   **When** I enter the first and last name of an attendee into fields and click the "Add Attendee" button
*   **Then** list gets updated accordingly
*   **And** user is notified of successful operation.

#### Scenario: User adds an identical attendee at the same moment as another user.
*   **Given** I am authenticated
*   **When** I enter the first and last name of an attendee into fields and click the "Add Attendee" button at the same time as another authenticated user
*   **Then** list gets updated with a duplicate entry.

### US-2.8 — Edit attendee in attendance list

#### Scenario: User edits an attendee in an attendance list.
*   **Given** I am authenticated
*   **When** I enter a new first and last names into fields and click a save button
*   **Then** list gets updated accordingly
*   **And** user is notified of successful operation.

#### Scenario: User edits an attendee in an attendance list at the same moment as another user.
*   **Given** I am authenticated
*   **When** I enter a new first and last names into fields and click a save button at the same time as another authenticated user
*   **Then** the list is edited twice, which may or may not be an issue depending on the data.

### US-2.9 — Remove attendee from attendance list

#### Scenario: User removes an attendance list.
*   **Given** I am authenticated
*   **When** I click the "Remove Attendee" button for any given attendee
*   **Then** the attendee is removed from the list
*   **And** its database data is deleted
*   **And** user is notified of successful operation.

#### Scenario: User removes an attendee at the same moment as another user.
*   **Given** I am authenticated
*   **When** I click the "Remove Attendee" button for any given attendee at the same time as another authenticated user
*   **Then** the attendee is removed twice, throwing an exception.