## ADDED Requirements

### Requirement: Portal Layout Structure (Základní layout)
The system SHALL provide consistent, responsive layout across all authenticated pages.

#### Scenario: Header structure
- **WHEN** user is logged in
- **THEN** system displays header with: PREdistribuce logo (left), selected profile identity (center: "ROLE / Name · Address"), logged-in user name + avatar (right)

#### Scenario: Sidebar navigation (Domácnosti)
- **WHEN** user is authenticated and in portal
- **THEN** system displays left sidebar with sections: Odběrná místa (Přehled OM or Detail OM based on count), Potřebuji zařídit, Moje žádosti, Účet (sub: Nastavení účtu, Volba profilu, Odhlášení)

#### Scenario: Main content area
- **WHEN** user navigates to a page
- **THEN** system displays main content in center column, with responsive max-width (1200px on desktop)

#### Scenario: Responsive design - tablet
- **WHEN** viewport width is 768-1024px (tablet)
- **THEN** sidebar is collapsible (hamburger menu), main content expands

#### Scenario: Responsive design - mobile
- **WHEN** viewport width is <768px (mobile)
- **THEN** sidebar is hidden (hamburger menu only), main content is full-width, header is condensed

#### Scenario: Footer
- **WHEN** user scrolls to bottom of page
- **THEN** system displays footer with: copyright, privacy policy link, terms of service link, technical support link, centered at bottom

### Requirement: Dashboard / Homepage (Domů)
The system SHALL display a welcome dashboard with key information and quick actions.

#### Scenario: Dashboard for authenticated user
- **WHEN** user logs in and completes Profile Selection
- **THEN** system displays Dashboard with: welcome message ("Vítejte, [Name]!"), summary cards (active metering points, open requests, recent notifications), quick action buttons (New request, View OM, My requests)

#### Scenario: Metering points summary
- **WHEN** dashboard is displayed
- **THEN** system shows card: "Vaše odběrná místa" with count, status indicator (all active / some inactive)

#### Scenario: Open requests summary
- **WHEN** dashboard is displayed
- **THEN** system shows card: "Aktivní žádosti" with count and list of top 3 most recent requests with status badges

#### Scenario: Recent notifications
- **WHEN** dashboard is displayed
- **THEN** system shows card: "Zprávy" with: outage notifications (planned maintenance), request status updates, system messages

#### Scenario: Quick action buttons
- **WHEN** dashboard is viewed
- **THEN** system displays 3 CTA buttons: "Nová žádost" (link to Potřebuji zařídit), "Moje odběrná místa" (link to Přehled/Detail OM), "Moje žádosti" (link to request tracking)

#### Scenario: No notifications
- **WHEN** user has no new notifications
- **THEN** dashboard displays "Žádné nové zprávy." in notifications card

### Requirement: Navigation and Menu Behavior
The system SHALL provide intuitive navigation with clear active states.

#### Scenario: Active menu item highlight
- **WHEN** user is on a page
- **THEN** corresponding sidebar menu item is highlighted with color and/or bold text

#### Scenario: Submenu expansion
- **WHEN** user hovers over or clicks expandable menu item
- **THEN** submenu items appear/collapse (e.g., "Účet" → "Nastavení účtu", "Volba profilu")

#### Scenario: Breadcrumb navigation
- **WHEN** user is on nested page (e.g., "Detail OM" → "Změna jističe" form)
- **THEN** system displays breadcrumb: "Domů / Potřebuji zařídit / Změna jističe" with links to navigate back

#### Scenario: Navigation persistence
- **WHEN** user navigates between pages
- **THEN** sidebar menu state is preserved (open/closed submenu, scroll position)

### Requirement: Accessibility (Přístupnost)
The system SHALL meet WCAG 2.1 AA accessibility standards.

#### Scenario: Keyboard navigation
- **WHEN** user navigates using Tab key
- **THEN** focus order is logical (header → sidebar → main content → footer), all interactive elements are focusable

#### Scenario: Screen reader support
- **WHEN** screen reader is used
- **THEN** all form labels have associated input elements, alt text for images, semantic HTML headers (h1, h2, etc.)

#### Scenario: Color contrast
- **WHEN** text is displayed
- **THEN** contrast ratio is at least 4.5:1 for normal text, 3:1 for large text (WCAG AA standard)

#### Scenario: Form error accessibility
- **WHEN** form has validation error
- **THEN** error message is linked to form field with aria-describedby, visible and announced by screen reader

### Requirement: Error Handling and User Feedback
The system SHALL provide clear error messages and user feedback.

#### Scenario: Error message display
- **WHEN** error occurs (form validation, server error, network error)
- **THEN** system displays error message in red with icon, clear explanation, suggested action

#### Scenario: Success message
- **WHEN** action completes successfully (form submitted, settings saved)
- **THEN** system displays success message (usually green toast notification) with confirmation text

#### Scenario: Loading state
- **WHEN** page or form is loading
- **THEN** system displays loading spinner or skeleton, prevents further user interaction until complete

#### Scenario: Network error handling
- **WHEN** network request fails
- **THEN** system displays "Problém s připojením. Zkuste později." with retry button

### Requirement: Responsive Typography and Spacing
The system SHALL use consistent typography and spacing across all pages.

#### Scenario: Heading hierarchy
- **WHEN** page is displayed
- **THEN** system uses: H1 for page title, H2 for sections, H3 for subsections (no skipped levels)

#### Scenario: Text sizing on mobile
- **WHEN** viewport is mobile (<768px)
- **THEN** base font size is at least 16px to prevent zoom-on-focus in iOS

#### Scenario: Touch target sizes
- **WHEN** buttons or interactive elements are displayed
- **THEN** minimum touch target size is 44x44px (for mobile), hover areas are at least 36x36px

### Requirement: Loading Performance
The system SHALL optimize loading times for better user experience.

#### Scenario: Initial page load
- **WHEN** user loads the portal
- **THEN** system serves First Contentful Paint (FCP) in <1.5 seconds, Largest Contentful Paint (LCP) in <2.5 seconds

#### Scenario: Image optimization
- **WHEN** image is loaded
- **THEN** system serves responsive images (srcset), lazy loading for below-fold images, optimized formats (WebP with fallback)

#### Scenario: Script splitting
- **WHEN** page loads
- **THEN** JavaScript is split: core code loaded initially, feature-specific code lazy-loaded on demand (code splitting)
