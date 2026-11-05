# Feature: Display Clients

**Feature ID:** 14
**Branch pattern:** `feature/14-display-clients`
**Status:** Ready
**Created:** 2026-11-05
**Input:** Display client directory including name, address, main contact, project sponsor, and account number.
**Depends on:** — [Feature 6 — Maintain Clients](feature-6-maintain-clients.md)

---

## User Stories

### US-14.1: View all clients
**As an** owner, PM, or accounting member
**I want to** view a list of all client organizations
**So that** I can review client contact, sponsorship, and account information

**Priority:** P1
**Independent test:** Navigate to `/clients` and verify all clients display with their account number, name, address, main contact, and project sponsor
**Acceptance scenarios:** see ### US-14.1 under Acceptance Criteria

### US-14.2: Search clients
**As a** user
**I want to** search clients by name or account number
**So that** I can quickly locate specific customer records

**Priority:** P1
**Independent test:** Search by account number and verify the matching client record is returned
**Acceptance scenarios:** see ### US-14.2 under Acceptance Criteria

### US-14.3: View client profile and engagements
**As a** user
**I want to** click on a client to view their associated projects and billing records
**So that** I can assess our history and engagements with that client

**Priority:** P1
**Independent test:** Click a client and verify associated projects and invoices appear on their profile
**Acceptance scenarios:** see ### US-14.3 under Acceptance Criteria

---

## Acceptance Criteria (Gherkin)

### US-14.1 — View all clients

#### Scenario: User views clients list successfully
* **Given** registered clients exist in the database
* **When** the user navigates to `/clients`
* **Then** the system displays all clients with their account number, name, main contact, and sponsor

#### Scenario: No clients exist
* **Given** no client records exist in the database
* **When** the user visits `/clients`
* **Then** the system displays "No clients found" with a prompt to add the first client

### US-14.2 — Search clients

#### Scenario: User searches for client by account number
* **Given** a client exists with account number "CLI-9001"
* **When** the user types "CLI-9001" into the search bar
* **Then** the table displays only the client matching that account number

#### Scenario: Search returns no matching clients
* **Given** registered clients exist in the database
* **When** the user enters an account number "CLI-0000" that does not match any record
* **Then** the table displays "No clients found matching 'CLI-0000'"

### US-14.3 — View client profile and engagements

#### Scenario: User views client profile
* **Given** a client has associated projects and invoice records
* **When** the user clicks on the client name
* **Then** the system displays the client profile showing contact details, active projects, and past invoices

#### Scenario: Client details accessed for non-existent client ID
* **Given** a user navigates to `/clients/999` where ID 999 does not exist
* **When** the request is made
* **Then** the system throws a ClientNotFoundException
* **And** displays an error message indicating the client was not found

