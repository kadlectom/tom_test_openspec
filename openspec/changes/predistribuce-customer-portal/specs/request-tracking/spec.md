## ADDED Requirements

### Requirement: Service Requests List (Moje žádosti)
The system SHALL display a list of all submitted service requests with current status.

#### Scenario: Display requests list
- **WHEN** user navigates to "Moje žádosti"
- **THEN** system displays table with: request ID, service type, metering point (EAN), submission date, current status, last update date

#### Scenario: Status badge colors
- **WHEN** requests are displayed
- **THEN** system uses color-coded badges: "Přijato" (blue), "Formální kontrola" (orange), "Technická kontrola" (orange), "Rozhodnutí" (green/red), "Realizace" (blue)

#### Scenario: Filter by service type
- **WHEN** filter dropdown is available
- **THEN** user can filter: Show all / Změna jističe / EV nabíjení / Připojení / Notifikace / Smlouva / Sdílení / Samoodečet

#### Scenario: Filter by status
- **WHEN** status filter is available
- **THEN** user can filter: All / Pending / In progress / Completed / Rejected

#### Scenario: Filter by metering point
- **WHEN** user has multiple metering points
- **THEN** system allows filter by EAN to show requests for specific OM

#### Scenario: Sort by date
- **WHEN** user clicks "Submission date" header
- **THEN** system sorts requests ascending/descending by submission date

#### Scenario: Empty list
- **WHEN** user has no submitted requests
- **THEN** system displays: "Žádné žádosti. Začněte v sekci 'Potřebuji zařídit'." with link to service page

#### Scenario: Click on request
- **WHEN** user clicks on a request row
- **THEN** system navigates to Request Detail page

### Requirement: Service Request Detail (Detail žádosti)
The system SHALL display comprehensive information about a specific request with timeline and documents.

#### Scenario: Display request information
- **WHEN** user opens request detail
- **THEN** system displays: request ID, service type, metering point (address + EAN), submission date, expected completion date, status summary

#### Scenario: Display status timeline (Časová osa)
- **WHEN** user views request detail
- **THEN** system displays linear timeline with steps: "Přijato" → "Formální kontrola" → "Technická kontrola" → "Rozhodnutí" → "Realizace"

#### Scenario: Timeline with dates
- **WHEN** step is completed
- **THEN** timeline shows step name, completion date, and brief description (e.g., "Přijato 2026-06-23 10:15 — Vaše žádost byla zařazena do fronty.")

#### Scenario: Current step highlighting
- **WHEN** request is in progress
- **THEN** current step is highlighted with different color/styling, other completed steps are grayed out

#### Scenario: Pending step
- **WHEN** step is waiting to start
- **THEN** timeline shows step name with status "Čeká se" or empty date placeholder

#### Scenario: Rejection in timeline
- **WHEN** request is rejected
- **THEN** timeline shows: "Rozhodnutí - Zamítnutí na 2026-07-10 — Důvod: Parametry nejsou v souladu se sítí. Akce: Prosím zkuste znovu s jinými parametry."

#### Scenario: Documents section
- **WHEN** request has uploaded documents or attachments
- **THEN** system displays "Přiložené dokumenty" section with file list: name, type, upload date, download link

#### Scenario: Submitted data summary
- **WHEN** user views request detail
- **THEN** system displays "Vaše údaje" section with all submitted form data (read-only)

#### Scenario: Contact information
- **WHEN** request has contact information
- **THEN** system displays contact name, phone, email (read-only from submission)

#### Scenario: No documents
- **WHEN** request has no documents
- **THEN** system displays: "Žádné dokumenty." (instead of section)

### Requirement: Request Status Updates
The system SHALL update request status as it progresses through workflow.

#### Scenario: Automatic status synchronization
- **WHEN** PREdistribuce backend updates request status
- **THEN** system syncs status (polling or webhook), displays updated status on next page load or refresh

#### Scenario: Email notification on status change
- **WHEN** request status changes (formální→technická, technická→rozhodnutí, etc.)
- **THEN** system sends email to user: "Vaše žádost #PRED-2026-000123 postoupila na 'Technická kontrola'. Očekávaná lhůta: 30 dní."

#### Scenario: Rejection notification
- **WHEN** request is rejected
- **THEN** system sends email with: rejection reason, suggested next steps, link to submit new request

### Requirement: Request Actions
The system SHALL allow users to perform actions on submitted requests.

#### Scenario: Download request confirmation
- **WHEN** user clicks "Stáhnout potvrzení" on detail page
- **THEN** system generates and downloads PDF with request summary (ID, service, dates, status)

#### Scenario: Contact support
- **WHEN** user has question about request
- **THEN** system displays "Kontaktujte nás" section with email/phone/chat link

#### Scenario: Cancel request (if allowed)
- **WHEN** request is in "Přijato" or "Formální kontrola" status
- **THEN** system displays "Stornovat žádost" button, user can confirm cancellation

#### Scenario: Request cancellation
- **WHEN** user confirms cancellation
- **THEN** system marks request as "Zrušeno", sends cancellation email to user
