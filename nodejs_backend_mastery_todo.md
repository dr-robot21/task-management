# Node.js Backend Mastery --- Project-Based TODO Roadmap

## Project: TaskFlow API

Build a production-style **task and project management REST API** using
**Node.js, Express, and SQLite**.

The backend will let users register and log in, create projects, manage
tasks, upload attachments, and access only the resources they are
allowed to use.

**Scope:** backend only. A separate React application can consume the
API later, but this roadmap does not include React, frontend pages, or
frontend tooling.

------------------------------------------------------------------------

## 0. Understand the project before coding

-   [ ] Read the complete roadmap once.

-   [ ] Understand the difference between Node.js, Express, and SQLite.

-   [ ] Understand that Node.js runs JavaScript outside the browser.

-   [ ] Understand that Express handles HTTP requests and responses.

-   [ ] Understand that SQLite stores application data in a database
    file.

-   [ ] Understand the client-server model.

-   [ ] Understand what an API is.

-   [ ] Understand what REST means.

-   [ ] Understand JSON and HTTP status codes.

-   [ ] Draw a simple architecture diagram:

    `HTTP client → Express routes → controllers → services → repositories → SQLite`

-   [ ] Decide on the first version's features:

    -   [ ] User registration and login.
    -   [ ] User profile.
    -   [ ] Projects CRUD.
    -   [ ] Tasks CRUD.
    -   [ ] Task status and priority.
    -   [ ] Project/task filtering and pagination.
    -   [ ] File attachments on tasks.
    -   [ ] Authorization and ownership.

-   [ ] Write a short README describing the project.

-   [ ] Create a list of API resources: `users`, `projects`, `tasks`,
    and `attachments`.

**Milestone:** You can explain what you are building and how a request
travels through the backend.

------------------------------------------------------------------------

## 1. Prepare the development environment

-   [ ] Install a current Node.js LTS release.
-   [ ] Verify the installation:
    -   [ ] `node --version`
    -   [ ] `npm --version`
-   [ ] Understand the difference between Node.js and npm.
-   [ ] Understand what `package.json` is.
-   [ ] Create the project directory: `taskflow-api`.
-   [ ] Open the directory in your code editor.
-   [ ] Initialize the project with `npm init -y`.
-   [ ] Add a `.gitignore`.
-   [ ] Ignore at least:
    -   [ ] `node_modules/`
    -   [ ] `.env`
    -   [ ] SQLite database files used locally.
    -   [ ] Uploaded user files.
    -   [ ] Logs.
-   [ ] Initialize Git.
-   [ ] Make the first commit.
-   [ ] Learn the difference between dependencies and development
    dependencies.
-   [ ] Learn how `npm install`, `npm uninstall`, and `npm run` work.
-   [ ] Create useful npm scripts such as `start`, `dev`, and `test`.

**Milestone:** The project is initialized, version-controlled, and runs
a basic Node.js file.

------------------------------------------------------------------------

## 2. Learn the Node.js fundamentals through small exercises

Do these exercises inside a temporary `practice/` directory before
building the real application.

### JavaScript in Node.js

-   [ ] Run a JavaScript file with `node filename.js`.
-   [ ] Use `console.log()` and `console.error()`.
-   [ ] Read command-line arguments with `process.argv`.
-   [ ] Read environment variables with `process.env`.
-   [ ] Understand the global `process` object.
-   [ ] Understand the difference between browser JavaScript and
    Node.js.
-   [ ] Learn how Node.js handles asynchronous work.
-   [ ] Understand the event loop at a high level.

### Modules

-   [ ] Understand why code is split into modules.
-   [ ] Learn ES modules: `import` and `export`.
-   [ ] Configure the project to use ES modules with `"type": "module"`.
-   [ ] Export a function from one file and import it in another.
-   [ ] Understand named exports and default exports.
-   [ ] Understand the difference between ES modules and CommonJS
    (`require`).
-   [ ] Keep the project consistent: use ES modules throughout.

### Asynchronous JavaScript

-   [ ] Practice callbacks.
-   [ ] Understand Promises.
-   [ ] Practice `.then()` and `.catch()`.
-   [ ] Rewrite the same example using `async` and `await`.
-   [ ] Handle errors with `try` / `catch`.
-   [ ] Understand why asynchronous code matters for file and database
    operations.
-   [ ] Learn when to use `Promise.all()`.

### Built-in Node.js modules

-   [ ] Use `node:fs` to read a text file.
-   [ ] Use `node:fs/promises` to read and write files asynchronously.
-   [ ] Create a directory.
-   [ ] Check whether a file exists.
-   [ ] Rename and delete a file.
-   [ ] Use `node:path` to join paths safely.
-   [ ] Understand `path.resolve()` and `path.basename()`.
-   [ ] Use `node:http` to create a tiny HTTP server without Express.
-   [ ] Inspect request method, URL, headers, and body.
-   [ ] Send a response with a status code and JSON.
-   [ ] Understand what Express will simplify for you.

**Milestone:** You can write small Node.js programs, split them into
modules, use async/await, and work with files.

------------------------------------------------------------------------

## 3. Design the backend architecture and folder structure

Do not put the entire application in `server.js`. Start with a clear
structure and add folders only when you need them.

Suggested structure:

``` text
taskflow-api/
├── src/
│   ├── app.js
│   ├── server.js
│   ├── config/
│   │   ├── env.js
│   │   └── database.js
│   ├── routes/
│   │   ├── index.routes.js
│   │   ├── auth.routes.js
│   │   ├── users.routes.js
│   │   ├── projects.routes.js
│   │   ├── tasks.routes.js
│   │   └── attachments.routes.js
│   ├── controllers/
│   ├── services/
│   ├── repositories/
│   ├── middleware/
│   ├── validators/
│   ├── db/
│   │   ├── migrations/
│   │   └── seeds/
│   ├── utils/
│   └── constants/
├── storage/
│   └── uploads/
├── tests/
│   ├── integration/
│   └── unit/
├── docs/
├── scripts/
├── .env.example
├── .gitignore
├── package.json
└── README.md
```

-   [ ] Understand the purpose of each folder.
-   [ ] Create `src/app.js` to configure Express.
-   [ ] Create `src/server.js` to start listening on a port.
-   [ ] Keep application setup separate from server startup.
-   [ ] Create a basic health route.
-   [ ] Create a route aggregator in `routes/index.routes.js`.
-   [ ] Decide on naming conventions for files and functions.
-   [ ] Understand the request lifecycle through the folders.
-   [ ] Keep controllers focused on HTTP input/output.
-   [ ] Keep business rules in services.
-   [ ] Keep database queries in repositories.
-   [ ] Keep reusable request checks in middleware and validators.
-   [ ] Avoid creating empty folders or unnecessary abstractions before
    they are needed.

**Milestone:** You understand where each responsibility belongs and can
trace a request through the application.

------------------------------------------------------------------------

## 4. Build your first Express server

-   [ ] Install Express.
-   [ ] Create the Express application in `app.js`.
-   [ ] Start the server from `server.js`.
-   [ ] Read the port from an environment variable.
-   [ ] Add `GET /api/health`.
-   [ ] Return JSON from the health route.
-   [ ] Understand `req` and `res`.
-   [ ] Understand `req.params`, `req.query`, and `req.body`.
-   [ ] Understand `res.status()`, `res.json()`, and `res.send()`.
-   [ ] Add `express.json()` middleware.
-   [ ] Test a route using curl, Postman, or Insomnia.
-   [ ] Create routes in a separate router file with `express.Router()`.
-   [ ] Mount the router under `/api`.
-   [ ] Add a route that returns a 404 for unknown endpoints.
-   [ ] Understand middleware execution order.
-   [ ] Write a small custom middleware that logs the HTTP method and
    URL.
-   [ ] Understand the difference between application-level and
    router-level middleware.

**Milestone:** You have a running Express API with organized routes and
JSON responses.

------------------------------------------------------------------------

## 5. Understand HTTP and REST API design

Before adding database operations, design the API.

-   [ ] Understand HTTP methods: GET, POST, PUT, PATCH, DELETE.
-   [ ] Understand safe and idempotent methods.
-   [ ] Understand request headers and response headers.
-   [ ] Understand path parameters versus query parameters.
-   [ ] Understand JSON request and response bodies.
-   [ ] Learn common status codes:
    -   [ ] `200` --- successful request.
    -   [ ] `201` --- resource created.
    -   [ ] `204` --- successful request with no response body.
    -   [ ] `400` --- invalid request.
    -   [ ] `401` --- authentication required or invalid.
    -   [ ] `403` --- authenticated but not allowed.
    -   [ ] `404` --- resource not found.
    -   [ ] `409` --- conflict, such as a duplicate email.
    -   [ ] `422` --- request content failed validation (if you choose
        this convention).
    -   [ ] `429` --- too many requests.
    -   [ ] `500` --- unexpected server error.
-   [ ] Design consistent JSON response shapes.
-   [ ] Decide how errors will be represented.
-   [ ] Use nouns for resource paths.
-   [ ] Avoid putting action names in paths when an HTTP method
    expresses the action.
-   [ ] Design these endpoints before implementing them:

### Initial endpoint plan

  Method   Endpoint                           Purpose
  -------- ---------------------------------- ------------------------------
  GET      `/api/health`                      Health check
  POST     `/api/auth/register`               Register
  POST     `/api/auth/login`                  Log in
  GET      `/api/users/me`                    Current user's profile
  PATCH    `/api/users/me`                    Update profile
  GET      `/api/projects`                    List current user's projects
  POST     `/api/projects`                    Create a project
  GET      `/api/projects/:projectId`         Get one project
  PATCH    `/api/projects/:projectId`         Update a project
  DELETE   `/api/projects/:projectId`         Delete a project
  GET      `/api/projects/:projectId/tasks`   List project tasks
  POST     `/api/projects/:projectId/tasks`   Create a task
  GET      `/api/tasks/:taskId`               Get one task
  PATCH    `/api/tasks/:taskId`               Update a task
  DELETE   `/api/tasks/:taskId`               Delete a task
  POST     `/api/tasks/:taskId/attachments`   Upload an attachment
  GET      `/api/attachments/:attachmentId`   Download an attachment
  DELETE   `/api/attachments/:attachmentId`   Delete an attachment

-   [ ] Decide whether delete operations are permanent or soft deletes.
-   [ ] Decide whether a task must belong to a project.
-   [ ] Decide whether a user can access only their own projects.
-   [ ] Write example requests and responses for the main endpoints.

**Milestone:** You have a documented API contract before implementing
the business logic.

------------------------------------------------------------------------

## 6. Configure environment variables and application configuration

-   [ ] Install and configure `dotenv` for local development.
-   [ ] Create `.env`.
-   [ ] Add `.env` to `.gitignore`.
-   [ ] Create `.env.example` containing placeholder values only.
-   [ ] Configure `PORT`.
-   [ ] Configure `NODE_ENV`.
-   [ ] Configure the SQLite database path.
-   [ ] Configure the upload directory.
-   [ ] Configure the authentication secret.
-   [ ] Validate required environment variables at startup.
-   [ ] Fail with a clear message if a required variable is missing.
-   [ ] Do not commit secrets or real credentials.
-   [ ] Understand the difference between development and production
    configuration.

**Milestone:** Configuration is centralized, validated, and not
hard-coded throughout the app.

------------------------------------------------------------------------

## 7. Learn SQLite and SQL before connecting everything to Express

Use a SQLite command-line tool or a database viewer to practice SQL
independently.

### SQL fundamentals

-   [ ] Understand what a relational database is.
-   [ ] Understand tables, rows, columns, and data types.
-   [ ] Create a SQLite database.
-   [ ] Create a table.
-   [ ] Insert records.
-   [ ] Select all records.
-   [ ] Select records with `WHERE`.
-   [ ] Update a record.
-   [ ] Delete a record.
-   [ ] Use `ORDER BY`.
-   [ ] Use `LIMIT` and `OFFSET`.
-   [ ] Use `LIKE`.
-   [ ] Use aggregate functions such as `COUNT`.
-   [ ] Understand primary keys.
-   [ ] Understand foreign keys.
-   [ ] Understand `NOT NULL`, `UNIQUE`, and `DEFAULT`.
-   [ ] Understand one-to-many relationships.
-   [ ] Understand joins.
-   [ ] Practice `INNER JOIN` and `LEFT JOIN`.
-   [ ] Understand indexes and why they can improve lookup performance.
-   [ ] Understand transactions and why multiple related changes may
    need to succeed or fail together.

### Design the database

Create these tables:

**users** - \[ \] `id` - \[ \] `name` - \[ \] `email` (unique) - \[ \]
`password_hash` - \[ \] `created_at` - \[ \] `updated_at`

**projects** - \[ \] `id` - \[ \] `user_id` (foreign key to users) - \[
\] `name` - \[ \] `description` - \[ \] `created_at` - \[ \]
`updated_at`

**tasks** - \[ \] `id` - \[ \] `project_id` (foreign key to projects) -
\[ \] `title` - \[ \] `description` - \[ \] `status` (for example: todo,
in_progress, done) - \[ \] `priority` (for example: low, medium, high) -
\[ \] `due_date` (nullable) - \[ \] `created_at` - \[ \] `updated_at`

**attachments** - \[ \] `id` - \[ \] `task_id` (foreign key to tasks) -
\[ \] `original_name` - \[ \] `stored_name` - \[ \] `mime_type` - \[ \]
`size` - \[ \] `created_at`

-   [ ] Draw an ER diagram.
-   [ ] Identify each primary key and foreign key.
-   [ ] Decide what should happen to a project's tasks when the project
    is deleted.
-   [ ] Decide what should happen to attachment records when a task is
    deleted.
-   [ ] Enable SQLite foreign-key enforcement on each database
    connection.
-   [ ] Add appropriate indexes after identifying common lookup
    patterns.

**Milestone:** You can create the database schema and explain the
relationships.

------------------------------------------------------------------------

## 8. Connect Node.js to SQLite

For this project, use **`better-sqlite3`** as a straightforward SQLite
library. It is synchronous, which makes it approachable for a small
learning project. Learn its trade-offs and avoid long-running or
expensive work inside database calls.

-   [ ] Install `better-sqlite3`.
-   [ ] Create a single database connection module.
-   [ ] Read the database path from configuration.
-   [ ] Create the database directory if it does not exist.
-   [ ] Enable foreign keys.
-   [ ] Set a sensible busy timeout.
-   [ ] Create a small test query.
-   [ ] Run a parameterized SELECT query.
-   [ ] Insert a row using placeholders.
-   [ ] Read the inserted row.
-   [ ] Update a row.
-   [ ] Delete a row.
-   [ ] Never concatenate user input into SQL strings.
-   [ ] Understand prepared statements.
-   [ ] Understand how to retrieve inserted IDs and affected row counts.
-   [ ] Create a transaction for an operation involving multiple
    database changes.
-   [ ] Handle database errors without exposing internal details to API
    clients.
-   [ ] Keep the database connection in one shared module rather than
    opening a new connection for every request.

**Milestone:** The Express application can safely read and write SQLite
data.

------------------------------------------------------------------------

## 9. Add database migrations and seed data

Avoid relying on manually recreating the database every time you change
the schema.

-   [ ] Understand what a database migration is.
-   [ ] Create a migrations directory.
-   [ ] Create an initial migration for all tables.
-   [ ] Create a migration-tracking table.
-   [ ] Write a script that applies migrations in order.
-   [ ] Ensure an already-applied migration is not applied twice.
-   [ ] Create a second migration that adds a field or index.
-   [ ] Learn how to handle migration failures.
-   [ ] Decide how schema changes are handled in development and
    production.
-   [ ] Create a seed script with development-only sample users,
    projects, and tasks.
-   [ ] Ensure seed data is not accidentally inserted in production.
-   [ ] Document how to initialize a fresh database.

**Milestone:** A new developer can create the database from migrations
and load safe sample data.

------------------------------------------------------------------------

## 10. Implement the repository and service layers

Start with one resource and follow the same pattern for the others.

-   [ ] Create a `users.repository.js`.
-   [ ] Put SQL queries for users in the repository.
-   [ ] Create a `users.service.js`.
-   [ ] Put business rules in the service.
-   [ ] Create a `users.controller.js`.
-   [ ] Read request data and send HTTP responses in the controller.
-   [ ] Create `users.routes.js`.
-   [ ] Connect the route to its controller.
-   [ ] Repeat the pattern for projects.
-   [ ] Repeat the pattern for tasks.
-   [ ] Keep SQL out of controllers.
-   [ ] Keep HTTP response handling out of repositories.
-   [ ] Avoid duplicating business rules across controllers.
-   [ ] Do not add a layer just for the sake of having more folders.

**Milestone:** You can explain the responsibilities of routes,
controllers, services, and repositories.

------------------------------------------------------------------------

## 11. Build CRUD for projects

### Create

-   [ ] Implement `POST /api/projects`.
-   [ ] Require a project name.
-   [ ] Allow an optional description.
-   [ ] Save the project in SQLite.
-   [ ] Associate it with the authenticated user later; initially, use a
    development-only test user if authentication is not ready.
-   [ ] Return `201 Created` and the created project.

### Read

-   [ ] Implement `GET /api/projects`.
-   [ ] Return only the current user's projects once authentication is
    implemented.
-   [ ] Implement `GET /api/projects/:projectId`.
-   [ ] Return `404` when the project does not exist or is not
    accessible.
-   [ ] Decide whether task counts should be included.

### Update

-   [ ] Implement `PATCH /api/projects/:projectId`.
-   [ ] Allow updating the name and description.
-   [ ] Reject empty or invalid names.
-   [ ] Update `updated_at`.
-   [ ] Return the updated project.

### Delete

-   [ ] Implement `DELETE /api/projects/:projectId`.
-   [ ] Decide whether to cascade-delete tasks.
-   [ ] Return a consistent response.
-   [ ] Verify that another user's project cannot be deleted.

### Test

-   [ ] Create a project.
-   [ ] Read all projects.
-   [ ] Read one project.
-   [ ] Update a project.
-   [ ] Delete a project.
-   [ ] Test an invalid ID.
-   [ ] Test a project that does not exist.
-   [ ] Test missing required fields.

**Milestone:** Project CRUD works through HTTP and persists in SQLite.

------------------------------------------------------------------------

## 12. Build CRUD for tasks

-   [ ] Implement task creation inside a project.
-   [ ] Verify that the parent project exists.
-   [ ] Verify that the user can access the parent project.
-   [ ] Validate title and description.
-   [ ] Validate status against allowed values.
-   [ ] Validate priority against allowed values.
-   [ ] Allow an optional due date.
-   [ ] Implement task listing for a project.
-   [ ] Implement retrieving one task.
-   [ ] Implement task updates.
-   [ ] Implement task deletion.
-   [ ] Update `updated_at` when a task changes.
-   [ ] Prevent moving a task to a project the user cannot access.
-   [ ] Decide whether a task can be moved between projects.
-   [ ] Test all CRUD operations.
-   [ ] Test invalid status and priority values.
-   [ ] Test missing and inaccessible projects.

**Milestone:** Users can manage tasks inside their own projects.

------------------------------------------------------------------------

## 13. Add request validation

Never assume that a request body is valid just because it is JSON.

-   [ ] Understand the difference between validation and sanitization.
-   [ ] Choose a validation library such as Zod or Joi.
-   [ ] Create schemas for registration, login, projects, tasks, and
    profile updates.
-   [ ] Validate route parameters where appropriate.
-   [ ] Validate query parameters.
-   [ ] Validate request bodies.
-   [ ] Reject unknown or unexpected fields where appropriate.
-   [ ] Trim strings.
-   [ ] Set maximum lengths.
-   [ ] Validate email format.
-   [ ] Validate numeric values and IDs.
-   [ ] Validate date formats.
-   [ ] Return a consistent `400` or `422` response for invalid input.
-   [ ] Do not trust client-provided user IDs for ownership.
-   [ ] Add tests for missing, malformed, and oversized values.

**Milestone:** Invalid input is rejected before it reaches business
logic or SQL.

------------------------------------------------------------------------

## 14. Implement authentication

Authentication answers: **Who is making this request?**

-   [ ] Understand authentication versus authorization.
-   [ ] Understand password hashing and why passwords must not be stored
    as plain text.
-   [ ] Install a password-hashing library such as `bcrypt`.
-   [ ] Implement user registration.
-   [ ] Hash passwords before saving them.
-   [ ] Never return password hashes in API responses.
-   [ ] Enforce unique email addresses.
-   [ ] Handle duplicate email errors cleanly.
-   [ ] Implement login.
-   [ ] Compare the submitted password with the stored hash.
-   [ ] Return a clear generic error for invalid credentials.
-   [ ] Choose an authentication strategy.
-   [ ] For this learning API, implement JWT access tokens.
-   [ ] Store the JWT secret in environment configuration.
-   [ ] Set a reasonable token expiration.
-   [ ] Add authentication middleware.
-   [ ] Read the token from the `Authorization: Bearer <token>` header.
-   [ ] Verify the token.
-   [ ] Attach the authenticated user's identity to the request.
-   [ ] Protect `/api/users/me`.
-   [ ] Implement the current user's profile endpoint.
-   [ ] Test missing, malformed, expired, and invalid tokens.
-   [ ] Understand the limitations of a simple access-token-only setup.
-   [ ] Learn refresh-token rotation and revocation as an advanced
    follow-up, rather than adding it before the basic flow works.

**Security note:** JWTs are signed, not encrypted. Do not put passwords
or sensitive personal information in their payload. For browser-based
production applications, carefully assess cookie-based sessions, secure
cookie settings, CSRF protections, and token-storage risks before
choosing how credentials are stored.

**Milestone:** Users can register, log in, and access protected
endpoints.

------------------------------------------------------------------------

## 15. Implement authorization and resource ownership

Authorization answers: **What is this user allowed to do?**

-   [ ] Ensure every project belongs to a user.
-   [ ] Filter project queries by the authenticated user's ID.
-   [ ] Ensure a user cannot read another user's project by guessing its
    ID.
-   [ ] Ensure a user cannot update another user's project.
-   [ ] Ensure a user cannot delete another user's project.
-   [ ] Ensure tasks are accessible only through projects the user owns.
-   [ ] Ensure attachment access follows the same ownership rules.
-   [ ] Decide whether inaccessible resources return `403` or `404`.
-   [ ] Add tests using two different users.
-   [ ] Attempt cross-user access for every protected resource.
-   [ ] Verify that IDs supplied in the body cannot override the
    authenticated user identity.

**Milestone:** A user cannot access or modify another user's data.

------------------------------------------------------------------------

## 16. Add filtering, sorting, and pagination

-   [ ] Understand why returning every database row is not scalable.
-   [ ] Add `page` and `limit` query parameters.
-   [ ] Set a maximum allowed page size.
-   [ ] Calculate the SQL `LIMIT` and `OFFSET` safely.
-   [ ] Return pagination metadata.
-   [ ] Add task filtering by status.
-   [ ] Add task filtering by priority.
-   [ ] Add task filtering by due date.
-   [ ] Add text search for task titles.
-   [ ] Add sorting by creation date or due date.
-   [ ] Whitelist allowed sort columns.
-   [ ] Never insert an arbitrary client-provided sort expression into
    SQL.
-   [ ] Combine filters with pagination.
-   [ ] Test empty results and invalid query parameters.

**Milestone:** List endpoints support safe, predictable filtering and
pagination.

------------------------------------------------------------------------

## 17. Learn file handling and implement uploads

This project will allow users to attach files to tasks. Learn the file
lifecycle, not just how to receive a file.

### Understand file handling

-   [ ] Understand the difference between text/JSON requests and
    `multipart/form-data`.
-   [ ] Understand what a file buffer is.
-   [ ] Understand file metadata: original name, MIME type, and size.
-   [ ] Understand the difference between an original filename and a
    stored filename.
-   [ ] Understand local filesystem storage versus object storage.
-   [ ] Understand why uploaded files should not automatically be
    trusted.
-   [ ] Decide which file types the application accepts.
-   [ ] Decide the maximum file size.
-   [ ] Decide whether multiple files can be attached to one task.

### Implement upload

-   [ ] Install Multer.
-   [ ] Create upload middleware.
-   [ ] Configure a dedicated upload directory outside public source
    files.
-   [ ] Generate a random stored filename.
-   [ ] Preserve the original filename only as metadata.
-   [ ] Set a file-size limit.
-   [ ] Set a maximum file count.
-   [ ] Allowlist permitted file types.
-   [ ] Do not trust the client-provided MIME type alone.
-   [ ] Where practical, inspect file signatures (magic bytes) for
    supported formats.
-   [ ] Reject unexpected file types.
-   [ ] Handle missing files.
-   [ ] Handle files that exceed the size limit.
-   [ ] Store file metadata in the `attachments` table.
-   [ ] Associate each attachment with a task.
-   [ ] Check that the authenticated user owns the task's project before
    accepting the upload.
-   [ ] Clean up the physical file if the database insert fails.
-   [ ] Avoid using the original filename as a filesystem path.

### Download and delete

-   [ ] Implement an authenticated download endpoint.
-   [ ] Check resource ownership before sending a file.
-   [ ] Use a safe stored path derived from a generated identifier.
-   [ ] Set appropriate content headers.
-   [ ] Implement attachment deletion.
-   [ ] Delete the database record and physical file safely.
-   [ ] Handle missing files and missing records.
-   [ ] Decide how to clean up orphaned files.
-   [ ] Test uploading, downloading, and deleting.
-   [ ] Test a user attempting to download another user's attachment.

### File security

-   [ ] Keep uploads outside the public web root unless public access is
    an intentional requirement.
-   [ ] Never execute uploaded files.
-   [ ] Do not trust file extensions or MIME headers by themselves.
-   [ ] Consider malware scanning for a real production service.
-   [ ] Consider storage quotas and rate limits.
-   [ ] Avoid exposing internal filesystem paths in API responses or
    errors.
-   [ ] Understand that local disk storage may not be durable across
    some deployment platforms.

**Milestone:** Authenticated users can upload, list, download, and
delete permitted task attachments securely.

------------------------------------------------------------------------

## 18. Add centralized error handling

-   [ ] Understand synchronous and asynchronous errors in Express.
-   [ ] Create a custom application error class.
-   [ ] Create a not-found handler.
-   [ ] Create a centralized error-handling middleware.
-   [ ] Place error middleware after routes.
-   [ ] Return consistent JSON error responses.
-   [ ] Handle validation errors.
-   [ ] Handle authentication errors.
-   [ ] Handle authorization errors.
-   [ ] Handle SQLite constraint errors.
-   [ ] Handle file-upload errors.
-   [ ] Avoid returning stack traces in production.
-   [ ] Log detailed errors on the server.
-   [ ] Never expose passwords, tokens, secrets, or private file paths
    in logs.
-   [ ] Test expected errors and unexpected errors.

**Milestone:** Errors are predictable for API clients and useful for
developers without leaking sensitive details.

------------------------------------------------------------------------

## 19. Add security middleware and harden the API

-   [ ] Install and configure `helmet`.
-   [ ] Configure CORS for the expected client origin(s).
-   [ ] Do not use unrestricted CORS in production without a reason.
-   [ ] Add rate limiting to login and registration endpoints.
-   [ ] Consider rate limiting other expensive endpoints.
-   [ ] Set request body size limits.
-   [ ] Validate and normalize user input.
-   [ ] Use parameterized SQL for every user-controlled value.
-   [ ] Keep secrets in environment variables.
-   [ ] Use HTTPS in production.
-   [ ] Set secure cookie options if cookies are used.
-   [ ] Review password policy and account-enumeration risks.
-   [ ] Review file upload limits and file-type checks.
-   [ ] Check authorization on every resource operation.
-   [ ] Keep dependencies updated.
-   [ ] Run `npm audit` and understand its findings before applying
    fixes.
-   [ ] Add a security checklist to the README.

**Milestone:** The API has baseline protections against common mistakes
and abuse.

------------------------------------------------------------------------

## 20. Add logging and operational visibility

-   [ ] Understand the difference between application logs and HTTP
    access logs.
-   [ ] Add structured logging with a library such as Pino.
-   [ ] Log server startup and shutdown.
-   [ ] Log request method, path, status code, and duration.
-   [ ] Assign a request ID to each request.
-   [ ] Log unexpected errors with enough context to debug them.
-   [ ] Avoid logging passwords, authorization headers, tokens, or
    uploaded file contents.
-   [ ] Decide how logs are handled in development and production.
-   [ ] Add a health endpoint.
-   [ ] Add a readiness check that verifies the database can be queried.
-   [ ] Understand why health endpoints should not expose secrets or
    internal configuration.

**Milestone:** You can diagnose common failures without exposing
sensitive information.

------------------------------------------------------------------------

## 21. Test the backend

### Manual API testing

-   [ ] Create a Postman or Insomnia collection.
-   [ ] Add a health check request.
-   [ ] Add registration and login requests.
-   [ ] Save a token in your testing environment.
-   [ ] Add project CRUD requests.
-   [ ] Add task CRUD requests.
-   [ ] Add upload and download requests.
-   [ ] Test successful responses.
-   [ ] Test invalid input.
-   [ ] Test missing authentication.
-   [ ] Test forbidden access.
-   [ ] Test resources that do not exist.

### Automated tests

-   [ ] Learn the built-in `node:test` test runner.
-   [ ] Learn assertions with `node:assert`.
-   [ ] Install Supertest for HTTP integration tests.
-   [ ] Separate test configuration from development configuration.
-   [ ] Use a temporary test database.
-   [ ] Ensure tests do not modify your development database.
-   [ ] Create tests for health and 404 routes.
-   [ ] Test registration and login.
-   [ ] Test protected endpoints.
-   [ ] Test project CRUD.
-   [ ] Test task CRUD.
-   [ ] Test validation failures.
-   [ ] Test cross-user access restrictions.
-   [ ] Test file upload size and type restrictions.
-   [ ] Test missing files and unauthorized downloads.
-   [ ] Test database constraints.
-   [ ] Test error response shapes.
-   [ ] Make tests repeatable and independent.
-   [ ] Add an npm script for the test suite.

**Milestone:** You can run automated tests and trust that core behavior
remains correct after changes.

------------------------------------------------------------------------

## 22. Document the API

-   [ ] Write a useful project README.
-   [ ] Document prerequisites and installation.
-   [ ] Document environment variables.
-   [ ] Document database initialization and migrations.
-   [ ] Document how to run the server.
-   [ ] Document how to run tests.
-   [ ] Document the folder structure.
-   [ ] Document authentication requirements.
-   [ ] Document every endpoint.
-   [ ] Include request body examples.
-   [ ] Include success response examples.
-   [ ] Include error response examples.
-   [ ] Explain pagination and filtering.
-   [ ] Explain upload constraints.
-   [ ] Add an OpenAPI specification.
-   [ ] Learn the purpose of Swagger UI or another OpenAPI viewer.
-   [ ] Verify that the documentation matches actual API behavior.

**Milestone:** Another developer can install, run, test, and use the API
without asking you to explain every endpoint.

------------------------------------------------------------------------

## 23. Improve the database and application design

Do this after the core API works.

-   [ ] Review SQL queries for duplicated logic.
-   [ ] Add indexes for frequently used filters and joins.
-   [ ] Use transactions for multi-step operations.
-   [ ] Review foreign-key behavior.
-   [ ] Review cascade-delete behavior carefully.
-   [ ] Add a database backup procedure.
-   [ ] Learn how to restore from a backup.
-   [ ] Understand SQLite's single-writer behavior and when it is
    appropriate.
-   [ ] Understand SQLite WAL mode and its trade-offs.
-   [ ] Avoid placing a SQLite database on an unsuitable network
    filesystem.
-   [ ] Measure before optimizing.
-   [ ] Check for N+1 query patterns.
-   [ ] Review memory use when handling large files.
-   [ ] Use streaming for file downloads rather than loading large files
    entirely into memory.
-   [ ] Consider a service-level transaction for operations that update
    multiple related records.
-   [ ] Keep migrations under version control.

**Milestone:** You understand the operational limits of SQLite and can
maintain the database safely.

------------------------------------------------------------------------

## 24. Production readiness and deployment preparation

The exact deployment steps depend on the hosting provider. Prepare the
application so it can run outside your development machine.

-   [ ] Set `NODE_ENV=production`.
-   [ ] Configure production environment variables securely.
-   [ ] Ensure the server listens on the host-provided port.
-   [ ] Ensure the database path is persistent.
-   [ ] Ensure the upload directory is persistent.
-   [ ] Confirm the hosting platform supports persistent local storage
    before relying on SQLite and local uploads.
-   [ ] Create a production database initialization procedure.
-   [ ] Run migrations as a controlled deployment step.
-   [ ] Create a backup and restore plan.
-   [ ] Configure HTTPS at the hosting layer or reverse proxy.
-   [ ] Configure CORS for the deployed client origin.
-   [ ] Disable verbose error responses.
-   [ ] Configure process supervision or the platform's restart
    mechanism.
-   [ ] Add health checks.
-   [ ] Test a clean deployment from the README.
-   [ ] Verify uploads survive a restart and redeployment if the
    platform claims persistent storage.
-   [ ] Verify database backups can actually be restored.
-   [ ] Never commit `.env`, database files containing real user data,
    or uploaded user files.

**Important SQLite deployment note:** SQLite is an excellent choice for
learning and for many small, single-instance applications. It is not a
drop-in fit for every multi-instance or network-filesystem deployment.
If the backend later needs multiple application instances writing
concurrently, reassess the database choice rather than forcing SQLite
into an unsuitable environment.

**Milestone:** You have a repeatable deployment process and understand
what must persist between restarts.

------------------------------------------------------------------------

## 25. Optional advanced Node.js topics

Complete these after the main API is stable.

-   [ ] Learn Node.js streams.
-   [ ] Stream a large file from disk to an HTTP response.
-   [ ] Understand backpressure.
-   [ ] Learn the EventEmitter pattern.
-   [ ] Understand buffers and binary data.
-   [ ] Learn worker threads and when CPU-heavy work needs them.
-   [ ] Understand child processes.
-   [ ] Learn graceful shutdown on `SIGINT` and `SIGTERM`.
-   [ ] Handle unhandled promise rejections and uncaught exceptions
    appropriately.
-   [ ] Learn caching concepts.
-   [ ] Add an email notification workflow using a development mail
    service (optional).
-   [ ] Add background jobs only if the application has a real need for
    them.
-   [ ] Learn WebSockets only if you later need real-time updates.
-   [ ] Learn Docker packaging after the app works locally.
-   [ ] Learn how reverse proxies work.
-   [ ] Explore an ORM or query builder only after you understand the
    SQL being generated.

**Milestone:** You understand important Node.js capabilities beyond
basic Express CRUD.

------------------------------------------------------------------------

## 26. Final quality checklist

### Functionality

-   [ ] A user can register and log in.
-   [ ] A user can view and update their own profile.
-   [ ] A user can create, read, update, and delete projects.
-   [ ] A user can create, read, update, and delete tasks.
-   [ ] A user can filter, sort, and paginate tasks.
-   [ ] A user can upload, download, and delete task attachments.
-   [ ] A user cannot access another user's resources.

### Code quality

-   [ ] The folder structure has clear responsibilities.
-   [ ] Controllers are not full of SQL queries.
-   [ ] Services contain business rules.
-   [ ] Repositories contain database operations.
-   [ ] Validation is centralized and consistent.
-   [ ] Errors use a consistent response format.
-   [ ] Configuration is not hard-coded.
-   [ ] No secrets are committed.
-   [ ] Code is formatted consistently.
-   [ ] Unused dependencies and files are removed.

### Reliability and security

-   [ ] Automated tests pass.
-   [ ] Foreign keys are enabled.
-   [ ] SQL uses prepared statements.
-   [ ] Passwords are hashed.
-   [ ] Protected routes require authentication.
-   [ ] Ownership checks are present.
-   [ ] Upload limits and allowlists are enforced.
-   [ ] Private files are not publicly exposed.
-   [ ] Logs do not contain secrets.
-   [ ] Database backup and restore have been tested.

### Documentation

-   [ ] README has setup instructions.
-   [ ] `.env.example` is complete and safe.
-   [ ] API endpoints are documented.
-   [ ] OpenAPI documentation is accurate.
-   [ ] Database migrations are documented.
-   [ ] Test commands are documented.

------------------------------------------------------------------------

# Suggested learning order

Do not try to build every feature at once. Complete one milestone, test
it, and commit your work before moving on.

  Stage   Focus                   Result
  ------- ----------------------- ---------------------------
  1       Node.js fundamentals    Small Node programs
  2       Express and HTTP        First working API
  3       REST design             Endpoint contract
  4       SQLite and SQL          Database schema
  5       Architecture and CRUD   Projects and tasks
  6       Validation              Reliable request handling
  7       Authentication          Register and login
  8       Authorization           Private user data
  9       Uploads and files       Task attachments
  10      Errors and security     Hardened API
  11      Tests and docs          Maintainable API
  12      Deployment              Production-ready backend

## Rules for learning effectively

1.  **Type the code yourself.** Do not copy a complete tutorial project
    without understanding it.
2.  **Build one feature at a time.** For each feature, implement the
    route, controller, service, repository, database query, and tests.
3.  **Test every endpoint.** Use curl, Postman, or Insomnia before
    moving on.
4.  **Read the error message.** Try to diagnose the problem before
    looking for a solution.
5.  **Commit after each milestone.** Use meaningful Git commit messages.
6.  **Do not skip SQL.** Learn what your database library is doing.
7.  **Do not skip security.** Ownership checks and upload validation are
    core features, not optional polish.
8.  **Keep a learning journal.** Write down what you learned, what
    broke, and how you fixed it.
9.  **Avoid premature complexity.** Start with a modular monolith; do
    not add microservices, Redis, queues, or an ORM just because they
    are popular.
10. **Use the final checklist as your definition of done.**

## First session --- start here

-   [ ] Install Node.js LTS and verify `node --version` and
    `npm --version`.
-   [ ] Create `taskflow-api`.
-   [ ] Run `npm init -y`.
-   [ ] Configure ES modules.
-   [ ] Create `src/server.js`.
-   [ ] Make the server print `TaskFlow API is running`.
-   [ ] Run it with Node.js.
-   [ ] Initialize Git and make your first commit.

**Your first goal is not to build the whole API. It is to understand
each piece while gradually turning TaskFlow into a working backend.**
