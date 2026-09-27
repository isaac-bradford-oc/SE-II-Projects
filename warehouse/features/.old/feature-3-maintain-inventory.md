# Feature: Maintain Inventory

**Feature ID:** 3
**Branch pattern:** `feature/3-maintain-inventory`
**Status:** Ready
**Created:** 2026-09-19
**Input:** 
**Depends on:** — [Feature 1 — Maintain User Authorization](feature-1-maintain-user-authorization.md)

---

## User Stories

### US-3.1: Update list of inventory items
**As a** office manager
**I want to** add, edit, or delete items from the inventory database
**So that** the database is kept up-to-date

**Priority:** P1
**Independent test:** Call `AuthService.login` with valid credentials; `AppContext` holds an `AuthSession` with the correct role
**Acceptance scenarios:** see ### US-3.1 under Acceptance Criteria

### US-3.2: Log outgoing items
**As a** picker
**I want to** log outgoing items as I pick them
**So that** the inventory database is kept up-to-date

**Priority:** P1
**Independent test:** Log in, log out, then call a protected service method and receive `NotAuthenticatedException`
**Acceptance scenarios:** see ### US-3.2 under Acceptance Criteria

### US-3.3: Log incoming items
**As a** dock worker
**I want** to log incoming items
**So that** the inventory database is kept up-to-date

**Priority:** P1
**Independent test:** Picker or dock worker `AuthSession` cannot invoke manager-only service methods; manager session can
**Acceptance scenarios:** see ### US-3.3 under Acceptance Criteria

### US-3.4: Log damaged/missing items
**As a** dock worker
**I want** to log damaged and/or missing items
**So that** the inventory database reflects the adjusted quantity of incoming items
**And** the supplier is notified

**Priority:** P1
**Independent test:** Picker or dock worker `AuthSession` cannot invoke manager-only service methods; manager session can
**Acceptance scenarios:** see ### US-3.4 under Acceptance Criteria

### US-3.5: Auto-order low items
**As a** automated process
**I want** order items when their quantity is below a calculated threshold
**So that** the inventory is kept adequately stocked for orders

**Priority:** P1
**Independent test:** Picker or dock worker `AuthSession` cannot invoke manager-only service methods; manager session can
**Acceptance scenarios:** see ### US-3.5 under Acceptance Criteria

### US-3.6: Manually order items
**As a** office manager
**I want** order an arbitrary quantity of items
**So that** the warehouse can account for abnormal situations

**Priority:** P1
**Independent test:** Picker or dock worker `AuthSession` cannot invoke manager-only service methods; manager session can
**Acceptance scenarios:** see ### US-3.6 under Acceptance Criteria

### US-3.7: Update list of suppliers
**As a** office manager
**I want to** add, edit, or delete items suppliers from the suppliers list
**So that** the warehouse knows from whom to order its products

**Priority:** P1
**Independent test:** Call `AuthService.login` with valid credentials; `AppContext` holds an `AuthSession` with the correct role
**Acceptance scenarios:** see ### US-3.7 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST allow office managers to audit individual items.
- **FR-002**: System MUST increment and decrement item quantities as logged by pickers and dock workers.
- **FR-003**: System MUST automatically order items up to their calculated maximum quantity when their current quantitiy goes below their calculated minimum quantity. 

---

## Key Entities

- **Item**: product with SKU, Item UPC, Case UPC, Supplier, Description, Bin/Slot location, Case Quantity, Case Cost, Price, On-hand, Min, Max, On-order, and Order Case.
- **Supplier**: item supplier with Name, Ship Days, Address, Terms, and Min Order.

---

## Data Model Requirements

### items

| Column | Notes |
|--------|-------|
| id | PK |
| sku | int, unique, required |
| itemUpc | int, unique, required |
| caseUpc | int, unique, required |
| supplierName | nvchar(100), required |
| description | nvchar(255), required |
| bin | nvchar(8), required |
| slot | nvchar(8), required |
| caseQuantity | int, required |
| caseCost | float, required |
| price | float, required |
| onHand | int, required |
| onOrder | int, required |
| minQuantity | int, required |
| maxQuantity | int, required |

### suppliers

| Column | Notes |
|--------|-------|
| id | PK |
| supplierName | nvchar(100), required |
| supplierAddress | nvchar(255), required |
| supplierShipDays | int, required |
| supplierTerms | nvchar(100), required |
| supplierMinOrder | int, required |

---

## Acceptance Criteria (Gherkin)

### US-3.1 — Log in

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

### US-3.2 — Log out

#### Scenario: Authorized user logs out
* **Given** a user is currently authorized
* **When** the user selects log out
* **Then** the system ends the session
* **And** no user remains authorized in `AppContext`

#### Scenario: Log out when no user is authorized
* **Given** no user is currently authorized
* **When** the client attempts to log out
* **Then** the system rejects the request with `NotAuthenticatedException`

### US-3.3 — Role-based access control

#### Scenario: Manager accesses a management function
* **Given** a user is logged in with role "manager"
* **When** the user invokes a manager-only protected service method
* **Then** the system allows the call (subject to that method’s own rules)

#### Scenario: Picker is denied a management function
* **Given** a user is logged in with role "picker"
* **When** the user invokes a manager-only protected service method
* **Then** the system throws `NotAuthorizedException`