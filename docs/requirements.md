# The Big J — Requirements

## 1. Project Overview

The Big J is a web-based job application tracking system. It will allow users to organize job applications, track application progress, save notes, mark important opportunities as favorites, and view their job-search activity through a dashboard.

The system will provide job seekers with one centralized location for managing their application process.

## 2. Problem Statement

Job seekers often apply to positions through multiple websites, including LinkedIn, Indeed, Handshake, and company career pages. This makes it difficult to remember which jobs they applied for, what stage each application is in, and what information they need to review before an interview.

The Big J will solve this problem by allowing users to manually record, organize, update, and monitor their job applications from one platform.

## 3. Target Users

The primary target users are:

- College students searching for internships or full-time positions
- Graduating students preparing to enter the workforce
- Recent college graduates
- Entry-level job seekers
- Career changers applying for new types of positions

## 4. User Personas

### Persona 1: Lisa Simpson — Graduating Accounting Student

- **Age:** 22
- **Occupation:** College student graduating with an Accounting degree
- **Background:** Aisha is in her final semester and is applying for entry-level accounting and financial analyst positions. She is applying through company websites, university career services, and job boards.
- **Goals:**
    - Track all applications before graduation
    - Record interview stages and deadlines
    - Save notes about companies and job requirements
    - Remember which resume version was used
- **Frustrations:**
    - Applies to many companies at the same time
    - Uses multiple spreadsheets and browser tabs
    - Forgets details about applications when interviews are scheduled
- **Needs from The Big J:** A centralized dashboard, application statuses, notes, favorites, filtering, and reminders.

### Persona 2: Gojo Satoru — Marketing Coordinator

- **Age:** 28
- **Occupation:** Marketing Coordinator
- **Background:** David is looking for a new marketing position while working at his current company. He applies to advertising agencies, nonprofit organizations, and private companies.
- **Goals:**
    - Organize applications from different websites
    - Save notes about each company
    - Track interview stages
    - Prioritize his favorite opportunities
- **Frustrations:**
    - Uses spreadsheets and browser bookmarks
    - Forgets important details about job postings
    - Sometimes misses follow-up dates
- **Needs from The Big J:** Search, filtering, favorites, interview notes, and follow-up reminders.

### Persona 3: Ippo Makunouchi — Construction Project Manager

- **Age:** 42
- **Occupation:** Construction Project Manager
- **Background:** Carlos has several years of experience and is searching for project management positions at construction companies. He applies through recruiters, company websites, and professional connections.
- **Goals:**
    - Manage multiple applications
    - Track recruiter and employer contact information
    - Record interview rounds and notes
    - Compare salary, location, and benefits
- **Frustrations:**
    - Has many applications at different stages
    - Finds recruiter information difficult to organize
    - Needs to remember details from previous interviews
- **Needs from The Big J:** Application management, status tracking, notes, contact information, and dashboard analytics.

### Persona 4: Marceline Abadeer — Recent Graduate

- **Age:** 24
- **Occupation:** Recent graduate applying for elementary school teaching positions
- **Background:** Elena recently graduated with an Education degree and is applying to schools and school districts in different cities. She is tracking applications, interviews, certifications, and follow-up tasks.
- **Goals:**
    - Organize applications from different school districts
    - Track interview rounds and hiring stages
    - Save notes about each school
    - Remember certification and document requirements
- **Frustrations:**
    - Applies to multiple schools with different requirements
    - Has difficulty remembering details about each position
    - Uses separate documents to track interviews and follow-ups
- **Needs from The Big J:** Application status tracking, notes, favorites, filtering, reminders, and a progress dashboard.
## 5. Use Cases

### Use Case 1: Create and Access an Account

**Primary Actor:** User

The user creates an account or logs in to securely access their job applications.

**Main Flow:**

1. The user opens the registration or login page.
2. The user enters their account information.
3. The system validates the information.
4. The system creates or authenticates the account.
5. The system redirects the user to the dashboard.

**Postcondition:** The user is authenticated and can access their private application data.

---

### Use Case 2: Manage Job Applications

**Primary Actor:** User

The user creates, views, edits, and deletes job applications.

**Main Flow:**

1. The user opens the applications page.
2. The user creates a new application.
3. The user enters the application details.
4. The system validates and saves the information.
5. The application appears in the user's application list.
6. The user can later view, edit, or delete the application.

**Postcondition:** The application is saved, updated, or deleted and is associated with the correct user.

---

### Use Case 3: Track Application Progress

**Primary Actor:** User

The user updates an application's status to track progress through the hiring process.

**Main Flow:**

1. The user opens an application.
2. The user selects a new status.
3. The system validates the status.
4. The system saves the updated status.
5. The new status appears on the application and dashboard.

**Supported Statuses:**

- Saved
- Applied
- Interview
- Offer
- Rejected
- Withdrawn

---

### Use Case 4: Search, Filter, and Favorite Applications

**Primary Actor:** User

The user searches for applications, filters them by specific criteria, and marks important applications as favorites.

**Main Flow:**

1. The user opens the applications page.
2. The user searches by company or job title.
3. The user filters applications by status or other criteria.
4. The user marks an important application as a favorite.
5. The system displays the matching applications.

**Postcondition:** The user can quickly locate important or specific applications.

---

### Use Case 5: Prepare for an Application or Interview

**Primary Actor:** User

The user creates and manages notes related to a job application.

**Main Flow:**

1. The user opens an application.
2. The user adds preparation notes.
3. The system saves the notes.
4. The user can view, edit, or delete the notes later.
5. The user reviews the notes before an interview or follow-up.

**Example Notes:**

- Company research
- Required technologies
- Interview questions
- Questions to ask the interviewer
- Follow-up information

## 6. User Stories

### Authentication

- As a user, I want to create an account so I can securely manage my applications.
- As a user, I want to log in so I can access my private application data.
- As a user, I want to log out so my account remains secure.

### Application Management

- As a user, I want to create a job application so I can track a position I applied for.
- As a user, I want to view my applications so I can see my current job-search activity.
- As a user, I want to edit an application so I can keep its information accurate.
- As a user, I want to delete an application so I can remove applications I no longer need.

### Status Tracking

- As a user, I want to update an application status so I can track my progress.
- As a user, I want to see the current status of each application so I know which opportunities are active.

### Search and Favorites

- As a user, I want to search by company or job title so I can quickly find an application.
- As a user, I want to filter applications by status so I can quickly find interviews or offers.
- As a user, I want to mark an application as a favorite so I can easily find important opportunities.

### Notes and Dashboard

- As a user, I want to add notes to an application so I can prepare for interviews.
- As a user, I want to view a dashboard so I can understand my overall application progress.

## 7. Functional Requirements

### Authentication

- FR-1: The system shall allow users to create an account.
- FR-2: The system shall allow registered users to log in and log out.
- FR-3: The system shall securely store user passwords.
- FR-4: The system shall prevent unauthenticated users from accessing private application data.
- FR-5: The system shall ensure that users can only access their own data.

### Application Management

- FR-6: The system shall allow users to create job applications.
- FR-7: The system shall allow users to view their job applications.
- FR-8: The system shall allow users to update their job applications.
- FR-9: The system shall allow users to delete their job applications.
- FR-10: The system shall store the company, job title, application date, status, and optional job details.

### Status Tracking

- FR-11: The system shall allow users to update application statuses.
- FR-12: The system shall support Saved, Applied, Interview, Offer, Rejected, and Withdrawn statuses.
- FR-13: The system shall display the current status for each application.

### Search, Filtering, and Favorites

- FR-14: The system shall allow users to search applications by company name and job title.
- FR-15: The system shall allow users to filter applications by status.
- FR-16: The system shall allow users to mark and unmark applications as favorites.
- FR-17: The system shall allow users to view only their favorite applications.

### Notes and Dashboard

- FR-18: The system shall allow users to add notes to applications.
- FR-19: The system shall allow users to edit and delete their notes.
- FR-20: The system shall display the total number of applications on the dashboard.
- FR-21: The system shall display applications grouped by status on the dashboard.
- FR-22: The dashboard shall update when application data changes.

## 8. Acceptance Criteria

### Authentication

- Users can register with a valid name, email, and password.
- The system rejects duplicate email addresses.
- Passwords are not stored as plain text.
- Users can log in with valid credentials.
- Invalid credentials produce an error message.
- Users can log out successfully.

### Application CRUD

- Users can create an application with all required fields.
- Users can view all applications belonging to their account.
- Users can edit their own applications.
- Users can delete their own applications after confirmation.
- Users cannot view, edit, or delete another user's applications.

### Status Tracking

- Users can select a supported status.
- The selected status is saved to the database.
- The updated status appears in the application list.
- Dashboard status counts update after a status change.

### Search, Filtering, and Favorites

- Users can search applications by company or job title.
- Users can filter applications by status.
- Users can clear filters and view all applications.
- Users can mark and unmark applications as favorites.
- Users can view a list containing only favorite applications.

### Notes and Dashboard

- Users can create notes for their own applications.
- Users can edit and delete their notes.
- Notes remain available after the user logs out and logs back in.
- The dashboard displays accurate application totals.
- The dashboard displays accurate status totals.

## 9. Non-Functional Requirements

- The system shall protect user data through authentication and authorization.
- The system shall securely hash user passwords.
- The system shall validate user input before saving data.
- The system shall provide clear error messages.
- The system shall use a relational database to store application data.
- The system shall provide a responsive browser-based interface.
- The system shall use consistent navigation throughout the application.
- The system should provide reasonable response times for common actions.
- The system shall maintain user data after logout.
- The codebase shall be organized so future features can be added easily.

## 10. V1 Scope

Version 1 will include:

- User registration and login
- User logout
- Application creation
- Application viewing
- Application editing
- Application deletion
- Application status tracking
- Search and filtering
- Favorite applications
- Application notes
- Basic dashboard statistics

The MVP will focus on manually entered job applications. Automatic job importing, email notifications, and calendar integrations will not be included in Version 1.

## 11. Future Features

Future versions may include:

- Interview scheduling
- Interview-round tracking
- Recruiter and interviewer contact management
- Application and interview reminders
- Job-search analytics
- Resume and cover-letter tracking
- Email notifications
- Calendar integration
- Resume uploads
- Job importing from external platforms
- Custom application statuses
- Exporting application data

## 12. Assumptions and Constraints

### Assumptions

- Users will manually enter their job applications.
- Users will provide accurate application information.
- Users will access the system through a modern web browser.
- Each user will manage their own private application data.
- Users will use notes to record interview and company information.

### Constraints

- Version 1 will focus on browser-based use.
- The system will not automatically import jobs from LinkedIn, Indeed, or other websites.
- Email and push notifications will be future features.
- The project will initially support one user account per person.
- The first version will focus on a simple and manageable feature set.
- The application will not guarantee employment; it will only help users organize their job search.