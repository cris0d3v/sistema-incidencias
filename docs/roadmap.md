# 07. Roadmap

Estimate for one person, at 10 to 15 hours per week. These are planning ranges.

## Phases

| Phase           | Content                                               | Weeks    | Acceptance criteria                                     |
| --------------- | ----------------------------------------------------- | -------- | ------------------------------------------------------- |
| 1. Foundation   | Repo, database, migrations, authentication, and roles | 1 to 1.5 | Each role logs in and sees their screen                 |
| 2. Core         | Create, list, view, and filter incidents              | 1 to 1.5 | A user reports and an agent sees the queue              |
| 3. Flow         | State machine, assignment, comments, and history      | 1.5 to 2 | An incident goes through the full cycle and is recorded |
| 4. Testing      | Transition and permission tests, CI on GitHub Actions | 1        | Green suite on every push                               |
| 5. Enhancements | Attachments, internal notes, emails, metrics          | 2 to 3   | Dashboard with sample data                              |
| 6. Delivery     | Deployment, demo data, README, and screenshots        | 1        | Public link anyone can open                             |

## Version milestones

| Version | Content                          |
| ------- | -------------------------------- |
| v0.1    | Phases 1 to 3: functional MVP    |
| v0.2    | Phase 4: testing and CI          |
| v0.3    | Phase 5: enhancements            |
| v1.0    | Phase 6: deployed and documented |

## Definition of done

A phase is done when:

- Its requirements from the [requirements document](requirements.md) meet the acceptance criteria.
- It has tests for the new logic.
- It is documented in this folder if any contract changed (API, model, states).
- The change is on `main` with green CI.

## Risks

| Risk                                                 | Mitigation                                               |
| ---------------------------------------------------- | -------------------------------------------------------- |
| Learning React takes longer than expected            | Start with the API using Swagger to test it without a UI |
| The state machine grows and becomes hard to maintain | Single transition table and tests from phase 3           |
| Starting on extras before having the core flow       | Extras only come in after v0.1                           |
| The project ends up undeployed                       | Phase 6 is planned from the start, not at the end        |
