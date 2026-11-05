# Feature: Email Invoices to Clients

**Feature ID:** 20
**Branch pattern:** `feature/20-email-invoices-to-clients`
**Status:** Ready
**Created:** 2026-11-05
**Input:** Email finalized invoices to clients (project sponsor).
**Depends on:** — [Feature 7 — Maintain Invoices](feature-7-maintain-invoices.md), [Feature 18 — Generate Invoices](feature-18-generate-invoices.md), [Feature 6 — Maintain Clients](feature-6-maintain-clients.md)

---

## User Stories

### US-20.1: Email invoice to client
**As an** accounting member or PM
**I want to** email a generated invoice with complete service details and payment instructions to a client's project sponsor
**So that** the client receives prompt billing for services rendered

**Priority:** P1
**Independent test:** Send an invoice email to client recipients and verify email dispatch and status update to 'sent'
**Acceptance scenarios:** see ### US-20.1 under Acceptance Criteria

### US-20.2: Preview and customize invoice email
**As an** accounting member
**I want to** preview and edit the email body, CC addresses, and subject before dispatching
**So that** any custom client correspondence notes can be included

**Priority:** P1
**Independent test:** Edit the email message body and confirm the customized message is transmitted
**Acceptance scenarios:** see ### US-20.2 under Acceptance Criteria

---

## Acceptance Criteria (Gherkin)

### US-20.1 — Email invoice to client

#### Scenario: User successfully emails invoice to client
* **Given** an invoice has been generated with status 'draft' for a client with valid contact emails
* **When** the accounting member clicks "Send Invoice"
* **Then** the system sends the invoice email with the services breakdown attached/embedded to the client'sproject sponsor
* **And** updates the invoice status to 'sent'
* **And** logs the email transmission in `email_logs`
* **And** displays visual confirmation "Invoice {invoice_number} sent successfully"

#### Scenario: Client has no project sponsor email configured
* **Given** a client record is missing a valid email address for its project sponsor
* **When** the user attempts to send the invoice email
* **Then** the system throws a MissingRecipientEmailException
* **And** alerts the user to update the client's project sponsor email before sending

### US-20.2 — Preview and customize invoice email

#### Scenario: Accounting member adds custom note
* **Given** the email invoice modal is open
* **When** the user appends a note "Please note our updated wire instructions" to the email body
* **Then** the dispatched email includes the added note

#### Scenario: Email subject or body is empty
* **Given** a user clears the email subject line completely
* **When** the user clicks "Send Invoice"
* **Then** the system throws an EmptyEmailContentException
* **And** prevents sending until a subject is provided

