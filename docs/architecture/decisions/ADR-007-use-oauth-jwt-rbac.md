# ADR-007: Use OAuth2, JWT, and Role-Based Access Control

## Status

Accepted

## Context

FinFlow 360 exposes sensitive payment, settlement, reconciliation, audit, and administrative functions.

Customers, partner systems, operations analysts, auditors, and administrators require different permissions. The platform must authenticate users and services without storing application passwords in individual backend services.

## Decision

Use OAuth2 and OpenID Connect for authentication, JWT access tokens for API authorization, and role-based access control for protected operations.

The initial roles will be CUSTOMER, PARTNER, OPERATIONS, AUDITOR, and ADMIN.

## Alternatives considered

- Application-managed username and password authentication

- Server-side sessions only

- API keys for all users and services

- Attribute-based access control as the initial authorization model

## Benefits

- Standards-based authentication and authorization

- Stateless API token validation

- Centralized identity management

- Support for interactive and machine-to-machine authentication

- Clear separation of permissions by role

- Strong integration with Spring Security and Next.js

## Tradeoffs

- Token expiration and refresh flows add complexity

- Revoking a JWT before expiration requires additional controls

- Incorrect role design can grant excessive permissions

- Identity-provider availability becomes an operational dependency

## Consequences

Spring Security will validate JWT signatures, issuer, audience, expiration, and required roles.

Customers may access only their own payment records even when they have the correct role. Operations users may investigate and retry eligible failures. Auditors will have read-only access. Administrators will manage roles and configuration.

Access tokens, refresh tokens, private keys, and secrets must never appear in logs or source control. Sensitive administrative actions must create audit records.