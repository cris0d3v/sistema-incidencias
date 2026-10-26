# ADR-0003: Shared types and constants in `packages/shared` (draft)

- **Status:** draft
- **Date:** 2026-10-26

## Context

The API and the web interface need the same statuses, priorities, and response shapes. If they are duplicated, they can drift out of sync without anyone noticing.

## Decision

A `packages/shared` folder with statuses, priorities, roles, and API response types. The API and the web app import it as a workspace dependency.

## Alternatives considered

- **Duplicating the types on each side:** simple at first, but error-prone.
- **Generating types from OpenAPI:** useful, but it adds a build step and does not cover the business constants.

## Consequences

- Changing a status forces the compiler to check both the API and the web app.
- `packages/shared` must not depend on NestJS or React. It only contains plain TypeScript.
