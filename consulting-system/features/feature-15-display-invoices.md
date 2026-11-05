# Feature: Display Invoices

**Feature ID:** 15
**Branch pattern:** `feature/15-display-invoices`
**Status:** Ready
**Created:** 2026-11-05
**Input:** Display invoices and invoice service item breakdowns (client name, client address, invoice number, invoice date, term, due date, project name, sponsor, payment method, services section).
**Depends on:** — [Feature 7 — Maintain Invoices](feature-7-maintain-invoices.md), [Feature 6 — Maintain Clients](feature-6-maintain-clients.md), [Feature 4 — Maintain Projects](feature-4-maintain-projects.md)

---

## User Stories

### US-15.1: View all invoices
**As an** accounting member, PM, or owner
**I want to** view a list of all client invoices
**So that** I can track billing status, due dates, and payment methods

**Priority:** P1
**Independent test:** Navigate to `/invoices` and verify invoices display with invoice number, client, project, date, due date, total, and status
**Acceptance scenarios:** see ### US-15.1 under Acceptance Criteria

### US-15.2: View detailed invoice and services section
**As a** user
**I want to** open a specific invoice to inspect its complete details including header info and itemized services section
**So that** I can review the date, role, description, rate, hours, and total for each service line

**Priority:** P1
**Independent test:** Click an invoice and verify the services breakdown table renders with accurate line calculations
**Acceptance scenarios:** see ### US-15.2 under Acceptance Criteria

### US-15.3: Filter invoices by status, client, or date
**As an** accounting member
**I want to** filter invoices by status ('draft', 'sent', 'paid', 'void'), client, or due date range
**So that** I can follow up on unpaid or overdue invoices

**Priority:** P1
**Independent test:** Filter invoices by status 'sent' and verify matching invoices are displayed
**Acceptance scenarios:** see ### US-15.3 under Acceptance Criteria

---

## Acceptance Criteria (Gherkin)

### US-15.1 — View all invoices

#### Scenario: Invoices list displays successfully
* **Given** invoices exist in the system
* **When** the user navigates to `/invoices`
* **Then** the table displays invoices with invoice number, client, due date, total, and status

#### Scenario: No invoices exist in the system
* **Given** no invoices have been generated yet
* **When** the user navigates to `/invoices`
* **Then** the system displays an empty table state with message "No invoices found"

### US-15.2 — View detailed invoice and services section

#### Scenario: User views itemized invoice
* **Given** an invoice exists with 3 service line items
* **When** the user opens the invoice details page
* **Then** the system displays the full invoice header (client, address, terms, payment method)
* **And** displays each service row with date, role, description, rate, hours, and line total
* **And** displays the computed total amount

#### Scenario: Invoice details requested for invalid invoice number
* **Given** a user navigates to `/invoices/INV-INVALID`
* **When** the page loads
* **Then** the system throws an InvoiceNotFoundException
* **And** displays an error notification to the user

### US-15.3 — Filter invoices by status, client, or date

#### Scenario: Filter invoices by status
* **Given** invoices exist with statuses 'draft', 'sent', and 'paid'
* **When** the user applies a filter for status 'sent'
* **Then** the list updates to display only invoices with status 'sent'

#### Scenario: Filter criteria matches no invoices
* **Given** no invoices currently have status 'void'
* **When** the user filters by status 'void'
* **Then** the system displays "No invoices match the selected criteria"

