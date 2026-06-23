## 1. Backend Setup (Supabase)

- [ ] 1.1 Provision Supabase project and PostgreSQL database
- [ ] 1.2 Configure authentication (email/password, SMS OTP via Twilio/similar)
- [ ] 1.3 Create database schema: users, metering_points, roles, service_requests, additional_users
- [ ] 1.4 Set up Supabase Auth with SMS verification flow
- [ ] 1.5 Create API endpoints for user registration and login
- [ ] 1.6 Implement session management (JWT tokens, refresh tokens)
- [ ] 1.7 Set up role-based access control (RLS policies)
- [ ] 1.8 Create API endpoint for EAN validation (sync with PREdistribuce data source)
- [ ] 1.9 Set up database audit logging for GDPR compliance

## 2. Frontend Scaffolding

- [ ] 2.1 Initialize Next.js project with TypeScript
- [ ] 2.2 Configure Tailwind CSS and custom PRE color variables
- [ ] 2.3 Install and configure Supabase client library
- [ ] 2.4 Set up environment variables (.env.local)
- [ ] 2.5 Create folder structure: pages, components, lib, styles
- [ ] 2.6 Set up ESLint and Prettier for code standards
- [ ] 2.7 Configure next.config.js for image optimization
- [ ] 2.8 Set up error boundary and error handling utilities

## 3. Authentication Flow (Autentizace)

- [ ] 3.1 Create Registration page layout (two-column: left form, right benefits)
- [ ] 3.2 Implement registration form component (type selection, EAN, email, phone)
- [ ] 3.3 Implement SMS OTP verification step with 10-minute timeout
- [ ] 3.4 Implement password creation step with strength validation
- [ ] 3.5 Create Login page with email/password fields
- [ ] 3.6 Implement login error handling (generic message, attempt tracking)
- [ ] 3.7 Implement account lockout after 3 failed attempts (30-min cooldown)
- [ ] 3.8 Implement account lockout after 10 daily attempts (force password reset)
- [ ] 3.9 Create Password Recovery page (3-step: email → link → new password)
- [ ] 3.10 Implement password reset email with 30-minute expiring link
- [ ] 3.11 Implement resend SMS/email with 60-sec cooldown and 3-attempt limit
- [ ] 3.12 Set up session management (HTTP-only cookies or JWT with 24h expiration)
- [ ] 3.13 Implement logout functionality
- [ ] 3.14 Add security headers (CSRF, XSS, Content-Security-Policy)

## 4. Profile Selection and Management (Profily)

- [ ] 4.1 Create Profile Selection page (list of available roles/metering points)
- [ ] 4.2 Implement profile switching without logout
- [ ] 4.3 Update header with selected profile (role/name·address on left, user on right)
- [ ] 4.4 Implement role-based access control (Majitel OM vs Dodatečný uživatel permissions)
- [ ] 4.5 Create permission validation middleware for API endpoints
- [ ] 4.6 Implement conditional navigation (Přehled OM vs Detail OM based on count)

## 5. Metering Points (Odběrná místa)

- [ ] 5.1 Create Metering Points Overview page (table/grid with address, EAN, amperage, tariff, status)
- [ ] 5.2 Implement filters (by status: active/inactive/pending)
- [ ] 5.3 Implement sorting by column (date, address, EAN)
- [ ] 5.4 Create Metering Point Detail page layout
- [ ] 5.5 Implement contract parameters display (EAN, address, owner, tariff, service tier)
- [ ] 5.6 Implement technical parameters display (meter type, amperage, phase count, serial, install date)
- [ ] 5.7 Create consumption graph component (12-month data, time period selector)
- [ ] 5.8 Implement lazy loading for consumption data
- [ ] 5.9 Display historical changes (meter replacement, tariff changes)
- [ ] 5.10 Add link to filter requests by selected metering point

## 6. Service Request Forms (Formuláře pro služby)

- [ ] 6.1 Create Service Landing Page ("Potřebuji zařídit") with 7 service tiles
- [ ] 6.2 Create Service Detail page template (description, steps, documents, processing time)
- [ ] 6.3 Implement amperage change form (metering point selector, current amperage, requested amperage, reason, description)
- [ ] 6.4 Implement EV charging station form (charger type, power, connection type, model, documents)
- [ ] 6.5 Implement grid connection form (address, power, consumption type, reason, documents)
- [ ] 6.6 Implement outage notification settings form (delivery method: email/SMS, notification type)
- [ ] 6.7 Implement contract change form (change type selector, details, documents)
- [ ] 6.8 Implement energy sharing form (metering point, sharing model, EAN list, documents)
- [ ] 6.9 Implement meter reading form (metering point, date, VT/NT values)
- [ ] 6.10 Create file upload component (drag-drop, format/size validation)
- [ ] 6.11 Implement form validation (client-side: required fields, format, range; server-side: all)
- [ ] 6.12 Implement form submission with loading state
- [ ] 6.13 Generate unique request ID (PRED-2026-000123 format)
- [ ] 6.14 Send confirmation email with request details and processing time

## 7. Request Tracking (Sledování žádostí)

- [ ] 7.1 Create Requests List page (table: request ID, service type, metering point, date, status)
- [ ] 7.2 Implement filters (by service type, status, metering point)
- [ ] 7.3 Implement sorting (by submission date)
- [ ] 7.4 Create Request Detail page layout
- [ ] 7.5 Implement status timeline component (steps: Přijato → Formální kontrola → Technická kontrola → Rozhodnutí → Realizace)
- [ ] 7.6 Display submitted data summary (read-only)
- [ ] 7.7 Display uploaded documents with download links
- [ ] 7.8 Implement rejection display in timeline with reason and suggested actions
- [ ] 7.9 Create "Download Confirmation" PDF generation
- [ ] 7.10 Implement status update polling (or webhook if backend supports)
- [ ] 7.11 Send email notifications on status changes
- [ ] 7.12 Implement request cancellation (if in early stages)
- [ ] 7.13 Add "Contact Support" section with email/phone/chat link

## 8. Account Management (Správa účtu)

- [ ] 8.1 Create Account Settings page with tabs (Personal info, Password, Notifications, User Management)
- [ ] 8.2 Implement Personal Information tab (display and edit: name, email, phone, billing address)
- [ ] 8.3 Implement Password Change tab (current password verification, new password strength validation)
- [ ] 8.4 Implement Notification Settings tab (toggles for outage, request status, marketing, billing, system alerts)
- [ ] 8.5 Implement Additional User Management tab (list, invite form, edit permissions, revoke access)
- [ ] 8.6 Implement invitation email with 7-day expiring link
- [ ] 8.7 Implement granular permissions (read-only, submit requests, unlimited/expiring access)
- [ ] 8.8 Implement account deletion with 30-day reactivation window
- [ ] 8.9 Implement data anonymization after 30-day deletion window

## 9. Portal Layout and Navigation (Layout a navigace)

- [ ] 9.1 Create Header component (logo, profile identity, logged-in user, menu)
- [ ] 9.2 Create Sidebar Navigation component with sections (Odběrná místa, Potřebuji zařídit, Moje žádosti, Účet)
- [ ] 9.3 Implement responsive sidebar (hamburger menu on mobile <768px)
- [ ] 9.4 Create Footer component (copyright, links, contact)
- [ ] 9.5 Create Dashboard/Homepage with summary cards (metering points, open requests, notifications)
- [ ] 9.6 Implement breadcrumb navigation
- [ ] 9.7 Implement active menu item highlighting and scroll position persistence

## 10. Design System and Components (Komponenty a design)

- [ ] 10.1 Create Button component (primary #1a2f6e, secondary #5a7a2b, variants: hover, disabled)
- [ ] 10.2 Create TextInput component with error states and labels
- [ ] 10.3 Create Select/Dropdown component
- [ ] 10.4 Create Checkbox and Radio button components
- [ ] 10.5 Create Card and Panel container components
- [ ] 10.6 Create Alert components (error, success, warning, info with toast notifications)
- [ ] 10.7 Create Badge/Status components (color-coded: active, inactive, pending, in-progress, completed, rejected)
- [ ] 10.8 Create Table component with sorting and filtering
- [ ] 10.9 Create Modal/Dialog component
- [ ] 10.10 Create Loading Spinner and Skeleton loaders
- [ ] 10.11 Implement accessibility (WCAG 2.1 AA: keyboard navigation, screen reader, color contrast 4.5:1)
- [ ] 10.12 Create responsive type scale (mobile 16px base, desktop 14px base)
- [ ] 10.13 Implement spacing system (4px baseline)
- [ ] 10.14 Document component library (Storybook or similar)

## 11. API Integration and Backend Endpoints

- [ ] 11.1 Implement GET /api/auth/user (get current user)
- [ ] 11.2 Implement POST /api/auth/register (registration endpoint)
- [ ] 11.3 Implement POST /api/auth/verify-sms (SMS OTP verification)
- [ ] 11.4 Implement POST /api/auth/login (login endpoint with rate limiting)
- [ ] 11.5 Implement POST /api/auth/logout (logout/session invalidation)
- [ ] 11.6 Implement POST /api/auth/password-reset (password recovery)
- [ ] 11.7 Implement GET /api/metering-points (list user's metering points)
- [ ] 11.8 Implement GET /api/metering-points/:id (get metering point details)
- [ ] 11.9 Implement GET /api/metering-points/:id/consumption (get consumption data for graph)
- [ ] 11.10 Implement POST /api/service-requests (submit new service request)
- [ ] 11.11 Implement GET /api/service-requests (list user's requests)
- [ ] 11.12 Implement GET /api/service-requests/:id (get request detail with timeline)
- [ ] 11.13 Implement PATCH /api/service-requests/:id/cancel (cancel request)
- [ ] 11.14 Implement GET /api/account (get user account info)
- [ ] 11.15 Implement PATCH /api/account (update personal info)
- [ ] 11.16 Implement PATCH /api/account/password (change password)
- [ ] 11.17 Implement GET /api/account/notifications (get notification settings)
- [ ] 11.18 Implement PATCH /api/account/notifications (update notification settings)
- [ ] 11.19 Implement GET /api/account/additional-users (list additional users)
- [ ] 11.20 Implement POST /api/account/additional-users (send invitation)
- [ ] 11.21 Implement PATCH /api/account/additional-users/:id (update permissions)
- [ ] 11.22 Implement DELETE /api/account/additional-users/:id (revoke access)

## 12. Email Notifications

- [ ] 12.1 Set up email service (Sendgrid, Mailgun, or similar)
- [ ] 12.2 Create email templates (registration confirmation, password reset, request confirmation, status updates, rejection notification)
- [ ] 12.3 Implement email sending on registration (confirmation)
- [ ] 12.4 Implement email sending on password reset
- [ ] 12.5 Implement email sending on service request submission
- [ ] 12.6 Implement email sending on request status changes
- [ ] 12.7 Implement email sending on additional user invitation
- [ ] 12.8 Implement email sending on access revocation

## 13. Security and Performance

- [ ] 13.1 Implement rate limiting on API endpoints (prevent brute force)
- [ ] 13.2 Implement CORS configuration (allow only trusted origins)
- [ ] 13.3 Implement input validation and sanitization (prevent XSS/SQL injection)
- [ ] 13.4 Implement HTTPS enforcement
- [ ] 13.5 Implement Content Security Policy headers
- [ ] 13.6 Implement secure password hashing (bcrypt, Argon2)
- [ ] 13.7 Implement request/response logging for audit trail
- [ ] 13.8 Optimize images (WebP, responsive srcsets, lazy loading)
- [ ] 13.9 Implement code splitting and lazy route loading
- [ ] 13.10 Set up Sentry or similar for error tracking
- [ ] 13.11 Implement Lighthouse score optimization (FCP <1.5s, LCP <2.5s)
- [ ] 13.12 Implement database backup strategy

## 14. Testing

- [ ] 14.1 Set up Jest for unit testing
- [ ] 14.2 Set up Cypress or Playwright for end-to-end testing
- [ ] 14.3 Write unit tests for utility functions and form validation
- [ ] 14.4 Write E2E tests for critical flows (registration, login, service request submission)
- [ ] 14.5 Implement manual QA checklist (responsive design, accessibility, browser compatibility)
- [ ] 14.6 Load testing (expected user volume: 1000+ concurrent users)
- [ ] 14.7 Security testing (OWASP Top 10, penetration testing)
- [ ] 14.8 Accessibility testing (keyboard navigation, screen reader, color contrast)

## 15. Deployment and Monitoring

- [ ] 15.1 Set up Vercel project and connect GitHub repository
- [ ] 15.2 Configure environment variables for staging and production
- [ ] 15.3 Set up preview deployments for pull requests
- [ ] 15.4 Configure Vercel analytics and monitoring
- [ ] 15.5 Set up error tracking (Sentry)
- [ ] 15.6 Set up uptime monitoring (Uptimerobot or Vercel monitoring)
- [ ] 15.7 Create deployment checklist and runbook
- [ ] 15.8 Plan blue-green deployment strategy
- [ ] 15.9 Test rollback procedures
- [ ] 15.10 Set up database backup and recovery procedures

## 16. Documentation and Launch

- [ ] 16.1 Create user documentation / help pages
- [ ] 16.2 Create API documentation (Swagger/OpenAPI)
- [ ] 16.3 Create deployment runbook
- [ ] 16.4 Create incident response procedures
- [ ] 16.5 Prepare launch announcement and communication
- [ ] 16.6 Set up customer support documentation
- [ ] 16.7 Plan training for PREdistribuce support team
- [ ] 16.8 Create analytics dashboard for monitoring portal usage
