# Feature: Maintain Users

**Feature ID:** 10
**Branch pattern:** `feature/10-maintain-users`
**Status:** Ready
**Created:** 2026-10-11
**Input:** Keep current list of users updated.
**Depends on:** — 

---

## User Stories

### US-10.1: Add user
**As a** first-time user
**I want to** create an account
**So that** I can access the league website and stay up-to-date

**Priority:** P1
**Independent test:** Create an account as a new user and view the user in a database table
**Acceptance scenarios:** see ### US-10.1 under Acceptance Criteria

### US-10.2: Edit user
**As a** user
**I want to** edit my account information
**So that** my information remains up-to-date

**Priority:** P1
**Independent test:** Edit a user and view the user in a database table
**Acceptance scenarios:** see ### US-10.2 under Acceptance Criteria

### US-10.3: Delete user
**As a** user
**I want to** delete my account
**So that** my user data is deleted and so that I stop receiving communications

**Priority:** P1
**Independent test:** Delete user account and see that the user is not in a database table
**Acceptance scenarios:** see ### US-10.3 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST allow users to manage themselves.
- **FR-002**: System MUST validate user form input before saving to database.
- **FR-003**: System MUST provide the user with visual confirmation of action taken after attempting to save input.

---

## Key Entities

- **User**: a user with name, email, and hashed password.

---

## Data Model Requirements

### users

| Column | Notes |
|--------|-------|
| id | PK, int |
| name | nvarchar(100), required |
| email | nvarchar(254), required |
| password_hash | binary(32), required |

---

## Acceptance Criteria (Gherkin)

### US-10.1 — Add user

#### Scenario: User adds user successfully
* **Given** an user fills in the sign-up form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an user fills in the sign-up form with invalid information (e.g. too many characters)
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-10.2 — Edit user

#### Scenario: User edits user successfully
* **Given** an user fills in the "edit user" form with acceptable information
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an user fills in the "edit user" form with invalid information
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation

### US-10.3 — Delete user

#### Scenario: User deletes user successfully
* **Given** an user clicks the "delete user" button
* **When** the user saves the form
* **Then** the system saves the form to the database
* **And** the user receives visual confirmation

#### Scenario: User inputs invalid information into the form
* **Given** an user clicks the "delete user" button
* **When** the user saves the form
* **Then** the system throws an exception
* **And** the user receives visual confirmation