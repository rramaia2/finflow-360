# ADR-003: Use Kafka for Asynchronous Processing

## Status

Accepted

## Context

Payment intake must remain responsive even when settlement processing is slow
or temporarily unavailable.

## Decision

Use Apache Kafka to separate payment intake from settlement and reconciliation.

## Alternatives considered

- Direct synchronous service calls
- Database polling
- AWS SQS

## Benefits

- High-throughput event processing
- Consumer independence
- Event replay
- Partition-based ordering

## Tradeoffs

- Additional operational complexity
- Eventual consistency
- Schema-version management
- Duplicate-delivery handling

## Consequences

Consumers must be idempotent, Kafka lag must be monitored, and failed events
must use retry and dead-letter topics.