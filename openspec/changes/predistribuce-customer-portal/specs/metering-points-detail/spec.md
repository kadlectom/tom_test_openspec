## ADDED Requirements

### Requirement: Metering Point Detail (Detail OM)
The system SHALL display comprehensive information about a selected metering point.

#### Scenario: Display contract parameters
- **WHEN** user views Detail OM
- **THEN** system displays: EAN, address, contract owner name, connection date, tariff type, service tier

#### Scenario: Display technical parameters
- **WHEN** user scrolls down on Detail OM
- **THEN** system displays: meter type, amperage (jistič), phase count (1-phase or 3-phase), meter serial number, installation date

#### Scenario: Display consumption graph
- **WHEN** user views Detail OM
- **THEN** system displays consumption graph for last 12 months (kWh), with month labels and values

#### Scenario: Graph time period selection
- **WHEN** user clicks on time period selector (12 months, 6 months, 3 months, 1 month)
- **THEN** system updates graph with selected period (if data available)

#### Scenario: Consumption data not available
- **WHEN** metering point has no consumption data (new connection)
- **THEN** system displays graph placeholder: "Data not yet available. Check back in a few days."

#### Scenario: Related service requests link
- **WHEN** user is on Detail OM
- **THEN** system displays link "View requests for this metering point" (filters Moje žádosti by current OM)

### Requirement: Metering Point Historical Information
The system SHALL preserve and display historical information about the metering point.

#### Scenario: View meter exchange history
- **WHEN** metering point has had meter changes in the past
- **THEN** system displays timeline: "Meter ABC123 replaced with XYZ789 on 2025-06-15"

#### Scenario: View tariff change history
- **WHEN** tariff has been changed on metering point
- **THEN** system displays: "Tariff changed from Standard to Economy on 2025-03-20"

#### Scenario: No historical changes
- **WHEN** metering point has no historical changes recorded
- **THEN** system displays "No changes recorded."
