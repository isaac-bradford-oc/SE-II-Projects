# Feature: Maintain Invoices

**Feature ID:** 7
**Branch pattern:** `feature/7-maintain-invoices`
**Status:** Ready
**Created:** 2026-11-05
**Input:** Maintain client invoices (client name, client address, invoice number, invoice date, invoice term [15 or 30 days], invoice due date, project name, project sponsor, payment method [check or wire], services section [date, role, description, rate, hours, total]).
**Depends on:** — [Feature 4 — Maintain Projects](feature-4-maintain-projects.md), [Feature 6 — Maintain Clients](feature-6-maintain-clients.md), [Feature 2 — Maintain Roles](feature-2-maintain-roles.md)

---

## User Stories

### US-7.1: Add invoice manually
**As an** accounting member or PM
**I want to** manually create an invoice record with header details and service line items
**So that** billing can be issued for project services rendered

**Priority:** P1
**Independent test:** Add an invoice with services line items and verify all details in the database
**Acceptance scenarios:** see ### US-7.1 under Acceptance Criteria

### US-7.2: Edit invoice
**As an** accounting member or PM
**I want to** edit an unpaid/draft invoice's terms, payment method, or line item descriptions
**So that** billing errors can be corrected prior to final client submission

**Priority:** P1
**Independent test:** Modify invoice term and service item notes and confirm the updates persist
**Acceptance scenarios:** see ### US-7.2 under Acceptance Criteria

### US-7.3: Delete or void invoice
**As an** accounting member or owner
**I want to** void or delete an invalid draft invoice
**So that** inaccurate invoices do not impact financial accounts

**Priority:** P1
**Independent test:** Delete an unissued invoice and verify removal from the database
**Acceptance scenarios:** see ### US-7.3 under Acceptance Criteria

---

## Acceptance Criteria (Gherkin)

### US-7.1 — Add invoice manually

#### Scenario: User creates invoice successfully
* **Given** an accounting member inputs valid invoice details with term of 30 days and adds service line items
* **When** the user clicks save
* **Then** the system calculates the due date as invoice date + 30 days
* **And** computes line totals and invoice total
* **And** saves the invoice with status 'draft'

#### Scenario: Missing required term or payment method
* **Given** a user leaves term or payment method unselected
* **When** the user attempts to save the invoice
* **Then** the system throws an InvalidInvoiceParametersException
* **And** highlights the required missing fields

### US-7.2 — Edit invoice

#### Scenario: User modifies draft invoice successfully
* **Given** an accounting member updates the payment method from 'check' to 'wire' on a draft invoice
* **When** the user saves the changes
* **Then** the system updates the invoice record
* **And** displays visual confirmation of update

#### Scenario: User attempts to edit a sent or paid invoice
* **Given** a user attempts to edit an invoice whose status is 'paid'
* **When** the user clicks save
* **Then** the system throws an InvoiceLockedException
* **And** the changes are rejected

### US-7.3 — Delete or void invoice

#### Scenario: User voids draft invoice successfully
* **Given** an authorized user selects delete/void on a draft invoice
* **When** confirmation is accepted
* **Then** the system marks the invoice as void or removes it
* **And** confirmation is shown to the user

#### Scenario: Attempting to void a paid invoice
* **Given** an authorized user attempts to void or delete an invoice with status 'paid'
* **When** the void action is submitted
* **Then** the system throws a CannotVoidPaidInvoiceException
* **And** blocks the deletion to protect accounting records

