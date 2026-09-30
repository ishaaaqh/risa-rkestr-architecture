# Repository Conventions

## Architecture repository

Contains:

- Requirements
- Architecture
- ADRs
- API governance
- Data model
- Flows
- Diagrams
- Sprint/ticket process

Does not contain application implementation code.

## Backend repository

Contains:

- Spring Boot application
- Domain/application/infrastructure implementation
- Tests
- Database migrations
- Local development infrastructure
- CI/CD configuration

## Frontend repository

Contains:

- Next.js application
- React/TypeScript features
- UI components
- Client-side tests
- CI/CD configuration

## Naming

Product: Rkestr

Core entity: Work Item

Company context: RISA

Java base package: `com.risa.rkestr`

API prefix: `/api/v1`

Database: `rkestr`

## Secrets

Never commit:

- Passwords
- API keys
- Private keys
- Tokens
- Production connection strings
- Real credentials

Use local environment variables / ignored `.env` files for development and managed secret storage for deployed environments.

## Documentation

Documentation should explain decisions and contracts, not duplicate implementation unnecessarily.
