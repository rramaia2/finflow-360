# ADR-002: Use PostgreSQL as the Transactional Database

## Status

Accepted

## Context

FinFlow 360 must reliably store payments, account references, idempotency keys, settlement results, reconciliation records, outbox events, and audit history.

Payment processing requires ACID transactions, database constraints, indexing, relational integrity, and reliable concurrent updates.

## Decision

Use PostgreSQL as the primary transactional database for FinFlow 360.

Use Spring Data JPA and Hibernate for standard persistence operations, with native SQL where query performance or database-specific functionality requires it.

## Alternatives considered

- MySQL

- MongoDB

- Amazon DynamoDB

- CockroachDB

## Benefits

- Strong ACID transaction support

- Foreign keys and relational-integrity constraints

- Unique constraints for idempotency enforcement

- Reliable transaction isolation and concurrency control

- Advanced indexing and query capabilities

- JSONB support for flexible metadata

- Strong integration with Spring Data JPA

## Tradeoffs

- Schema migrations must be carefully managed

- Horizontal scaling is more complex than with some NoSQL databases

- Poorly designed queries or indexes can affect performance

- Database availability requires backups, replication, and operational monitoring

## Consequences

PostgreSQL schemas must be version-controlled using Flyway or Liquibase.

The payment and outbox records will be written within the same database transaction.

Idempotency keys will use unique database constraints. Frequently used search and processing fields must be indexed.

Amazon RDS for PostgreSQL will be used in AWS environments, with a local PostgreSQL container used for development.