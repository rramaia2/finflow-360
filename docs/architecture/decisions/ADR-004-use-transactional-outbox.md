# ADR-004: Use the Transactional Outbox Pattern

## Status

Accepted

## Context

When a payment is accepted, the system must save the payment in PostgreSQL and publish a corresponding event to Kafka.

Saving the database record and publishing directly to Kafka are separate operations. The database transaction could succeed while Kafka publication fails, leaving an accepted payment without a settlement event.

## Decision

Use the transactional outbox pattern to reliably publish payment and settlement events.

The application will store the business record and its outbox event in PostgreSQL within the same transaction. A separate publisher will read unpublished outbox records and send them to Kafka.

## Alternatives considered

- Publish directly to Kafka after the database commit

- Publish to Kafka before saving the payment

- Distributed two-phase commit

- Periodic polling of payment tables without an outbox

## Benefits

- Prevents accepted payments from silently losing their events

- Keeps business data and event creation atomic

- Supports reliable publication retries

- Avoids distributed transactions

- Provides a record of pending and published events

## Tradeoffs

- Requires an additional outbox table

- Introduces a publisher process or connector

- Events may be published more than once

- Published outbox records require retention and cleanup

- Publication introduces a small delay

## Consequences

Each service that publishes critical events must write an outbox record in the same transaction as its business update.

Outbox records must include a unique event ID, aggregate ID, event type, payload, creation time, publication status, retry count, and error information.

The publisher must retry temporary failures. Consumers must remain idempotent because duplicate publication is possible.