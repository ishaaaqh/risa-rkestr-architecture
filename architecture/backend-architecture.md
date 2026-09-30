# Backend Architecture

## Technology direction

- Java 21+
- Spring Boot
- Maven
- PostgreSQL
- Message Broker
- Object Storage
- Optional Redis
- Containerized runtime

## Modular structure

```text
com.risa.rkestr

identity/
workspace/
workitem/
classification/
deadline/
reminder/
notification/
search/
audit/
shared/
infrastructure/
```

Each module owns its domain/application/infrastructure concerns as appropriate.

## Layering

Conceptually:

```text
API
 |
Application
 |
Domain
 |
Infrastructure
```

The exact implementation may adapt where Spring integration requires it, but domain rules must not depend directly on transport concerns.

## Core principle

Business logic should not be distributed across controllers, database triggers, UI code, and message consumers without an explicit architectural reason.
