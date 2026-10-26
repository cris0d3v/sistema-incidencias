# 05. API (draft)

Base: `/api/v1`. Format: JSON. Authentication: `Authorization: Bearer <token>`.
Interactive documentation is published at `/api/docs` (Swagger).

## MVP Endpoints

### Authentication

| Method | Route            | Description             | Access        |
| ------ | ---------------- | ----------------------- | ------------- |
| POST   | `/auth/register` | Create user account     | Public        |
| POST   | `/auth/login`    | Log in, returns JWT     | Public        |
| GET    | `/auth/me`       | Authenticated user data | Authenticated |

### Incidents

| Method | Route                        | Description                                                     | Access                                                   |
| ------ | ---------------------------- | --------------------------------------------------------------- | -------------------------------------------------------- |
| GET    | `/incidents`                 | Paginated list with filters                                     | User: only their own. Agent and administrator: all.      |
| POST   | `/incidents`                 | Create incident                                                 | Authenticated                                            |
| GET    | `/incidents/:id`             | Detail with timeline                                            | Reporter, assigned agent, administrator. Agents see all. |
| PATCH  | `/incidents/:id/assignment`  | Assign or reassign agent                                        | Agent (take own case), administrator                     |
| POST   | `/incidents/:id/transitions` | Change status (body: `{ "to": "InProgress", "reason": "..." }`) | According to [transition table](state-flow.md)           |
| POST   | `/incidents/:id/comments`    | Add comment                                                     | Reporter, assigned agent, administrator                  |

A transitions endpoint is used instead of `PATCH /incidents/:id` with a free `status` field. This way validation cannot be bypassed by accident.

### Catalogs

| Method | Route             | Description                        | Access        |
| ------ | ----------------- | ---------------------------------- | ------------- |
| GET    | `/categories`     | Active categories                  | Authenticated |
| POST   | `/categories`     | Create category                    | Administrator |
| PATCH  | `/categories/:id` | Edit or deactivate                 | Administrator |
| GET    | `/users`          | User list                          | Administrator |
| PATCH  | `/users/:id`      | Change role or activate/deactivate | Administrator |

### Filters for `GET /incidents`

Query parameters: `status`, `priority`, `category_id`, `assignee_id`, `q` (search in title and description), `page`, `per_page` (maximum 100).

## Error format

All errors follow the same format:

```json
{
  "code": "TRANSITION_NOT_ALLOWED",
  "message": "Cannot move from Closed to InProgress.",
  "details": []
}
```

| HTTP Code | Usage                                                            |
| --------- | ---------------------------------------------------------------- |
| 400       | Malformed request                                                |
| 401       | Missing or invalid token                                         |
| 403       | Authenticated, no permission for this action                     |
| 404       | Resource does not exist or is not visible to the user            |
| 409       | Status transition not allowed                                    |
| 422       | Data validation failed (for example, missing resolution comment) |

A 404 is also returned when the user cannot see the resource, to avoid revealing that it exists.

## Conventions

- Dates in ISO 8601 with time zone (UTC in the API).
- Pagination with `page` and `per_page`, and response with `total`.
- Internal numeric IDs. If you want to hide them later, migrate to UUID.
