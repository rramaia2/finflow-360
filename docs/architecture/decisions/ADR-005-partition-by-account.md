# ADR-005: Partition Kafka Events by Account ID

## Status

Accepted

## Context

Kafka guarantees event ordering only within a partition.

Payments associated with the same account may contain dependent state changes. Processing those events out of order could produce invalid payment statuses, incorrect balances, or inconsistent reconciliation results.

## Decision

Use account ID as the Kafka message key for payment, settlement, and reconciliation events.

All events associated with the same account will therefore be routed to the same Kafka partition.

## Alternatives considered

- Partition by transaction ID

- Partition by event ID

- Use random partition assignment

- Use a single Kafka partition

## Benefits

- Preserves event ordering for the same account

- Supports account-level processing consistency

- Distributes different accounts across partitions

- Allows multiple consumers to process separate accounts concurrently

- Provides a stable and understandable partitioning strategy

## Tradeoffs

- High-volume accounts may create partition hotspots

- Account ID must be available in every relevant event

- Increasing partition counts does not automatically redistribute existing records

- Ordering is not guaranteed across different accounts

## Consequences

Every relevant event must include a valid account ID.

Producers must set the account ID as the Kafka record key. Consumers must validate permitted payment-state transitions even when ordering is preserved.

Partition distribution, consumer lag, and high-volume accounts must be monitored. A future ADR will be required if account-level hotspots become a significant scaling problem.