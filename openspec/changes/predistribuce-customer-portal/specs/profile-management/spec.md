## ADDED Requirements

### Requirement: Profile Selection (Výběr profilu)
The system SHALL allow users with multiple roles or metering points to select which profile (role + metering point) they want to work with.

#### Scenario: Multiple roles available
- **WHEN** authenticated user has both "Majitel OM" and "Dodatečný uživatel" roles
- **THEN** system displays selectable list of all available profiles with role, name, address, and EAN

#### Scenario: Single metering point
- **WHEN** user has only one metering point with Majitel OM role
- **THEN** system skips Profile Selection, directly enters portal (Výběr profilu is hidden)

#### Scenario: Profile selection
- **WHEN** user clicks on a profile from the list
- **THEN** system loads selected profile, displays header with "ROLE / Name · Address" (left) and "Logged-in user" (right)

#### Scenario: No profiles available
- **WHEN** authenticated user has zero metering points assigned
- **THEN** system displays "No metering points found. Please contact support."

### Requirement: Profile Switching (Přepnutí profilu)
The system SHALL allow users to switch between profiles without logging out.

#### Scenario: Switch profile from menu
- **WHEN** user clicks "Volba profilu" (or similar) in account section of sidebar
- **THEN** system displays Profile Selection page, preserves logged-in state

#### Scenario: Switch to different role on same metering point
- **WHEN** user (logged-in as Majitel OM) switches to Dodatečný uživatel role on same OM
- **THEN** system updates session, restricts available actions based on Dodatečný uživatel permissions

#### Scenario: Header identity update
- **WHEN** user switches to different profile
- **THEN** system updates left header to show new role + name + address, keeps right header (logged-in user) unchanged

### Requirement: Role-Based Access Control
The system SHALL enforce different permissions for Majitel OM vs. Dodatečný uživatel.

#### Scenario: Majitel OM permissions
- **WHEN** user is Majitel OM
- **THEN** system allows: view all OM details, submit all service requests, manage additional users, change settings

#### Scenario: Dodatečný uživatel restricted permissions
- **WHEN** user is Dodatečný uživatel with "read-only" permission
- **THEN** system allows: view OM details, view service requests, but NOT submit new requests or manage users

#### Scenario: Dodatečný uživatel with "submit requests"
- **WHEN** user is Dodatečný uživatel with "submit requests" permission
- **THEN** system allows: view OM details, submit and manage service requests, view account settings (but NOT manage users)

#### Scenario: Permission expiration
- **WHEN** Dodatečný uživatel permission has expiration date and date passes
- **THEN** system revokes access, displays "Your access has expired" on login attempt
