## ADDED Requirements

### Requirement: Brand Colors (Barevná paleta PREdistribuce)
The system SHALL use PREdistribuce brand colors consistently across all UI elements.

#### Scenario: Primary color usage
- **WHEN** primary CTA buttons, headers, or emphasis elements are displayed
- **THEN** system uses primary color #1a2f6e (dark navy blue) with hover state #152560 (darker shade)

#### Scenario: Accent red usage
- **WHEN** logo or critical alerts are displayed
- **THEN** system uses accent red #e30613 for the "E" in logo, error borders, critical warnings

#### Scenario: Accent green usage
- **WHEN** secondary CTA buttons (Register, success states) are displayed
- **THEN** system uses accent green #5a7a2b with hover state #4a6a20

#### Scenario: Neutral colors
- **WHEN** text, borders, or backgrounds are displayed
- **THEN** system uses: white #ffffff (background), light gray #cccccc (borders), dark text #1a1a1a (primary text), medium gray #555555 (secondary text)

#### Scenario: Semantic colors
- **WHEN** error messages are shown
- **THEN** system uses: error background #fdf0f0, error border #e30613, error icon #e30613, error title #c0392b

### Requirement: Typography System (Typografie)
The system SHALL use consistent font family and sizing hierarchy.

#### Scenario: Font family
- **WHEN** any text is rendered
- **THEN** system uses sans-serif font stack: 'Roboto', 'Inter', Arial, sans-serif (responsive system fonts)

#### Scenario: Heading 1 (H1)
- **WHEN** page title is displayed
- **THEN** font size: 32px, weight: 700 (bold), color: #1a1a1a, line-height: 1.2

#### Scenario: Heading 2 (H2)
- **WHEN** section heading is displayed
- **THEN** font size: 24px, weight: 700, color: #1a1a1a, line-height: 1.3

#### Scenario: Heading 3 (H3)
- **WHEN** subsection heading is displayed
- **THEN** font size: 18px, weight: 600, color: #1a1a1a, line-height: 1.4

#### Scenario: Body text
- **WHEN** standard paragraph or body copy is displayed
- **THEN** font size: 14px, weight: 400 (normal), color: #1a1a1a, line-height: 1.5

#### Scenario: Small text
- **WHEN** form label or helper text is displayed
- **THEN** font size: 13px, weight: 400, color: #555555, line-height: 1.4

#### Scenario: Large text (16px)
- **WHEN** emphasis or lead text is needed
- **THEN** font size: 16px, weight: 500, color: #1a1a1a, line-height: 1.5

### Requirement: Button Components (Tlačítka)
The system SHALL provide styled button components with consistent behavior.

#### Scenario: Primary button (Primární — modrá)
- **WHEN** primary action button is displayed (e.g., "Přihlásit se", "Odeslat")
- **THEN** background: #1a2f6e, text color: white, padding: 10px 28px, font-size: 14px, font-weight: 500, border: none, border-radius: 0 (sharp corners)

#### Scenario: Primary button hover
- **WHEN** user hovers over primary button
- **THEN** background changes to #152560 (darker shade), cursor is pointer

#### Scenario: Primary button disabled
- **WHEN** primary button is disabled (form incomplete)
- **THEN** background: #cccccc, text color: #999999, cursor is not-allowed

#### Scenario: Secondary button (Sekundární — zelená)
- **WHEN** secondary action button is displayed (e.g., "Registrujte se")
- **THEN** background: #5a7a2b, text color: white, padding: 10px 28px, font-size: 14px, font-weight: 500, border: none, border-radius: 0

#### Scenario: Secondary button hover
- **WHEN** user hovers over secondary button
- **THEN** background changes to #4a6a20, cursor is pointer

#### Scenario: Tertiary button (Text link)
- **WHEN** text link button is displayed (e.g., "Zapomněli jste heslo?")
- **THEN** text color: #1a2f6e, background: transparent, text-decoration: underline, cursor: pointer

#### Scenario: Button with icon
- **WHEN** button has icon
- **THEN** icon is left or right of text with 8px spacing, icon and text are vertically aligned

### Requirement: Form Components (Formulářové prvky)
The system SHALL provide styled form inputs with consistent validation states.

#### Scenario: Text input
- **WHEN** text input field is displayed
- **THEN** border: 1px solid #cccccc, width: 100%, height: 38px, padding: 0 10px, font-size: 14px, background: white, border-radius: 0

#### Scenario: Input focus state
- **WHEN** input receives focus (click or tab)
- **THEN** outline: none, border-color: #1a2f6e (primary color), subtle shadow (optional)

#### Scenario: Input with error
- **WHEN** input has validation error
- **THEN** border-color: #e30613 (red), error message displayed below in red

#### Scenario: Input with success
- **WHEN** input has valid value
- **THEN** border-color: #5a7a2b (green), optional checkmark icon

#### Scenario: Password input toggle
- **WHEN** password input is displayed
- **THEN** eye icon is visible on right side, clicking toggles password visibility

#### Scenario: Textarea
- **WHEN** textarea is displayed
- **THEN** same styling as text input, min-height: 120px, resize: vertical, font-family: monospace for code

#### Scenario: Select dropdown
- **WHEN** select/dropdown is displayed
- **THEN** same border/padding as text input, arrow icon on right, styling consistent with text input on focus/error

#### Scenario: Checkbox
- **WHEN** checkbox is displayed
- **THEN** size: 18x18px, border: 1px solid #cccccc, checked state: background #1a2f6e with white checkmark, label text adjacent with 8px spacing

#### Scenario: Radio button
- **WHEN** radio button is displayed
- **THEN** size: 18x18px, border: 1px solid #cccccc, selected state: inner circle #1a2f6e, label text adjacent with 8px spacing

#### Scenario: Form label
- **WHEN** form field has label
- **THEN** font-size: 13px, font-weight: 400, color: #555555, displayed above input with 4px margin-bottom

#### Scenario: Placeholder text
- **WHEN** input has placeholder
- **THEN** color: #999999, font-style: italic, disappears on focus

### Requirement: Card and Container Components (Karty a kontejnery)
The system SHALL provide styled card and container elements.

#### Scenario: Card component
- **WHEN** card is displayed (metering point summary, service tile)
- **THEN** border: 1px solid #cccccc, padding: 16px, background: white, border-radius: 4px, subtle shadow

#### Scenario: Card hover state
- **WHEN** user hovers over interactive card
- **THEN** shadow increases, border-color lightens slightly, cursor: pointer

#### Scenario: Panel/Section container
- **WHEN** main content panel is displayed
- **THEN** background: white, padding: 24px, border: 1px solid #cccccc, max-width responsive

### Requirement: Alert and Message Components (Oznámení a zprávy)
The system SHALL provide styled alerts for errors, success, warnings, and info messages.

#### Scenario: Error alert
- **WHEN** error message is displayed
- **THEN** background: #fdf0f0, border-left: 4px solid #e30613, text color: #c0392b, padding: 12px 16px, icon: red X

#### Scenario: Success alert
- **WHEN** success message is displayed
- **THEN** background: #f0fdf4, border-left: 4px solid #5a7a2b, text color: #2d5016, padding: 12px 16px, icon: green checkmark

#### Scenario: Warning alert
- **WHEN** warning message is displayed
- **THEN** background: #fffbeb, border-left: 4px solid #f59e0b, text color: #92400e, padding: 12px 16px, icon: yellow warning triangle

#### Scenario: Info alert
- **WHEN** information message is displayed
- **THEN** background: #eff6ff, border-left: 4px solid #1a2f6e, text color: #1e3a8a, padding: 12px 16px, icon: blue info circle

#### Scenario: Toast notification
- **WHEN** toast appears (form submitted, settings saved)
- **THEN** fixed position (bottom-right), auto-disappears after 4 seconds, color-coded based on type (success/error/info)

### Requirement: Table Components (Tabulky)
The system SHALL provide styled table for displaying lists.

#### Scenario: Table structure
- **WHEN** table is displayed (Přehled OM, Moje žádosti)
- **THEN** header row: bold text, background: #f0f0f0, data rows: alternating white/#fafafa background, border: 1px solid #cccccc

#### Scenario: Table header
- **WHEN** table header is shown
- **THEN** font-weight: 700, font-size: 13px, color: #1a1a1a, text-align: left (or right for numeric), clickable for sorting (optional)

#### Scenario: Table cell padding
- **WHEN** table cell is displayed
- **THEN** padding: 12px 16px, vertical-align: middle

#### Scenario: Table hover state
- **WHEN** user hovers over table row
- **THEN** background: #f5f5f5, cursor: pointer (if row is clickable)

### Requirement: Badge and Status Components (Odznaky a statusy)
The system SHALL provide styled status badges for request/metering point status.

#### Scenario: Active status badge
- **WHEN** metering point is active
- **THEN** background: #d1fae5, text color: #065f46, text: "Aktivní"

#### Scenario: Inactive status badge
- **WHEN** metering point is inactive
- **THEN** background: #e5e7eb, text color: #374151, text: "Neaktivní"

#### Scenario: Pending status badge
- **WHEN** request is pending
- **THEN** background: #fef3c7, text color: #92400e, text: "Čeká se"

#### Scenario: In-progress status badge
- **WHEN** request is in progress
- **THEN** background: #bfdbfe, text color: #1e40af, text: "V procesu"

#### Scenario: Completed status badge
- **WHEN** request is completed
- **THEN** background: #dcfce7, text color: #166534, text: "Hotovo"

#### Scenario: Rejected status badge
- **WHEN** request is rejected
- **THEN** background: #fee2e2, text color: #991b1b, text: "Zamítnuté"

### Requirement: Spacing and Layout Grid (Mezery a mřížka)
The system SHALL use consistent spacing and grid system.

#### Scenario: Spacing scale
- **WHEN** spacing is applied
- **THEN** scale used: 4px, 8px, 12px, 16px, 24px, 32px, 48px (multiples of 4)

#### Scenario: Grid system
- **WHEN** layout is created
- **THEN** grid is 12-column, responsive: 1 column (mobile), 2 columns (tablet), 3+ columns (desktop)

### Requirement: Dark Mode Support (Budoucí feature)
The system SHALL support dark mode (for future implementation).

#### Scenario: Dark mode colors (future)
- **WHEN** dark mode is enabled
- **THEN** background colors invert: white → #1a1a1a, text colors invert: #1a1a1a → white, borders: #333333, primary color: #6b93d6 (lighter blue)
