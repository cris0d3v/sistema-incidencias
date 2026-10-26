# ADR-0001: Modular monolith instead of microservices

- **Status:** draft but acepted
- **Date:** 2026-10-26

## Context

The project is developed by a single person and is a portfolio project. It needs to demonstrate architecture design without the operational cost of multiple services.

## Decision

A single backend in NestJS, organized into modules with explicit boundaries. Modules communicate only through exported services.

## Alternatives considered

- **Microservices:** they add inter-service communication, multiple deployments, and distributed tracing. They offer no benefit with a single team and a single deployment.
- **Monolith without modules:** faster at the start, but business rules end up mixed into controllers and services.

## Consequences

- A single deployment and a single database simplify operations.
- If a module ever needed to scale separately, the modular separation makes it easier to extract later.
- Module boundaries need discipline. A module that reads another's tables breaks the decision.
