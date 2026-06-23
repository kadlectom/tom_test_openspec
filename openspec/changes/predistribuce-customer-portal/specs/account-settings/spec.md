## ADDED Requirements

### Requirement: Account Settings Dashboard (Nastavení účtu)
The system SHALL provide a comprehensive account management interface.

#### Scenario: Display account settings sections
- **WHEN** user navigates to "Nastavení účtu" (in sidebar under Účet)
- **THEN** system displays tabs: "Osobní údaje" / "Heslo" / "Notifikace" / "Správa uživatelů"

#### Scenario: Default tab
- **WHEN** user opens account settings
- **THEN** system defaults to "Osobní údaje" tab

### Requirement: Personal Information Management (Osobní údaje)
The system SHALL allow users to view and edit personal information.

#### Scenario: Display personal data
- **WHEN** user opens "Osobní údaje" tab
- **THEN** system displays (read-only or editable): full name, email, phone number, billing address, account creation date

#### Scenario: Edit name
- **WHEN** user clicks "Upravit" button next to name
- **THEN** system enables name field for edit, user changes name, clicks "Uložit"

#### Scenario: Edit contact information
- **WHEN** user edits email or phone
- **THEN** system updates field (email change may require re-verification via SMS/link)

#### Scenario: Edit billing address
- **WHEN** user edits billing address
- **THEN** system displays address form with: street, city, postal code, country (auto-filled for CZ)

#### Scenario: Save changes
- **WHEN** user saves changes
- **THEN** system displays "Údaje byly uloženy." confirmation

### Requirement: Password Change (Heslo)
The system SHALL allow secure password changes.

#### Scenario: Password change form
- **WHEN** user opens "Heslo" tab
- **THEN** system displays form with: current password (required), new password (required), confirm password (required)

#### Scenario: Current password verification
- **WHEN** user submits password change form
- **THEN** system verifies current password, rejects if incorrect with "Stávající heslo je nesprávné."

#### Scenario: New password validation
- **WHEN** user enters new password
- **THEN** system shows live strength validation: "Min. 8 znaků, 1 velké písmeno, 1 číslo, 1 speciální znak"

#### Scenario: Password match validation
- **WHEN** new password and confirm password don't match
- **THEN** system displays "Hesla se neshodují."

#### Scenario: Same password as current
- **WHEN** new password is same as current password
- **THEN** system displays "Nové heslo musí být jiné než stávající."

#### Scenario: Successful password change
- **WHEN** form is submitted with valid data
- **THEN** system updates password, sends email "Vaše heslo bylo změněno.", requires re-login on next session

### Requirement: Notification Settings (Notifikace)
The system SHALL allow users to control email and SMS notifications.

#### Scenario: Notification preferences display
- **WHEN** user opens "Notifikace" tab
- **THEN** system displays toggles for: outage notifications, request status updates, marketing emails, billing notifications, system alerts

#### Scenario: Outage notifications
- **WHEN** user toggles "Informace o odstávkách"
- **THEN** system enables/disables receiving advance notice of planned outages (notification enabled by default)

#### Scenario: Request status notifications
- **WHEN** user toggles "Stav žádostí"
- **THEN** system enables/disables email/SMS updates when service request status changes

#### Scenario: Marketing notifications
- **WHEN** user toggles "Marketingové sdělení"
- **THEN** system enables/disables promotional and newsletter emails (default: disabled)

#### Scenario: Billing notifications
- **WHEN** user toggles "Faktury a platby"
- **THEN** system enables/disables billing-related emails (invoice, overdue payment) (default: enabled)

#### Scenario: System alerts
- **WHEN** user toggles "Systémová upozornění"
- **THEN** system enables/disables critical system alerts (maintenance, security) (default: enabled)

#### Scenario: Notification delivery method
- **WHEN** notification setting is toggleable
- **THEN** user can select delivery method per notification: email, SMS, or both (where applicable)

#### Scenario: Save notification preferences
- **WHEN** user saves notification settings
- **THEN** system displays "Nastavení byly uloženy." and immediately applies changes

### Requirement: Additional User Management (Správa uživatelů)
The system SHALL allow Majitel OM to manage additional users with granular permissions.

#### Scenario: Display additional users list
- **WHEN** Majitel OM opens "Správa uživatelů" tab
- **THEN** system displays list of all Dodatečný uživatelé: name, email, phone, role, permissions (read-only / submit requests), access validity (unlimited / expires 2025-12-31)

#### Scenario: Invite additional user
- **WHEN** user clicks "Přidat uživatele" button
- **THEN** system displays form: email (required), name (auto-filled option), select metering points (checkboxes for each OM), permissions (checkboxes: read-only / submit requests), validity (unlimited / specify end date)

#### Scenario: Send invitation
- **WHEN** Majitel OM submits invitation form
- **THEN** system sends email to invitee with: invitation link, instructions, access type details, expires in 7 days if not accepted

#### Scenario: Invitation acceptance
- **WHEN** invitee clicks link and logs in (or registers if new)
- **THEN** system grants access to selected metering points with specified permissions

#### Scenario: Edit user permissions
- **WHEN** Majitel OM clicks "Upravit" on a Dodatečný uživatel row
- **THEN** system displays edit form: name, email (read-only), metering points (checkboxes), permissions (checkboxes), access validity

#### Scenario: Update access validity
- **WHEN** Majitel OM extends or shortens user access expiration date
- **THEN** system updates validity, notifies user via email of new expiration date

#### Scenario: Revoke access
- **WHEN** Majitel OM clicks "Odebrat přístup" on user row
- **THEN** system displays confirmation dialog, revokes all permissions, notifies user via email

#### Scenario: Revoked access attempt
- **WHEN** revoked user tries to log in
- **THEN** system displays "Váš přístup byl odebrán. Kontaktujte správce." on login

#### Scenario: No additional users
- **WHEN** Majitel OM has no additional users configured
- **THEN** system displays "Zatím jste nepřidali žádné další uživatele. Klikněte 'Přidat uživatele'."

### Requirement: Account Deletion (Smazání účtu)
The system SHALL allow users to delete their accounts with data anonymization.

#### Scenario: Delete account request
- **WHEN** user scrolls to bottom of settings and clicks "Smazat účet"
- **THEN** system displays confirmation warning: "Tato akce je trvalá. Budete mít 30 dní na znovuaktivaci."

#### Scenario: Confirmation email
- **WHEN** user confirms account deletion
- **THEN** system sends confirmation email with: 30-day reactivation link, account deletion summary, contact support info

#### Scenario: Account reactivation window
- **WHEN** user clicks reactivation link within 30 days
- **THEN** account is restored with all data intact

#### Scenario: Account purging
- **WHEN** 30-day window expires
- **THEN** system anonymizes personal data (name, email, address), retains only request history (for audit) with user ID anonymized
