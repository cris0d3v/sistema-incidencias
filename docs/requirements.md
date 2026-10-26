# 01. Requirements

## Vision

A system where users report incidents (technical failures, support requests), agents handle them based on priority, and the administrator configures categories and deadlines. Every change is recorded.

## Scope

**Inside the MVP:**

- Authentication with roles.
- Create, list, filter, and view incidents.
- Assignment and status changes with validated transitions.
- Public comments and immutable history.

**Outside the MVP (later versions):**

- Attachments, internal notes, email notifications, metrics, SLA with alerts, real-time updates.

**Out of project scope:**

- Integration with external systems (ITSM, inbound email, LDAP).
- Billing or asset tracking.

## Roles

| Role          | Description                                                              |
| ------------- | ------------------------------------------------------------------------ |
| User          | Reports incidents and only sees their own.                               |
| Agent         | Handles incidents, assigns them to themselves, and changes their status. |
| Administrator | Manages users, categories, and configuration. Sees all incidents.        |

## Functional requirements

| ID    | Requirement                                                                | Stage |
| ----- | -------------------------------------------------------------------------- | ----- |
| FR-01 | Registration and login with email and password                             | MVP   |
| FR-02 | Create incident with title, description, category, and priority            | MVP   |
| FR-03 | List incidents with filters by status, priority, category, and assignee    | MVP   |
| FR-04 | Text search in title and description                                       | MVP   |
| FR-05 | View details with a timeline of comments and changes                       | MVP   |
| FR-06 | Assign incident to an agent                                                | MVP   |
| FR-07 | Change status according to allowed transitions                             | MVP   |
| FR-08 | Comment on an incident                                                     | MVP   |
| FR-09 | View immutable change history                                              | MVP   |
| FR-10 | Manage users and roles                                                     | MVP   |
| FR-11 | Manage categories                                                          | MVP   |
| FR-12 | Attach files with size and type limits                                     | V2    |
| FR-13 | Internal notes visible only to agents and administrators                   | V2    |
| FR-14 | Email notifications on creation, assignment, and resolution                | V2    |
| FR-15 | Metrics dashboard: open by status, average resolution time, agent workload | V2    |
| FR-16 | SLA deadlines by priority and overdue flag                                 | Extra |

## Business rules

| ID    | Rule                                                                                |
| ----- | ----------------------------------------------------------------------------------- |
| BR-01 | Only the assigned agent or an administrator can move the incident to _In progress_. |
| BR-02 | It cannot be marked _Resolved_ without a resolution comment.                        |
| BR-03 | A _Closed_ incident cannot be edited. If the problem returns, it is reopened.       |
| BR-04 | A user can only confirm closure or reopen their own incidents.                      |
| BR-05 | Internal notes are never returned in responses to the reporter (from V2).           |
| BR-06 | Every status, priority, or assignment change generates a history entry.             |
| BR-07 | Example SLA deadlines: Critical 4 h, High 8 h, Medium 24 h, Low 72 h.               |

## Non-functional requirements

| ID     | Requirement   | Acceptance criteria                                                                             |
| ------ | ------------- | ----------------------------------------------------------------------------------------------- |
| NFR-01 | Security      | Passwords hashed with argon2 or bcrypt. Permissions verified on the backend for every endpoint. |
| NFR-02 | Integrity     | Foreign keys in the database. Status change and history recorded in the same transaction.       |
| NFR-03 | Testing       | Unit tests for the state machine and integration tests for permissions.                         |
| NFR-04 | Usability     | Loading, empty, and error states on every view. Works on mobile and desktop.                    |
| NFR-05 | Performance   | The incident list responds in under 500 ms with 10,000 records, using pagination and indexes.   |
| NFR-06 | Documentation | API documented with OpenAPI (Swagger). README with instructions to run the project.             |
| NFR-07 | Deployment    | The entire system starts with `docker compose up`.                                              |

## Assumptions

- Single tenant: all users belong to one organization.
- Interface language: Spanish.
- Single time zone for displaying dates.
