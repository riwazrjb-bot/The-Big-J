# The Big J — Software Design

## 1. System Architecture

The Big J will use a client-server architecture because it requires centralized data storage, authentication, and authorization. Users will interact with the system through the frontend client, while the backend server will process requests, apply business logic, and manage access to user data.

The system will use a three-layer architecture:

1. **Presentation Layer:** Handles the user interface and user interactions.
2. **Application Layer:** Handles API routes, business logic, authentication, authorization, and sessions.
3. **Data Layer:** Stores and manages application data using PostgreSQL.

This separation improves organization, maintainability, and security. The frontend will not communicate directly with the database. All database requests will pass through the backend, which will verify the user's session and ensure that users can access only their own information.

The architecture will follow this structure:

    User
      ↓
    React Frontend
      ↓ HTTP Requests
    Node.js and Express Backend
      ↓ SQL Queries
    PostgreSQL Database

## 2. Technology Stack

### Frontend

- HTML
- CSS
- JavaScript
- React

The frontend will provide the user interface and handle interactions such as registration, login, creating applications, updating statuses, adding notes, searching, filtering, marking favorites, and viewing the dashboard.

### Backend

- Node.js
- Express.js
- REST API

The backend will handle API requests, application logic, routing, input validation, authentication, authorization, and communication with PostgreSQL.

### Authentication and Security

- Argon2
- express-session

Argon2 will securely hash user passwords before they are stored in PostgreSQL. The `express-session` library will manage authenticated user sessions and protect restricted routes.

### Database

- PostgreSQL

PostgreSQL will store:

- User accounts
- Job applications
- Application statuses
- Application notes
- Favorite application information

### Virtualization and Development Environment

- Vagrant
- VMware

Vagrant will be used to create and configure virtual machines. VMware will provide the virtualization environment used to run the virtual machines.

### Version Control and Project Management

- Git
- GitHub
- GitHub Issues
- GitHub Projects

## 3. Component Design

The Big J will be divided into frontend, backend, and database components.

| Component | Responsibility |
|---|---|
| React Frontend | Displays the interface and handles user interactions. |
| API Routes | Receive requests from the frontend and return responses. |
| Controllers | Process business logic for authentication, applications, notes, and dashboard data. |
| Authentication Middleware | Protects routes and verifies user sessions. |
| Session Management | Maintains authenticated user sessions. |
| Database Queries | Retrieve, create, update, and delete data in PostgreSQL. |
| PostgreSQL Tables | Store users, applications, and application notes. |

## 4. Data Model Overview

### Users

The users component stores account information for registered users.

A user will have:

- A unique ID
- A name
- An email address
- A securely hashed password
- An account creation date

### Job Applications

The applications component stores information about positions that users are tracking.

An application may include:

- Company name
- Job title
- Job posting URL
- Industry
- Location
- Employment type
- Application date
- Application status
- Favorite status
- Creation date
- Last updated date

Each application will belong to one user.

### Application Notes

The notes component stores preparation information related to a job application.

A note may include:

- A unique ID
- The related application ID
- Note content
- Creation date
- Last updated date

Each note will belong to one application and will be accessible only by the user who owns that application.

### Supported Application Statuses

The system will support the following statuses:

- Saved
- Applied
- Interview
- Offer
- Rejected
- Withdrawn

## 5. API Design

The Express backend will use REST API routes to receive requests from the frontend.

### Authentication Routes

- `POST /api/auth/register` — Creates a new user account.
- `POST /api/auth/login` — Authenticates a user and creates a session.
- `POST /api/auth/logout` — Ends the user's session.
- `GET /api/auth/me` — Returns information about the currently authenticated user.

### Application Routes

- `GET /api/applications` — Retrieves the user's applications.
- `GET /api/applications/:id` — Retrieves one specific application.
- `POST /api/applications` — Creates a new job application.
- `PATCH /api/applications/:id` — Updates an existing application.
- `DELETE /api/applications/:id` — Deletes an application.

### Filtering and Search

- `GET /api/applications?status=Interview` — Filters applications by status.
- `GET /api/applications?favorite=true` — Retrieves favorite applications.
- `GET /api/applications?search=teacher` — Searches applications by company name or job title.

### Note Routes

- `POST /api/applications/:id/notes` — Creates a note for an application.
- `PATCH /api/applications/:id/notes/:noteId` — Updates an application note.
- `DELETE /api/applications/:id/notes/:noteId` — Deletes an application note.

### Dashboard Routes

- `GET /api/dashboard/stats` — Retrieves the total number of applications and application counts grouped by status.

## 6. Authentication and Authorization Design

The Big J will use authentication and authorization to protect user accounts and application data.

### Authentication

Authentication verifies the identity of a user.

Users will be able to:

- Register for an account
- Log in using their email and password
- Remain logged in through a session
- Log out of their account

During registration, the user's password will be hashed using Argon2 before being stored in PostgreSQL. The original password will never be stored in the database.

During login, the backend will:

1. Find the user by email.
2. Compare the submitted password with the stored Argon2 hash.
3. Create a session if the credentials are valid.
4. Return a successful response to the frontend.

If the credentials are invalid, the backend will return an error without revealing whether the email or password was incorrect.

### Session Management

The application will use `express-session` to manage authenticated user sessions.

After a successful login, the backend will create a session containing the user's ID. The user's browser will send the session cookie with future requests. The backend will use the session to identify the user.

When the user logs out, the session will be destroyed.

Session cookies should use appropriate security settings, including:

- `httpOnly` to prevent client-side JavaScript from accessing the cookie
- `secure` when using HTTPS in production
- `sameSite` to help reduce cross-site request forgery risks

### Authorization

Authorization determines what an authenticated user is allowed to access.

The Big J will ensure that users can only view, update, or delete their own applications and notes. Every protected request will verify the user's session and compare the session user ID with the user ID associated with the requested data.

A user will not be allowed to access another user's application by changing the application ID in the URL.

### Authentication Middleware

Authentication middleware will run before protected routes. It will:

- Check whether a valid session exists.
- Reject unauthenticated requests.
- Identify the currently logged-in user.
- Attach the user ID to the request.
- Allow authenticated requests to continue.

Protected routes will include:

- `GET /api/applications`
- `GET /api/applications/:id`
- `POST /api/applications`
- `PATCH /api/applications/:id`
- `DELETE /api/applications/:id`
- `POST /api/applications/:id/notes`
- `PATCH /api/applications/:id/notes/:noteId`
- `DELETE /api/applications/:id/notes/:noteId`
- `GET /api/dashboard/stats`

### Security Requirements

- Passwords must never be stored as plain text.
- Passwords must be hashed using Argon2.
- Protected routes must require a valid session.
- Users must only access their own data.
- Authentication errors must not reveal sensitive account information.
- Session secrets and database credentials must be stored in environment variables.
- Secrets must not be committed to GitHub.

## 7. User Interface Design

The Big J will provide a simple and responsive browser-based interface for managing job applications.

### Landing Page

The landing page will introduce The Big J to visitors.

Features:

- Project name and description
- Explanation of the main features
- Login button
- Registration button

### Login Page

The login page will allow existing users to access their accounts.

Features:

- Email input
- Password input
- Login button
- Link to the registration page
- Error messages for invalid credentials

### Registration Page

The registration page will allow new users to create an account.

Features:

- Name input
- Email input
- Password input
- Confirm password input
- Registration button
- Link to the login page
- Validation messages

### Dashboard Page

The dashboard will be the main page shown after a user logs in.

Features:

- Total number of applications
- Application counts grouped by status
- Recent applications
- Favorite applications
- Search controls
- Status filters
- Add Application button
- List or cards displaying the user's applications

The dashboard will not contain the entire application form. The Add Application button will direct the user to a separate page.

### Add Application Page

The Add Application page will allow users to create a new job application.

Fields may include:

- Company name
- Job title
- Job posting URL
- Industry
- Location
- Employment type
- Application status
- Application date
- Favorite option
- Preparation notes

After submission, the application will be saved to PostgreSQL and the user will be redirected to the dashboard or application details page.

### Application Details Page

When a user selects an application from the dashboard, they will be taken to the application details page.

Features:

- Company name
- Job title
- Job posting URL
- Industry
- Location
- Employment type
- Current application status
- Application date
- Favorite status
- Preparation notes
- Edit button
- Delete button

### Edit Application Page

The Edit Application page will use the same form structure as the Add Application page.

Users will be able to:

- Update application information
- Change the application status
- Edit preparation notes
- Change the favorite status
- Save or cancel changes

### Application Notes

Users will be able to create and manage notes related to an application.

Features:

- Add a preparation note
- Edit an existing note
- Delete a note
- View notes on the application details page

Example notes may include:

- Company research
- Required qualifications
- Interview questions
- Questions to ask the interviewer
- Follow-up information

### Navigation

Authenticated users will have access to:

- Dashboard
- Add Application
- Logout

Unauthenticated users will have access to:

- Landing Page
- Login
- Registration

### Planned Frontend Routes

- `/` — Landing page
- `/login` — Login page
- `/register` — Registration page
- `/dashboard` — User dashboard
- `/applications/new` — Add application page
- `/applications/:id` — Application details page
- `/applications/:id/edit` — Edit application page

## 8. System Workflows

### User Registration

1. The user opens the registration page.
2. The user enters their name, email, password, and password confirmation.
3. The frontend validates the required fields.
4. The frontend sends a `POST /api/auth/register` request.
5. The backend checks whether the email is already registered.
6. The backend hashes the password using Argon2.
7. The backend stores the new user in PostgreSQL.
8. The backend returns a successful response.
9. The user is redirected to the login page.

If the input is invalid or the email already exists, the backend returns an error message.

### User Login

1. The user opens the login page.
2. The user enters their email and password.
3. The frontend sends a `POST /api/auth/login` request.
4. The backend searches for the user by email.
5. The backend compares the submitted password with the stored Argon2 hash.
6. If the credentials are valid, the backend creates a session.
7. The backend returns a successful response.
8. The user is redirected to the dashboard.

If the credentials are invalid, the user receives an error message and remains on the login page.

### Creating a Job Application

1. The authenticated user opens the dashboard.
2. The user selects the Add Application button.
3. The user enters the job application details.
4. The frontend validates the form.
5. The frontend sends a `POST /api/applications` request.
6. The authentication middleware verifies the user's session.
7. The backend validates the submitted data.
8. The backend stores the application using the authenticated user's ID.
9. The backend returns the newly created application.
10. The user is redirected to the dashboard or application details page.

### Viewing an Application

1. The user selects an application from the dashboard.
2. The frontend sends a `GET /api/applications/:id` request.
3. The authentication middleware verifies the user's session.
4. The backend confirms that the application belongs to the authenticated user.
5. The backend retrieves the application from PostgreSQL.
6. The application details are displayed to the user.

If the application does not belong to the user or does not exist, the backend returns an error response.

### Updating an Application Status

1. The user opens an application details page.
2. The user selects a new application status.
3. The frontend sends a `PATCH /api/applications/:id` request.
4. The authentication middleware verifies the user's session.
5. The backend confirms that the application belongs to the authenticated user.
6. The backend updates the status in PostgreSQL.
7. The backend returns the updated application.
8. The updated status appears on the application details page and dashboard.

### Adding an Application Note

1. The user opens an application details page.
2. The user enters preparation notes.
3. The frontend sends a `POST /api/applications/:id/notes` request.
4. The authentication middleware verifies the user's session.
5. The backend confirms that the application belongs to the authenticated user.
6. The backend stores the note in PostgreSQL.
7. The new note appears on the application details page.

### Logging Out

1. The authenticated user selects the Logout button.
2. The frontend sends a `POST /api/auth/logout` request.
3. The backend destroys the user's session.
4. The backend returns a successful response.
5. The user is redirected to the landing page or login page.
6. The user can no longer access protected pages without logging in again.

## 9. Deployment and Virtualization

Vagrant and VMware will be used to create and manage virtual machines for testing The Big J in a multi-server environment.

Vagrant will define and configure the virtual machines using a `Vagrantfile`. VMware will act as the virtualization provider that runs the virtual machines.

### Virtual Machine Structure

The project will use separate virtual machines for the application server and database server.

#### Application Server VM

The application server VM will run:

- React frontend
- Node.js backend
- Express REST API
- Authentication and session management

#### Database Server VM

The database server VM will run:

- PostgreSQL
- The project database
- User account data
- Job application data

### Network Communication

The frontend and backend will communicate through HTTP requests. The backend will communicate with the PostgreSQL database through the virtual network.

    Client Browser
          ↓ HTTP Requests
    Application Server VM
          ↓ Database Requests
    Database Server VM

The database server will not be accessed directly by the client browser. All database requests will pass through the backend server.