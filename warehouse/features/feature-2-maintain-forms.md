# Feature: Maintain Forms

**Feature ID:** 2
**Branch pattern:** `feature/2-maintain-forms`
**Status:** Ready
**Created:** 2026-09-19
**Input:** Support form creation, auditing, drafting, and sending.
**Depends on:** — [Feature 1 — Maintain User Authorization](feature-1-maintain-user-authorization.md)

---

## User Stories

### US-2.1: Update list of available forms
**As a** office manager
**I want to** add, edit, or delete a form from the list
**So that** the available forms for office workers remain accurate

**Priority:** P1
**Independent test:** Call `AuthService.login` with valid credentials; `AppContext` holds an `AuthSession` with the correct role
**Acceptance scenarios:** see ### US-2.1 under Acceptance Criteria

### US-2.2: Make a draft
**As a** office worker
**I want to** make a new form draft and fill in necessary information
**So that** form is ready to be sent

**Priority:** P1
**Independent test:** Log in, log out, then call a protected service method and receive `NotAuthenticatedException`
**Acceptance scenarios:** see ### US-2.2 under Acceptance Criteria

### US-2.3: Send a form
**As a** office worker
**I want** to send a form to a supplier or customer
**So that** they have a record of the form's information

**Priority:** P1
**Independent test:** Picker or dock worker `AuthSession` cannot invoke manager-only service methods; manager session can
**Acceptance scenarios:** see ### US-2.3 under Acceptance Criteria

### US-2.4: Calculate total
**As a** automated process
**I want** to calculate the total price of items on any given form
**So that** everyone who sees the form can quickly see the total

**Priority:** P1
**Independent test:** Picker or dock worker `AuthSession` cannot invoke manager-only service methods; manager session can
**Acceptance scenarios:** see ### US-2.4 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST generate all forms with the same outline structure (order information at top, items in the middle, authorization user and order date at bottom).
- **FR-002**: System MUST send forms in a standard file format (e.g. PDF).
- **FR-003**: System MUST use the columns SKU, Description, Cases, Price, and Total for the middle (items) section of the forms with the grand total at the bottom.
- **FR-004**: System MUST send form files to suppliers/customers over email

---

## Key Entities

- **Form**: form object that knows its form type (Bill of Lading, Supplier Order Form, or Customer Order Form), information, recipient, and sender.
- **FormTypes**: list of form types that is updated by office managers.

---

## Data Model Requirements

### forms

| Column | Notes |
|--------|-------|
| id | PK |
| type | enum: `BILL_OF_LADING` \| `SUPPLIER_ORDER_FORM` \| `CUSTOMER_ORDER_FORM`, required |
| recipientAddress | nvchar(255), required |
| senderAddress | nvchar(255), required |
| customerNumber | int, required |
| postOfficeNumber | int, required |
| shippedDate | date, required |
| driverFirstName | nvchar(50), required |
| driverLastName | nvchar(50), required |
| deliveryDate | date, required |
| receivedBy | date, required |

---

## Acceptance Criteria (Gherkin)

### US-2.1 — Log in

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

### US-2.2 — Log out

#### Scenario: Authorized user logs out
* **Given** a user is currently authorized
* **When** the user selects log out
* **Then** the system ends the session
* **And** no user remains authorized in `AppContext`

#### Scenario: Log out when no user is authorized
* **Given** no user is currently authorized
* **When** the client attempts to log out
* **Then** the system rejects the request with `NotAuthenticatedException`

### US-2.3 — Role-based access control

#### Scenario: Manager accesses a management function
* **Given** a user is logged in with role "manager"
* **When** the user invokes a manager-only protected service method
* **Then** the system allows the call (subject to that method’s own rules)

#### Scenario: Picker is denied a management function
* **Given** a user is logged in with role "picker"
* **When** the user invokes a manager-only protected service method
* **Then** the system throws `NotAuthorizedException`