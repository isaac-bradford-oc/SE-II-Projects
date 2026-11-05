# Feature: Maintain Clients

**Feature ID:** 6
**Branch pattern:** `feature/6-maintain-clients`
**Status:** Ready
**Created:** 2026-11-05
**Input:** Maintain client organizations including name, address, main contact, project sponsor, and account number.
**Depends on:** — 

---

## User Stories

### US-6.1: Add client
**As an** owner or PM
**I want to** add a client organization with contact and billing information
**So that** projects, billing agreements, and invoices can be linked to the client

**Priority:** P1
**Independent test:** Add a new client and verify the client appears in the clients database table
**Acceptance scenarios:** see ### US-6.1 under Acceptance Criteria

### US-6.2: Edit client
**As an** owner or PM
**I want to** update client details such as address, main contact, or project sponsor
**So that** communication and invoicing information remains accurate

**Priority:** P1
**Independent test:** Update a client's main contact or address and verify updates in the database
**Acceptance scenarios:** see ### US-6.2 under Acceptance Criteria

### US-6.3: Delete client
**As an** owner
**I want to** delete an inactive client with no active projects or invoices
**So that** the client directory remains free of obsolete accounts

**Priority:** P1
**Independent test:** Delete a client with no dependencies and verify removal from database
**Acceptance scenarios:** see ### US-6.3 under Acceptance Criteria

---

## Acceptance Criteria (Gherkin)

### US-6.1 — Add client

#### Scenario: User creates client successfully
* **Given** an owner or PM fills in the "add client" form with valid name, address, main contact, project sponsor, and unique account number
* **When** the user clicks save
* **Then** the system inserts the client record into the database
* **And** the user receives confirmation of client creation

#### Scenario: Duplicate account number entered
* **Given** a user enters an account number that already belongs to another client
* **When** the user attempts to save the client
* **Then** the system throws a DuplicateAccountNumberException
* **And** the user is informed that the account number must be unique

### US-6.2 — Edit client

#### Scenario: User edits client successfully
* **Given** an authorized user updates the address and project sponsor for a client
* **When** the user clicks update
* **Then** the system updates the client record in the database
* **And** the user receives visual confirmation of the update

#### Scenario: User clears required client name
* **Given** an authorized user clears the client name field while editing
* **When** the user clicks update
* **Then** the system throws a MissingRequiredFieldsException
* **And** the client record is not updated

### US-6.3 — Delete client

#### Scenario: User deletes client with no active projects
* **Given** an owner chooses to delete a client with no associated projects or invoices
* **When** deletion is confirmed
* **Then** the system removes the client from the database
* **And** the user receives visual confirmation of deletion

#### Scenario: Client has linked projects
* **Given** an owner attempts to delete a client that is linked to existing projects
* **When** deletion is attempted
* **Then** the system throws a ClientHasActiveProjectsException
* **And** the deletion is prevented

