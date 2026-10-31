# ADR 001: PostgreSQL with Docker and Flyway

Date: 2026-10-31
Status: Accepted

## Context

The application needs a relational database for shipments,
tracking events, warehouses, storage locations, and pallets.
Local setup must be reproducible, and schema changes must
be tracked in Git.

## Decision

Use PostgreSQL as the application database and run it locally
in Docker Compose.

Use a named Docker volume to preserve database data.

Manage schema changes with Flyway migrations.
Hibernate will validate mappings rather than create or update tables.
Database credentials will not be committed to Git.

## Alternatives considered

- H2: not selected as the main database because the final submission
  requires PostgreSQL or MySQL.
- Manually installed PostgreSQL: not selected because it requires
  machine-specific installation and configuration.
- Hibernate automatic schema updates: not selected because explicit
  migrations provide a reviewable history of schema changes.

## Consequences

The database setup and schema changes are reproducible.
However, Docker must be running during local development,
and database changes require migration files.

## M1 verification

PostgreSQL is running in Docker.
The Spring Boot application successfully applied Flyway migration V1,
confirmed by a successful entry in flyway_schema_history.

The application runs from IntelliJ; only the database runs in Docker.
