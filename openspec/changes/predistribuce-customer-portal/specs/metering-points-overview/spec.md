## ADDED Requirements

### Requirement: Metering Points List (Přehled OM)
The system SHALL display a list of all metering points belonging to the logged-in user.

#### Scenario: Display list for multiple metering points
- **WHEN** user has 2 or more metering points
- **THEN** system displays "Přehled OM" page with table/grid showing: address, EAN, amperage (jistič), tariff, and current status

#### Scenario: Navigation for single metering point
- **WHEN** user has exactly 1 metering point
- **THEN** sidebar shows "Detail OM" link directly (not "Přehled OM"), navigation skips list view

#### Scenario: Click on metering point
- **WHEN** user clicks on a metering point from the list
- **THEN** system navigates to Detail OM page for selected point

#### Scenario: Empty metering points
- **WHEN** user has no metering points
- **THEN** system displays "Žádná odběrná místa nebyla nalezena."

#### Scenario: Filter by status
- **WHEN** Metering Points List is displayed
- **THEN** system provides optional filter by status (Active, Inactive, Pending)

### Requirement: Metering Point Status
The system SHALL track and display the status of each metering point.

#### Scenario: Active metering point
- **WHEN** metering point is actively connected to PREdistribuce network
- **THEN** system displays status as "Aktivní" (green badge)

#### Scenario: Inactive metering point
- **WHEN** metering point is disconnected or deactivated
- **THEN** system displays status as "Neaktivní" (gray badge)

#### Scenario: Pending metering point
- **WHEN** metering point request is being processed
- **THEN** system displays status as "Čeká se na vyřízení" (yellow badge)
