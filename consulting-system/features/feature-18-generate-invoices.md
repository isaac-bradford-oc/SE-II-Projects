# Feature: Generate Invoices

**Feature ID:** 18
**Branch pattern:** `feature/18-generate-invoices`
**Status:** Ready
**Created:** 2026-11-05
**Input:** Automatically generate invoices from reviewed timesheets for a project/client, creating the services section and updating timesheet status to 'invoiced'.
**Depends on:** — [Feature 7 — Maintain Invoices](feature-7-maintain-invoices.md), [Feature 5 — Maintain Timesheets](feature-5-maintain-timesheets.md), [Feature 3 — Maintain Rates](feature-3-maintain-rates.md), [Feature 4 — Maintain Projects](feature-4-maintain-projects.md), [Feature 6 — Maintain Clients](feature-6-maintain-clients.md)

---

## User Stories

### US-18.1: Generate invoice for project billing period
**As an** accounting member or PM
**I want to** generate an invoice for a specific project and billing date range from approved ('reviewed') timesheets
**So that** accurate client invoices are produced without manual entry and billed timesheets are marked as 'invoiced'

**Priority:** P1
**Independent test:** Generate an invoice for a project with reviewed timesheets; verify invoice created with matching service rows and timesheets marked 'invoiced'
**Acceptance scenarios:** see ### US-18.1 under Acceptance Criteria

### US-18.2: Preview and customize generated invoice parameters
**As an** accounting member
**I want to** select the invoice term (15 or 30 days) and payment method (check or wire) prior to final generation
**So that** the due date and payment instructions conform to the client's agreement

**Priority:** P1
**Independent test:** Configure 30-day term and wire payment method; verify invoice due date equals invoice date + 30 days and payment method is wire
**Acceptance scenarios:** see ### US-18.2 under Acceptance Criteria

---

## Acceptance Criteria (Gherkin)

### US-18.1 — Generate invoice for project billing period

#### Scenario: Successfully generate invoice from reviewed timesheets
* **Given** a project has 4 reviewed timesheets with defined billing rates totaling $4,000
* **When** an accounting member selects the project, sets term to 30 days, payment method to 'wire', and clicks "Generate Invoice"
* **Then** the system creates a new invoice with total $4,000 and 4 service lines
* **And** sets the due date to 30 days after the invoice date
* **And** updates all 4 timesheet records to status 'invoiced'
* **And** displays visual confirmation with the generated invoice number

#### Scenario: No reviewed timesheets available
* **Given** a project has no timesheets with status 'reviewed' in the selected period
* **When** the user attempts to generate an invoice
* **Then** the system throws a NoBillableTimesheetsException
* **And** displays an error message that no approved timesheets are available for billing

#### Scenario: Missing rate for project role
* **Given** a reviewed timesheet exists for a role that has no rate configured for the project
* **When** the invoice generation is attempted
* **Then** the system throws a MissingRateConfigurationException
* **And** displays which role is missing an assigned rate

### US-18.2 — Preview and customize generated invoice parameters

#### Scenario: Due date calculation for 15-day term
* **Given** an accounting member selects term of 15 days on invoice date 2026-11-01
* **When** the preview is generated
* **Then** the due date is calculated as 2026-11-16
* **And** payment method is reflected as chosen

#### Scenario: Missing required term or payment method during customization
* **Given** an accounting member attempts to finalize invoice generation with an empty payment method
* **When** the preview is submitted
* **Then** the system throws an InvalidInvoiceParametersException
* **And** highlights the missing parameter requiring user selection

