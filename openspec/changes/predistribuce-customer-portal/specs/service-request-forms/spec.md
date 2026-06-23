## ADDED Requirements

### Requirement: Service Request Landing Page (Potřebuji zařídit)
The system SHALL display all available services as tiles in a 3-column grid.

#### Scenario: Display service tiles
- **WHEN** user navigates to "Potřebuji zařídit" section
- **THEN** system displays 7 service tiles: Změna jističe, EV nabíjení, Připojení síť, Přerušení info, Změna smlouvy, Sdílení elektřiny, Samoodečet

#### Scenario: Service tile content
- **WHEN** service tile is displayed
- **THEN** tile contains: icon, service name, one-line description, "Zjistit více →" link

#### Scenario: Click service tile
- **WHEN** user clicks on a service tile
- **THEN** system navigates to service detail page (description, steps, required documents, processing time, "Přejít k formuláři" button)

### Requirement: Service Detail Page
The system SHALL explain each service with steps, documents, and processing time.

#### Scenario: Service detail structure
- **WHEN** user views service detail
- **THEN** system displays: service description, numbered step list, required documents list, estimated processing time, "Přejít k formuláři" CTA button

#### Scenario: Required documents list
- **WHEN** service requires attachments (e.g., technical drawings)
- **THEN** system lists: "Povinné doklady: Technické schéma, Fotografie měřidla" with file format hints (PDF, JPG, max 5MB)

#### Scenario: Back to services list
- **WHEN** user clicks back or breadcrumb
- **THEN** system returns to "Potřebuji zařídit" landing page

### Requirement: Online Service Request Forms
The system SHALL provide structured forms for submitting 7 types of service requests.

#### Scenario: Cambio jističe (Amperage Change)
- **WHEN** user selects "Změna jističe" and clicks "Přejít k formuláři"
- **THEN** system displays form with: metering point selector, current amperage (read-only), requested amperage (select dropdown), reason (radio: renovation/appliance/tariff/other), description, contact info (read-only, but editable)

#### Scenario: EV Charging Station (Připojení dobíjecí stanice)
- **WHEN** user selects EV charging and clicks form
- **THEN** system displays form with: metering point selector, charger type (dropdown: wallbox/public), power (kW input), connection type (1-phase/3-phase), model name, documents (file upload), contact info

#### Scenario: Grid Connection (Připojení k síti)
- **WHEN** user selects "Připojení k distribuční síti" and clicks form
- **THEN** system displays form with: address/parcel, desired power (kW), consumption type (household/business), reason (new construction/expansion), documents (address plan, power calculation), contact info

#### Scenario: Outage Notifications (Informace o přerušení)
- **WHEN** user selects "Informace o přerušení dodávky"
- **THEN** system displays settings form: metering point selector, delivery method (email/SMS), notification type (planned outages only / planned + recovery notification), enable button

#### Scenario: Contract Change (Změna smlouvy)
- **WHEN** user selects "Změna smlouvy" and clicks form
- **THEN** system displays form with: change type (tariff/billing address/contact/payment method/other), selected change details, required documents, contact info

#### Scenario: Energy Sharing (Sdílení elektřiny - CEZ)
- **WHEN** user selects "Sdílení elektřiny" and clicks form
- **THEN** system displays form with: metering point selector (must be producer), sharing model (bilateral/community group), participant EAN list (comma-separated), documents, contact info

#### Scenario: Manual Meter Reading (Samoodečet)
- **WHEN** user selects "Samoodečet elektroměru" and clicks form
- **THEN** system displays inline form with: metering point selector, reading date (pre-filled with today), high tariff (kWh) number input, low tariff (kWh) number input (if dual-rate)

### Requirement: Form Validation
The system SHALL validate form inputs both client-side and server-side.

#### Scenario: Required field validation
- **WHEN** user submits form with empty required field
- **THEN** system displays red error message below field: "Toto pole je povinné."

#### Scenario: EAN validation
- **WHEN** user enters EAN
- **THEN** system validates format (12-13 digits), displays error if invalid

#### Scenario: Number range validation
- **WHEN** user enters amperage or power
- **THEN** system validates min/max (e.g., amperage 6-63), shows error if outside range

#### Scenario: File upload validation
- **WHEN** user uploads document
- **THEN** system validates type (PDF, JPG, PNG), size (max 5MB), shows error if invalid

#### Scenario: Duplicate meter reading
- **WHEN** user submits meter reading with value equal to or less than last reading
- **THEN** system displays error: "Entered reading must be higher than the last recorded reading."

### Requirement: Form Submission
The system SHALL submit requests to backend and confirm receipt.

#### Scenario: Successful submission
- **WHEN** user completes form and clicks "Odeslat" button
- **THEN** system shows loading state, submits to backend, displays success message: "Vaše žádost byla přijata. Číslo žádosti: #123456"

#### Scenario: Submission failure
- **WHEN** backend returns error (network, server error)
- **THEN** system displays error message: "Nepodařilo se odeslat žádost. Prosím zkuste později."

#### Scenario: Request number generation
- **WHEN** form is successfully submitted
- **THEN** system generates unique request ID (e.g., "PRED-2026-000123") displayed to user

#### Scenario: Confirmation email
- **WHEN** request is submitted
- **THEN** system sends confirmation email to user with: request ID, service name, submitted data, expected processing time
