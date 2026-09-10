# Feature: Maintain Website Frontend

**Feature ID:** 4
**Branch pattern:** `feature/4-Maintain-Website-Frontend`  
**Status:** Ready
**Created:** 2026-09-04  
**Input:** This feature is for keeping the church's front-facing website up-to-date.

---

## User Stories

### US-4.1: Add announcement
**As an** authenticated user  
**I want to** add a new announcement   
**So that** the public can keep up-to-date with church events.

**Priority:** P1  
**Independent test:** can I enter an announcement title and body (in both English and Spanish) into fields and subsequently click a button to save the new announcement to the "Announcements" page?
**Acceptance scenarios:** see ### US-4.1 under Acceptance Criteria

### US-4.2: Edit announcement
**As an** authenticated user  
**I want to** edit any given announcement
**So that** users can update announcements.

**Priority:** P1  
**Independent test:** for any given announcement, can I edit the title and body fields, and subsequently click a button to save the new data?
**Acceptance scenarios:** see ### US-4.3 under Acceptance Criteria

### US-4.3: Delete announcement
**As an** authenticated user  
**I want to** delete an existing announcement from the "Announcements" page
**So that** the page does not contain announcements that are no longer needed.

**Priority:** P1  
**Independent test:** for any given announcement, can I click a "Remove Announcement" button to remove the announcement from the "Announcements" page?
**Acceptance scenarios:** see ### US-4.3 under Acceptance Criteria

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

### `announcements` table
| Field | Type | Rules |
|-------|------|-------|
| `id` | INTEGER PK | Auto-increment |
| `title` | STRING | Required; max 100 chars |

---

## Acceptance Criteria

### US-4.1 — Add announcement

#### Scenario: User adds a announcement.
*   **Given** I am authenticated
*   **When** I enter the title and body of the announcement (in both English and Spanish) into fields and click the "Add Announcement" button
*   **Then** "Announcements" page gets updated accordingly
*   **And** user is notified of successful operation.

#### Scenario: User adds an identical announcement at the same moment as another user.
*   **Given** I am authenticated
*   **When** I enter the title and body of the announcement (in both English and Spanish) into a field and click the "Add Announcement" button at the same time as another authenticated user
*   **Then** "Announcements" page gets updated with a duplicate entry.

### US-4.2 — Edit announcement

#### Scenario: User edits an announcement.
*   **Given** I am authenticated
*   **When** I edit the English title and body, and Spanish title and body fields, and click a save button
*   **Then** "Announcements" page gets updated accordingly
*   **And** user is notified of successful operation.

#### Scenario: User edits the announcement at the same moment as another user.
*   **Given** I am authenticated
*   **When** I edit the English title and body, and Spanish title and body fields, and click a save button at the same time as another authenticated user
*   **Then** the announcement is edited twice, which may or may not be an issue depending on the data.

### US-4.3 — Delete announcement

#### Scenario: User deletes a announcement.
*   **Given** I am authenticated
*   **When** I click the "Delete Announcement" button for any given announcement
*   **Then** the announcement is removed from the "Announcements" page
*   **And** its database data is deleted
*   **And** user is notified of successful operation.

#### Scenario: User deletes a announcement at the same moment as another user.
*   **Given** I am authenticated
*   **When** I click the "Delete Announcement" button for any given announcement at the same time as another authenticated user
*   **Then** the announcement is removed twice, throwing an exception.