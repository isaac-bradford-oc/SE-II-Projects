# Feature: Maintain User Authorization

**Feature ID:** 1
**Branch pattern:** `feature/1-maintain-user-authorization`
**Status:** Ready
**Created:** 2026-09-19
**Input:** Control access to the warehouse system by identity and role; support log in and log out.
**Depends on:** —

---

## User Stories

### US-1.1: Log in
**As a** user (office, dock worker, or picker)
**I want to** log in with username and password
**So that** I gain authorized access to the functions allowed for my role

**Priority:** P1
**Independent test:** Call `AuthService.login` with valid credentials; `AppContext` holds an `AuthSession` with the correct role
**Acceptance scenarios:** see ### US-1.1 under Acceptance Criteria

### US-1.2: Log out
**As a** authorized user
**I want to** log out
**So that** my session ends and no user remains authorized on that client

**Priority:** P1
**Independent test:** Log in, log out, then call a protected service method and receive `NotAuthenticatedException`
**Acceptance scenarios:** see ### US-1.2 under Acceptance Criteria

### US-1.3: Role-based access control
**As a** office manager
**I want** management and report functions restricted to managers
**So that** only permitted users can maintain master data or view reports

**Priority:** P1
**Independent test:** Picker or dock worker `AuthSession` cannot invoke manager-only service methods; manager session can
**Acceptance scenarios:** see ### US-1.3 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST authenticate users with username and password credentials.
- **FR-002**: System MUST grant access only when credentials match a user previously set up in the system.
- **FR-003**: System MUST reject invalid credentials with a clear error and MUST NOT establish an `AuthSession`.
- **FR-004**: System MUST end the user’s authorized session on log out so that no user remains authorized in `AppContext`.
- **FR-005**: System MUST deny log out when no user is currently authorized.
- **FR-006**: System MUST associate each user with a role of `manager`, `picker`, or `dockWorker`.
- **FR-007**: System MUST allow manager-role users to access maintenance and report functions (enforced for Features 2–6 and 9–11).
- **FR-008**: System MUST deny non-manager-role users access to maintenance and report functions.
- **FR-009**: System MUST require a valid `AuthSession` in `AppContext` for all protected service methods.

---

## Key Entities

- **User**: account with username, password (hashed), and role (`manager` | `picker` | `dockWorker`)
- **AuthSession**: in-memory session in `AppContext` (userId, username, role, loginTime) — not an HTTP token

---

## Data Model Requirements

### users

| Column | Notes |
|--------|-------|
| id | PK |
| username | unique, required |
| password | hashed; never exposed outside security package |
| role | enum: `MANAGER` \| `PICKER` \| `DOCK_WORKER`, required |

---

## Acceptance Criteria (Gherkin)

### US-1.1 — Log in

#### Scenario: User logs in with valid credentials
* **Given** a user exists with username "manager1", password "secret", and role "manager"
* **When** the user submits those credentials to log in
* **Then** the system grants access
* **And** the `UserView` includes role "manager"
* **And** `AppContext` holds an `AuthSession` for that user

#### Scenario: User logs in with invalid credentials
* **Given** a user exists with username "manager1"
* **When** the user submits username "manager1" and an incorrect password
* **Then** the system shows an error
* **And** no `AuthSession` is established

#### Scenario: User logs in when not set up in the system
* **Given** no user exists with username "unknown"
* **When** the user submits username "unknown" and any password
* **Then** the system shows an error
* **And** no `AuthSession` is established

### US-1.2 — Log out

#### Scenario: Authorized user logs out
* **Given** a user is currently authorized
* **When** the user selects log out
* **Then** the system ends the session
* **And** no user remains authorized in `AppContext`

#### Scenario: Log out when no user is authorized
* **Given** no user is currently authorized
* **When** the client attempts to log out
* **Then** the system rejects the request with `NotAuthenticatedException`

### US-1.3 — Role-based access control

#### Scenario: Manager accesses a management function
* **Given** a user is logged in with role "manager"
* **When** the user invokes a manager-only protected service method
* **Then** the system allows the call (subject to that method’s own rules)

#### Scenario: Picker is denied a management function
* **Given** a user is logged in with role "picker"
* **When** the user invokes a manager-only protected service method
* **Then** the system throws `NotAuthorizedException`