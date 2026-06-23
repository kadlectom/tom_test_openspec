## ADDED Requirements

### Requirement: User Registration (Domácnosti)
The system SHALL allow new users to register as Domácnost (household) customers with email verification via SMS.

#### Scenario: Successful registration
- **WHEN** user selects "Domácnost" type and submits EAN, email, phone, and reads terms
- **THEN** system sends 6-digit SMS code to phone, displays verification step

#### Scenario: SMS code entry
- **WHEN** user enters valid 6-digit code within 10 minutes
- **THEN** system proceeds to password creation step (min. 8 chars, 1 uppercase, 1 number, 1 special char)

#### Scenario: Password creation
- **WHEN** user enters matching passwords that meet requirements
- **THEN** system creates account, redirects to Profile Selection (Výběr profilu)

#### Scenario: Account already exists for EAN
- **WHEN** EAN is already registered in the system
- **THEN** system displays error "This EAN is already registered. Please log in."

#### Scenario: Invalid EAN
- **WHEN** EAN is not found in PREdistribuce data source
- **THEN** system displays "EAN not found in our system. Please contact support."

#### Scenario: SMS resend
- **WHEN** user clicks "Resend code" within SMS verification step
- **THEN** system sends new code with 60-second cooldown, max 3 attempts per hour

### Requirement: User Login
The system SHALL authenticate users with email and password, with account lockout after failed attempts.

#### Scenario: Successful login
- **WHEN** user enters correct email and password
- **THEN** system authenticates user and redirects to Profile Selection (Výběr profilu)

#### Scenario: Incorrect credentials
- **WHEN** user enters wrong email or password
- **THEN** system displays generic message "Nesprávný e-mail nebo heslo." and increments attempt counter

#### Scenario: Account lockout (3 attempts)
- **WHEN** user has 3 failed login attempts within 15 minutes
- **THEN** system locks account for 30 minutes, displays "Account temporarily locked. Use password recovery."

#### Scenario: Account lockout (10 daily attempts)
- **WHEN** user has 10 failed attempts in one day
- **THEN** system requires full password reset via email link (valid 30 min, one-time use)

### Requirement: Password Recovery
The system SHALL allow users to reset forgotten passwords through email link.

#### Scenario: Request password reset
- **WHEN** user submits email on "Zapomněli jste heslo?" page
- **THEN** system sends email with reset link (valid 30 min), displays "Pokud je e-mail registrován, odeslali jsme instrukce."

#### Scenario: Reset link clicked
- **WHEN** user clicks reset link within 30 minutes
- **THEN** system displays password creation form with live strength validation

#### Scenario: Password reset link expired
- **WHEN** user clicks expired or already-used reset link
- **THEN** system displays "Link expired. Request a new password reset."

#### Scenario: Resend reset email
- **WHEN** user clicks "Resend" on password recovery
- **THEN** system sends new email with 60-second cooldown, max 3 attempts per hour

### Requirement: Session Management
The system SHALL manage user sessions securely with appropriate timeouts.

#### Scenario: Session creation
- **WHEN** user logs in successfully
- **THEN** system creates secure HTTP-only cookie or JWT token with 24-hour expiration

#### Scenario: Session expiration
- **WHEN** 24 hours pass without user activity
- **THEN** system invalidates session, redirects user to login on next action

#### Scenario: Manual logout
- **WHEN** user clicks "Logout" button
- **THEN** system clears session and redirects to login page
