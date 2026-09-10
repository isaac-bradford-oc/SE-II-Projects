# Feature: Maintain Members

**Feature ID:** 1
**Branch pattern:** `feature/1-Maintain-Members`  
**Status:** Ready  
**Created:** 2026-09-04  
**Input:** This feature is for tracking attendees' information.
**Depends on:** [Feature 2 — Maintain Bible Classes](feature-2-maintain-bible-classes.md)  

---

## User Stories

### US-1.1: Edit baptism status
**As an** authenticated user  
**I want to** edit any given attendee's baptism status  
**So that** church leadership can know who can participate in Communion.

**Priority:** P1  
**Independent test:** for any given attendee, can I click a button on the church website to edit that attendee's baptism status?
**Acceptance scenarios:** see ### US-1.1 under Acceptance Criteria

### US-1.2: Edit names
**As an** authenticated user  
**I want to** edit any given attendee's first and/or last name
**So that** church leadership can identify individual attendees.

**Priority:** P1  
**Independent test:** for any given attendee, can I type a name in a field, save the new name, and view the updated field?
**Acceptance scenarios:** see ### US-1.2 under Acceptance Criteria

### US-1.3: Edit address
**As an** authenticated user  
**I want to** edit any given attendee's postal address  
**So that** church leadership can send mail to attendees.

**Priority:** P1  
**Independent test:** for any given attendee, can I type an address in a field, save the new address, and view the updated field?
**Acceptance scenarios:** see ### US-1.3 under Acceptance Criteria

### US-1.4: Edit phone number
**As an** authenticated user  
**I want to** edit any given attendee's phone number  
**So that** church leadership can send texts to attendees.

**Priority:** P1  
**Independent test:** for any given attendee, can I type a phone number in a field, save the new number, and view the updated field?
**Acceptance scenarios:** see ### US-1.4 under Acceptance Criteria

### US-1.5 Edit school
**As an** authenticated user  
**I want to** edit any given child attendee's current school   
**So that** church leadership can provide the given child with transportation if necessary.

**Priority:** P1  
**Independent test:** for any given child attendee, can I type a school name in a field, save the new school, and view the updated field?
**Acceptance scenarios:** see ### US-1.5 under Acceptance Criteria

### US-1.6: Edit date of first attendance
**As an** authenticated user  
**I want to** edit any given attendee's date of first attendance  
**So that** church leadership can monitor influx rates and see how long people have been coming.

**Priority:** P1  
**Independent test:** for any given attendee, can I type a date in a field, save the new date, and view the updated field?
**Acceptance scenarios:** see ### US-1.3 under Acceptance Criteria

### US-1.7: Add associated family member
**As an** authenticated user  
**I want to** add a relative to any given attendee  
**So that** church leadership can see which attendees are related.

**Priority:** P1  
**Independent test:** for any given attendee, can I enter the name of the relative into a field, save the field, and view the new member in the associated family member list?
**Acceptance scenarios:** see ### US-1.7 under Acceptance Criteria

### US-1.8: Edit associated family member
**As an** authenticated user  
**I want to** edit any relative for any given attendee  
**So that** church leadership can see which attendees are related and keep entries up-to-date.

**Priority:** P1  
**Independent test:** for any given attendee, can I edit the name of any relative into a field, save the field, and view the edited member in the associated family member list?
**Acceptance scenarios:** see ### US-1.8 under Acceptance Criteria

### US-1.9: Remove associated family member
**As an** authenticated user  
**I want to** remove a relative from any given attendee  
**So that** church leadership can see which attendees are related and keep entires up-to-date.

**Priority:** P1  
**Independent test:** for any given attendee, can I click a remove button for any relative and view the updated associated family member list?
**Acceptance scenarios:** see ### US-1.9 under Acceptance Criteria

### US-1.10: Edit active status
**As an** automated process  
**I want to** change any given attendee's active status to "inactive" if they are not recorded in attendance lists for three consecutive months  
**So that** church leadership can reach out to inactive attendees and offer assistance if necessary.

**Priority:** P1  
**Independent test:** for any given attendee, does an authenticated user see their status as "inactive" if they are not recorded in church attendance lists for three consecutive months?
**Acceptance scenarios:** see ### US-1.8 under Acceptance Criteria

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

### `members` table
| Field | Type | Rules |
|-------|------|-------|
| `id` | INTEGER PK | Auto-increment |
| `baptismStatus` | BOOLEAN | Required; default `false` |
| `firstName` | STRING | Required; max 255 chars |
| `lastName` | STRING | Required; max 255 chars |
| `address` | STRING | Required; max 255 chars |
| `phoneNumber` | STRING | Required; max 255 chars |
| `school` | STRING | Max 255 chars |
| `dateFirstAttended` | STRING | Required; max 255 chars |
| `associatedFamily` | ARRAY | Required; default `[]`; references `memberList` |
| `activeStatus` | BOOLEAN | Required; default `true` |

---

## Acceptance Criteria

### US-1.1 — Edit baptism status

#### Scenario: User edits an attendee's baptism status using a button.
*   **Given** I am authenticated
*   **When** I click the "Mark attendee as (not) baptised" button
*   **Then** given attendee's baptism status field changes accordingly
*   **And** user is notified of successful operation.

#### Scenario: User edits an attendee's baptism status at the same moment as another user.
*   **Given** I am authenticated
*   **When** I click the "Mark attendee as (not) baptised" button at the same time as another authenticated user
*   **Then** given attendee's baptism status field changes twice (resuling in no actualized change).

### US-1.2 — Edit names

#### Scenario: User edits an attendee's first and last name.
*   **Given** I am authenticated
*   **When** I edit an attendee's first and last name and save it
*   **Then** given attendee's name fields change accordingly
*   **And** user is notified of successful operation.

#### Scenario: User edits an attendee's first or last name only.
*   **Given** I am authenticated
*   **When** I edit an attendee's first or last name and save it
*   **Then** given attendee's name fields change accordingly
*   **And** user is notified of successful operation.

#### Scenario: User edits an attendee's first and last name at the same moment as another user.
*   **Given** I am authenticated
*   **When** I edit an attendee's first and last name and save it at the same time as another authenticated user
*   **Then** given attendee's name fields change accordingly
*   **And** given attendee's name fields change twice (resuling in no actualized change).

### US-1.3 — Edit address

#### Scenario: User edits an attendee's address.
*   **Given** I am authenticated
*   **When** I edit an attendee's address and save it
*   **Then** given attendee's address field changes accordingly
*   **And** user is notified of successful operation.

#### Scenario: User edits an attendee's address at the same moment as another user.
*   **Given** I am authenticated
*   **When** I edit an attendee's address at the same time as another authenticated user
*   **Then** given attendee's address field changes twice (resuling in no actualized change).

### US-1.4 — Edit phone number

#### Scenario: User edits an attendee's phone number.
*   **Given** I am authenticated
*   **When** I edit an attendee's phone number and save it
*   **Then** given attendee's phone number field changes accordingly
*   **And** user is notified of successful operation.

#### Scenario: User edits an attendee's phone number at the same moment as another user.
*   **Given** I am authenticated
*   **When** I edit an attendee's phone number at the same time as another authenticated user
*   **Then** given attendee's phone number field changes twice (resuling in no actualized change).

### US-1.5 — Edit school

#### Scenario: User edits a child attendee's school.
*   **Given** I am authenticated
*   **When** I edit a child attendee's school name and save it
*   **Then** given attendee's school field changes accordingly
*   **And** user is notified of successful operation.

#### Scenario: User edits a child attendee's school at the same moment as another user.
*   **Given** I am authenticated
*   **When** I edit a child attendee's school name at the same time as another authenticated user
*   **Then** given attendee's school field changes twice (resuling in no actualized change).

### US-1.6 — Edit date of first attendance

#### Scenario: User edits an attendee's date of first attendance.
*   **Given** I am authenticated
*   **When** I edit an attendee's date of first attendance and save it
*   **Then** given attendee's date of first attendance field changes accordingly
*   **And** user is notified of successful operation.

#### Scenario: User edits an attendee's date of first attendance at the same moment as another user.
*   **Given** I am authenticated
*   **When** I edit an attendee's date of first attendance at the same time as another authenticated user
*   **Then** given attendee's date of first attendance field changes twice (resuling in no actualized change).

### US-1.7 — Add associated family

#### Scenario: User adds to an attendee's associated family.
*   **Given** I am authenticated
*   **When** I add a relative to an attendee's associated family list and save it
*   **Then** given attendee's relatives list changes accordingly
*   **And** user is notified of successful operation.

#### Scenario: User adds to an attendee's associated family at the same moment as another user.
*   **Given** I am authenticated
*   **When** I add a relative to an attendee's associated family list and save it at the same time as another authenticated user
*   **Then** new member is inserted into the given attendee's relatives list twice

### US-1.8 — Edit associated family

#### Scenario: User edits a relative in an attendee's associated family.
*   **Given** I am authenticated
*   **When** I edit the name of a relative from an attendee's associated family list and save it
*   **Then** given attendee's relatives list changes accordingly
*   **And** user is notified of successful operation.

#### Scenario: User edits a relative in an attendee's associated family at the same moment as another user.
*   **Given** I am authenticated
*   **When** I edit the name of a relative from an attendee's associated family list and save it at the same time as another authenticated user
*   **Then** the member name is edited twice, which may or may not be an issue depending on the data.

### US-1.9 — Remove associated family

#### Scenario: User removes a relative from an attendee's associated family.
*   **Given** I am authenticated
*   **When** I remove a relative from an attendee's associated family list and save it
*   **Then** given attendee's relatives list changes accordingly
*   **And** user is notified of successful operation.

#### Scenario: User removes a relative from an attendee's associated family at the same moment as another user.
*   **Given** I am authenticated
*   **When** I remove a relative from an attendee's associated family list and save it at the same time as another authenticated user
*   **Then** the member is removed from the given attendee's relatives list twice, throwing an exception.

### US-1.10 — Edit active status

#### Scenario: User edits an attendee's active status.
*   **Given** I am authenticated
*   **When** I edit an attendee's active status and save it
*   **Then** given attendee's active status field changes accordingly
*   **And** user is notified of successful operation.

#### Scenario: User edits an attendee's active status at the same moment as another user.
*   **Given** I am authenticated
*   **When** I edit an attendee's active status at the same time as another authenticated user
*   **Then** given attendee's active status field changes twice (resuling in no actualized change because this field is functionally a toggle).