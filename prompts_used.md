# Part 4: AI-Assisted CRM Architecture Exploration

## Technology Stack

**Front-End:**
- HTML
- CSS
- JavaScript
- jQuery
- Bootstrap

**Server-Side:**
- PHP

**Database:**
- MySQL

---

## 1. Functional Modules

A CRM built with PHP/MySQL/Bootstrap stack should include the following core modules:

### Core CRM Modules

**1. Authentication Module**
- User login/logout functionality
- Password reset and recovery
- Session management
- User account activation

**2. Contacts Module**
- Store individual contact information (name, email, phone, address, company)
- View contact history
- Add notes to contacts
- Link contacts to accounts and opportunities
- Contact search and filtering

**3. Accounts Module**
- Manage company/organization records
- Track account status and industry
- Link multiple contacts to one account
- View account interaction history
- Account value tracking

**4. Leads Module**
- Capture new prospective customers
- Track lead source (web form, email, phone, referral)
- Assign lead scores
- Track lead status (new, qualified, contacted, converted, rejected)
- Convert leads to opportunities

**5. Opportunities Module**
- Manage sales opportunities/deals
- Track deal value and probability
- Manage sales stage (prospecting, qualification, proposal, negotiation, closed won/lost)
- Set close dates
- Link to accounts and contacts
- Sales pipeline management

**6. Activities Module**
- Log interactions: calls, emails, meetings
- Track activity date and time
- Assign activities to team members
- Link activities to contacts/opportunities

**7. Tasks Module**
- Create to-do items for sales team
- Set due dates and priorities
- Assign tasks to team members
- Track task completion status
- Link tasks to opportunities/contacts

**8. Reports Module**
- Sales pipeline reports
- Team performance reports
- Contact and lead reports
- Opportunity forecasting reports
- Custom report builder

**9. User Management Module**
- Create and manage user accounts
- Assign roles and permissions
- Track user activity logs
- User status management

**10. Dashboard Module**
- Personalized dashboards for different roles
- Key performance indicators (KPIs)
- Sales pipeline visualization
- Recent activity feeds
- Quick action widgets

---

## 2. Database Design

### Core Tables Required

**users**
- user_id (PRIMARY KEY)
- username (UNIQUE)
- email (UNIQUE)
- password_hash (bcrypt hashed)
- first_name
- last_name
- role_id (FOREIGN KEY to roles)
- is_active (BOOLEAN)
- created_at (TIMESTAMP)
- updated_at (TIMESTAMP)
- last_login (TIMESTAMP)

**roles**
- role_id (PRIMARY KEY)
- role_name (admin, sales_manager, sales_rep, support_agent, viewer)
- permissions (JSON or separate permissions table)
- created_at (TIMESTAMP)

**contacts**
- contact_id (PRIMARY KEY)
- first_name
- last_name
- email (UNIQUE)
- phone
- mobile_phone
- company_name
- job_title
- address
- city
- state
- postal_code
- country
- account_id (FOREIGN KEY to accounts)
- created_by (FOREIGN KEY to users)
- created_at (TIMESTAMP)
- updated_at (TIMESTAMP)
- notes (TEXT)

**accounts**
- account_id (PRIMARY KEY)
- account_name
- industry
- account_status (prospect, active, inactive)
- annual_revenue
- number_of_employees
- website
- primary_contact_id (FOREIGN KEY to contacts)
- billing_address
- created_by (FOREIGN KEY to users)
- created_at (TIMESTAMP)
- updated_at (TIMESTAMP)

**leads**
- lead_id (PRIMARY KEY)
- lead_name
- email
- phone
- company
- lead_source (web form, email, phone, referral, social, marketing_campaign)
- lead_status (new, qualified, contacted, converted, rejected)
- lead_score (0-100)
- assigned_to (FOREIGN KEY to users)
- created_at (TIMESTAMP)
- updated_at (TIMESTAMP)
- converted_to_contact_id (FOREIGN KEY to contacts, nullable)

**opportunities**
- opportunity_id (PRIMARY KEY)
- opportunity_name
- account_id (FOREIGN KEY to accounts)
- primary_contact_id (FOREIGN KEY to contacts)
- opportunity_value (DECIMAL)
- stage (prospecting, qualification, proposal, negotiation, closed_won, closed_lost)
- probability (0-100)
- close_date (DATE)
- assigned_to (FOREIGN KEY to users)
- created_at (TIMESTAMP)
- updated_at (TIMESTAMP)
- notes (TEXT)

**activities**
- activity_id (PRIMARY KEY)
- activity_type (call, email, meeting, other)
- subject
- description (TEXT)
- activity_date (DATETIME)
- duration_minutes (INT, nullable for non-call activities)
- contact_id (FOREIGN KEY to contacts)
- opportunity_id (FOREIGN KEY to opportunities, nullable)
- related_to (contacts, accounts, leads, opportunities)
- created_by (FOREIGN KEY to users)
- created_at (TIMESTAMP)

**tasks**
- task_id (PRIMARY KEY)
- task_title
- description (TEXT)
- due_date (DATE)
- priority (low, medium, high)
- status (open, in_progress, completed, cancelled)
- assigned_to (FOREIGN KEY to users)
- related_to (contacts, accounts, opportunities)
- related_id (references id in related_to table)
- created_by (FOREIGN KEY to users)
- created_at (TIMESTAMP)
- completed_at (TIMESTAMP, nullable)

**audit_logs**
- log_id (PRIMARY KEY)
- user_id (FOREIGN KEY to users)
- action (create, read, update, delete)
- table_name
- record_id
- old_values (JSON)
- new_values (JSON)
- timestamp (TIMESTAMP)
- ip_address

---

## 3. Useful Libraries

### Frontend Libraries

**Bootstrap 5**
- Purpose: Responsive UI framework, pre-built components, grid system
- Use: Create responsive layouts, forms, buttons, navigation
- Installation: Include via CDN or npm

**jQuery**
- Purpose: Simplified DOM manipulation, event handling, AJAX requests
- Use: Form validation, dynamic content loading, user interactions
- Installation: Include via CDN or npm

**DataTables** (https://datatables.net/)
- Purpose: Advanced table management with sorting, filtering, pagination
- Use: Display contacts, leads, opportunities in sortable/searchable tables
- Features: Server-side processing, export to CSV/PDF

**Chart.js** (https://www.chartjs.org/)
- Purpose: Simple yet flexible JavaScript charting library
- Use: Display sales pipeline charts, revenue forecasts, team performance metrics
- Features: Bar charts, pie charts, line graphs, responsive

**Moment.js** (or date-fns)
- Purpose: Parse, validate, manipulate, and display dates
- Use: Format dates consistently across the application
- Features: Timezone support, locale support

**Popper.js + Tooltip.js**
- Purpose: Positioning library for tooltips and popovers
- Use: Provide helpful context and information on hover
- Works with Bootstrap's tooltip/popover components

### Backend Libraries (PHP)

**Composer** (Dependency Manager)
- Purpose: Manage PHP package dependencies
- Use: Install and update libraries automatically
- Installation: Composer package manager

**PDO or MySQLi**
- Purpose: Database abstraction layer for secure database connections
- Use: Prepared statements to prevent SQL injection
- Built-in: Part of PHP standard library

**PHPMailer** (https://github.com/PHPMailer/PHPMailer)
- Purpose: Robust email sending library
- Use: Send password reset emails, notification emails, activity summaries
- Features: HTML emails, attachments, multiple protocols (SMTP, sendmail, mail)

**password_hash/password_verify (PHP Built-in)**
- Purpose: Secure password hashing using bcrypt algorithm
- Use: Hash user passwords during registration and login
- Built-in: Part of PHP standard library (PHP 5.5+)

**PHPDotenv** (https://github.com/vlucas/phpdotenv)
- Purpose: Load environment variables from .env file
- Use: Store sensitive configuration (database credentials, API keys) securely
- Prevents hardcoding sensitive data in code

**FPDF** or **TCPDF** (PHP PDF Libraries)
- Purpose: Generate PDF documents
- Use: Create report exports, invoice generation, document downloads
- Features: Tables, images, custom fonts

**Monolog** (https://github.com/Seldaek/monolog)
- Purpose: Logging library for debugging and monitoring
- Use: Log errors, user actions, security events
- Features: Multiple log handlers (file, database, email)

**PHPUnit**
- Purpose: Unit testing framework
- Use: Write automated tests for critical functions
- Installation: Via Composer

---

## 4. Security Considerations

### Authentication

**Password Security:**
- Use bcrypt algorithm for password hashing (PHP's password_hash() function)
- Implement password strength requirements (minimum 8 characters, mix of uppercase, numbers, special characters)
- Hash passwords before storing in database
- Never store passwords in plain text
- Implement password reset functionality with secure tokens

**Session Management:**
- Use PHP sessions with secure session handlers
- Set session timeout (30-60 minutes of inactivity)
- Regenerate session ID after login to prevent session fixation attacks
- Implement HTTPS to encrypt session cookies
- Set secure and HttpOnly flags on cookies

**Multi-Factor Authentication (Nice-to-have):**
- Email-based verification on first login
- Optional TOTP (Time-based One-Time Password) for sensitive accounts

### Authorization

**Role-Based Access Control (RBAC):**
- Implement roles: Admin, Sales Manager, Sales Rep, Support Agent, Viewer
- Define permissions for each role:
  - Admin: Full access to all features
  - Sales Manager: View/manage team's opportunities and contacts
  - Sales Rep: View/manage own opportunities and assigned contacts
  - Support Agent: View/manage tickets and associated contacts
  - Viewer: Read-only access to specific data

**Access Control Implementation:**
- Check user role before displaying/allowing actions
- Prevent direct URL manipulation to access unauthorized data
- Validate permissions on both front-end (UX) and back-end (security)

### SQL Injection Prevention

**Use Prepared Statements:**
```php
// Secure: Using parameterized query
$stmt = $pdo->prepare("SELECT * FROM users WHERE email = ?");
$stmt->execute([$email]);

// or with named parameters
$stmt = $pdo->prepare("SELECT * FROM users WHERE email = :email");
$stmt->execute([':email' => $email]);
```

**Never Use String Interpolation:**
```php
// VULNERABLE - Never do this
$query = "SELECT * FROM users WHERE email = '$email'";

// Safe - Always use prepared statements
$stmt = $pdo->prepare("SELECT * FROM users WHERE email = ?");
$stmt->execute([$email]);
```

**Input Validation:**
- Validate email format using filter_var()
- Validate data types before processing
- Use whitelisting for expected inputs (e.g., only numbers, specific strings)
- Sanitize user inputs but validate on back-end

### Cross-Site Scripting (XSS) Prevention

**Output Encoding:**
- Use htmlspecialchars() when displaying user-generated content
- Encode all dynamic output before displaying in HTML
```php
// Safe: Escaping output
echo htmlspecialchars($user_input, ENT_QUOTES, 'UTF-8');
```

**Content Security Policy (CSP):**
- Implement CSP headers to restrict executable content
- Add to server configuration or PHP header:
```php
header("Content-Security-Policy: default-src 'self'; script-src 'self' trusted-cdn.com");
```

**Input Sanitization:**
- Strip HTML tags from user input if not needed
- Use filter_var() with appropriate filters
```php
$email = filter_var($email, FILTER_SANITIZE_EMAIL);
```

### Cross-Site Request Forgery (CSRF) Prevention

**CSRF Tokens:**
- Generate unique token for each form
- Include token in form and validate on submission
- Tokens should expire after use or time period

```php
// Generate token
$_SESSION['csrf_token'] = bin2hex(random_bytes(32));

// Include in form
<input type="hidden" name="csrf_token" value="<?php echo $_SESSION['csrf_token']; ?>">

// Validate on submission
if ($_POST['csrf_token'] !== $_SESSION['csrf_token']) {
    die('CSRF token validation failed');
}
```

**SameSite Cookie Flag:**
- Set SameSite=Strict or SameSite=Lax on session cookies
```php
session_set_cookie_params([
    'samesite' => 'Strict',
    'secure' => true,  // HTTPS only
    'httponly' => true // No JavaScript access
]);
```

### Data Privacy

**HTTPS/TLS:**
- Always use HTTPS to encrypt data in transit
- Obtain SSL certificate (free via Let's Encrypt)
- Redirect all HTTP to HTTPS

**Data Encryption:**
- Encrypt sensitive data at rest (PCI DSS compliance for payment data)
- Use encryption for personally identifiable information (PII)

**Database Backups:**
- Regular automated backups
- Store backups securely (separate server/cloud)
- Test backup restoration process

**Audit Logging:**
- Log all critical actions (login, data modifications, admin actions)
- Store logs securely with tamper protection
- Monitor logs for suspicious activity

**User Data Access:**
- Implement principle of least privilege
- Users only see data they should access
- Log all data access for compliance

---

## 5. MVP (Minimum Viable Product) Proposal

### Version 1: Core CRM Functionality

The MVP should focus on essential features that provide immediate business value:

**Included Features:**

1. **Authentication System** (Week 1-2)
   - User login/logout
   - Password reset
   - Session management
   - Role-based access control

2. **Contacts Management** (Week 2-3)
   - Create, read, update, delete contacts
   - Search and filter contacts
   - View contact history
   - Export contacts list

3. **Leads Management** (Week 3-4)
   - Create and track leads
   - Lead assignment to sales reps
   - Lead status tracking (new, qualified, converted)
   - Convert leads to contacts

4. **Opportunities/Deals** (Week 4-5)
   - Create and track opportunities
   - Manage sales pipeline stages
   - Deal value and probability tracking
   - Basic opportunity reports

5. **Tasks** (Week 5-6)
   - Create and assign tasks
   - Task due date tracking
   - Task completion status
   - Task prioritization (low, medium, high)

6. **Dashboard** (Week 6-7)
   - Sales pipeline overview
   - Recent activity feed
   - Key metrics (total opportunities, pipeline value)
   - Quick action buttons

7. **Reporting** (Week 7-8)
   - Sales pipeline report
   - Team performance report
   - Opportunity forecast report
   - Export to CSV

**Not Included in MVP:**
- Marketing automation
- Email integration
- Advanced analytics
- Workflow automation
- Mobile app
- Third-party integrations
- Advanced forecasting with AI

**MVP Timeline:** 8 weeks
**MVP Team:** 2-3 developers, 1 QA tester

**Success Metrics:**
- All core CRUD operations working
- Core security implemented
- Load time < 2 seconds for key pages
- 95%+ uptime
- User adoption from 5-10 initial users

---

## 6. Architecture Diagram

### System Architecture: PHP/MySQL/Bootstrap CRM

```
┌─────────────────────────────────────────────────────────────────┐
│                         CLIENT LAYER                              │
│                    (Browser-Based Interface)                      │
├─────────────────────────────────────────────────────────────────┤
│  HTML/CSS/JavaScript/jQuery/Bootstrap                             │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Dashboard │ Contacts │ Leads │ Opportunities │ Tasks    │   │
│  │  Reports  │ Activities │ Settings │ User Management      │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                    │
│  DataTables (sorting, filtering, pagination)                     │
│  Chart.js (visualizations)                                        │
│  jQuery (AJAX requests, DOM manipulation)                        │
│  Bootstrap (responsive UI components)                             │
└─────────────────────────────────────────────────────────────────┘
                              ↓ (AJAX/HTTP)
┌─────────────────────────────────────────────────────────────────┐
│                    APPLICATION LAYER                              │
│                  (PHP Web Application)                            │
├─────────────────────────────────────────────────────────────────┤
│  ┌──────────────────────────────────────────────────────────┐   │
│  │ Router/Controller Layer                                  │   │
│  │ ├─ AuthController (login, logout, password reset)       │   │
│  │ ├─ ContactController (CRUD operations)                  │   │
│  │ ├─ LeadController (lead management)                     │   │
│  │ ├─ OpportunityController (sales pipeline)               │   │
│  │ ├─ TaskController (task management)                     │   │
│  │ ├─ ReportController (generate reports)                  │   │
│  │ └─ UserController (user & role management)              │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                    │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │ Business Logic Layer                                     │   │
│  │ ├─ AuthService (authentication, authorization)          │   │
│  │ ├─ ContactService (contact operations)                  │   │
│  │ ├─ LeadService (lead operations)                        │   │
│  │ ├─ SalesService (opportunity management)                │   │
│  │ ├─ ReportService (report generation)                    │   │
│  │ └─ SecurityService (encryption, hashing, tokens)        │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                    │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │ Utility Libraries                                        │   │
│  │ ├─ PDO/MySQLi (secure database connections)             │   │
│  │ ├─ PHPMailer (email sending)                            │   │
│  │ ├─ PHPDotenv (environment configuration)                │   │
│  │ ├─ Monolog (logging)                                     │   │
│  │ ├─ FPDF (PDF generation)                                │   │
│  │ └─ PHPUnit (unit testing)                               │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                              ↓ (SQL Queries)
┌─────────────────────────────────────────────────────────────────┐
│                      DATABASE LAYER                               │
│                    (MySQL Database)                               │
├─────────────────────────────────────────────────────────────────┤
│  Tables:                                                          │
│  ├─ users, roles (authentication & authorization)               │
│  ├─ contacts, accounts (customer data)                          │
│  ├─ leads (prospective customers)                               │
│  ├─ opportunities (sales pipeline)                              │
│  ├─ activities, tasks (interactions & actions)                  │
│  ├─ audit_logs (security & compliance)                          │
│  └─ reports (generated reports storage)                         │
│                                                                    │
│  Prepared Statements & Parameterized Queries                     │
│  Indexes on frequently queried columns                           │
│  Proper foreign key relationships                                │
│  ACID compliance for data integrity                              │
└─────────────────────────────────────────────────────────────────┘
```

### Data Flow Example: Creating a New Contact

```
User Input (Browser)
       ↓
Bootstrap Form + jQuery Validation
       ↓
AJAX Request to /api/contacts/create
       ↓
PHP Router: Route Request to ContactController
       ↓
AuthService: Verify User Authorization
       ↓
Input Validation & Sanitization
       ↓
ContactService: Process Business Logic
       ↓
PDO: Execute Prepared Statement
       ↓
MySQL: Insert Contact Record
       ↓
AuditLog: Log the action
       ↓
Return JSON Response
       ↓
jQuery: Process Response
       ↓
Update UI, Show Success Message
       ↓
Refresh Contacts Table via DataTables
```

### Security Layers in Architecture

```
┌─────────────────────────────────────┐
│   HTTPS/TLS Encryption               │ (Data in transit)
└─────────────────────────────────────┘
                ↓
┌─────────────────────────────────────┐
│   CSRF Token Validation              │ (Form submission)
└─────────────────────────────────────┘
                ↓
┌─────────────────────────────────────┐
│   Authentication (Login)             │ (User identity)
└─────────────────────────────────────┘
                ↓
┌─────────────────────────────────────┐
│   Authorization (Role-based)         │ (User permissions)
└─────────────────────────────────────┘
                ↓
┌─────────────────────────────────────┐
│   Input Validation & Sanitization    │ (XSS prevention)
└─────────────────────────────────────┘
                ↓
┌─────────────────────────────────────┐
│   Prepared Statements & Parameters   │ (SQL injection prevention)
└─────────────────────────────────────┘
                ↓
┌─────────────────────────────────────┐
│   Database Encryption (at rest)      │ (Data security)
└─────────────────────────────────────┘
                ↓
┌─────────────────────────────────────┐
│   Audit Logging & Monitoring         │ (Compliance & detection)
└─────────────────────────────────────┘
```

---

## Summary

**Architecture Overview:**
- **Three-tier architecture:** Presentation (HTML/CSS/JS) → Application (PHP) → Data (MySQL)
- **Security-first design:** All layers include security mechanisms
- **Scalable framework:** Libraries and modular design allow growth
- **MVP approach:** Start with core functionality, add features based on user feedback

**Key Design Principles:**
- Separation of concerns (controllers, services, utilities)
- DRY (Don't Repeat Yourself) - reusable functions
- Prepared statements for all database queries
- Output encoding for all user-generated content
- Role-based access control for authorization
- Comprehensive logging for audit trails

**Technology Advantages:**
- **PHP:** Widely supported hosting, easy deployment, mature ecosystem
- **MySQL:** Reliable, scalable, industry-standard RDBMS
- **Bootstrap:** Responsive design without extensive CSS
- **jQuery:** Minimal learning curve, strong DOM manipulation
- **Libraries:** Reduce development time, battle-tested security

**Development Ready:** With this architecture, development can begin with clear module separation, known security requirements, and defined database schema.
