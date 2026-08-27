# ADR-006: Use Next.js for Customer and Operations Portals

## Status

Accepted

## Context

FinFlow 360 requires web portals for customers and operations users.

Customers need to submit payments and track transaction status. Operations users need to search payments, review failures, inspect reconciliation exceptions, and request controlled retries.

The frontend must support TypeScript, reusable components, secure authentication, API integration, responsive layouts, and automated testing.

## Decision

Use Next.js, React, and TypeScript to build the customer and operations portals.

Use shared UI components and role-aware navigation while keeping customer and operations functionality logically separated.

## Alternatives considered

- React with Vite

- Angular

- Vue.js with Nuxt

- Server-rendered templates in Spring Boot

## Benefits

- Strong React and TypeScript support

- File-based routing and layout management

- Support for client-side and server-side rendering

- Reusable component architecture

- Mature testing and frontend tooling ecosystem

- Straightforward integration with OAuth2 providers and REST APIs

## Tradeoffs

- Developers must understand server and client component boundaries

- Authentication requires careful token and session management

- Framework upgrades may introduce architectural changes

- Server-side features can increase deployment complexity

## Consequences

Frontend code will use TypeScript with strict type checking.

API contracts will be generated from or aligned with OpenAPI specifications. Protected pages must validate authentication and role permissions.

Customer users must only access their own transactions. Operations features must only be displayed and called by authorized roles.

Jest and React Testing Library will cover components, while Cypress or Playwright will cover critical user workflows.