# ADR-0002: PostgreSQL as the database (draft)

- **Status:** draft
- **Date:** 2026-10-26

## Context

The system needs referential integrity, transactions to change status and record history in a single step, and filters with text search.

## Decision

PostgreSQL, with versioned migrations.

## Alternatives considered

- **MySQL:** works, but PostgreSQL offers more complete `CHECK` constraints and built-in text search without plugins.
- **SQL Server:** valid, but with fewer free options for deploying the project.
- **MongoDB:** does not fit well with strict relationships and cross-entity transactions.

## Consequences

- Status and priority constraints live in the database, in addition to the application.
- Migrations must be maintained with TypeORM or Prisma from the start.
