# Documentation: Incident Management System

Technical documentation for the project. Start with the requirements and follow the order in the table if this is your first time.

| Document                           | Contents                                                 |
| ---------------------------------- | -------------------------------------------------------- |
| [requirements.md](requirements.md) | Scope, functional requirements, business rules and roles |
| [architecture.md](architecture.md) | Modular monolith, components, monorepo and deployment    |
| [data-model.md](data-model.md)     | Entities, relationships and database constraints         |
| [state-flow.md](state-flow.md)     | Incident lifecycle and allowed transitions               |
| [api.md](api.md)                   | Main endpoints, permissions and error format             |
| [security.md](security.md)         | Authentication, authorization, attachments and auditing  |
| [roadmap.md](roadmap.md)           | Development phases and acceptance criteria               |
| [adr/](adr/)                       | Architecture decision records                            |

## Conventions

- Diagrams use Mermaid and render directly on GitHub.
- Important decisions are recorded as ADRs in `adr/`. An ADR is never deleted: if a decision changes, a new one is created that supersedes the previous one.
- Example values (SLA deadlines, file limits) are configurable and do not represent real policies.
