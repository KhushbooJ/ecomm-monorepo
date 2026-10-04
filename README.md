# ecomm-monorepo

A Maven multi-module monorepo for a mini e-commerce platform built with Spring Boot, PostgreSQL, Kafka, and Redis.

## Structure

```
ecomm-monorepo/
├── apps/               # Deployable Spring Boot services
│   └── order-service   # Handles orders and user registration
└── libs/               # Shared internal libraries
    └── shared-utils    # Security config, Redis cache, exception handling, common types
```

Both `apps/order-service` and `libs/shared-utils` are git submodules pointing to their own repositories.

## Prerequisites

- Java 17+
- Maven 3.9+
- Docker (for local infrastructure via Docker Compose)

## Building

Build all modules from the root:

```bash
./mvnw clean install
```

Modules are built in dependency order: `libs/shared-utils` is installed first, then `apps/order-service`.

To build a single module:

```bash
./mvnw clean install -pl libs/shared-utils
./mvnw clean install -pl apps/order-service
```

## Modules

| Module | Type | Description |
|---|---|---|
| [`libs/shared-utils`](libs/shared-utils/README.md) | Library | Security, Redis cache service, exception handling, shared enums |
| [`apps/order-service`](apps/order-service/README.md) | Service | Order management and user registration API |

## Infrastructure

Each service manages its own infrastructure via Docker Compose. Spring Boot automatically starts the required containers on application startup (`spring-boot-docker-compose`).

| Service | Image | Purpose |
|---|---|---|
| `order-db` | `postgres:16` | Order service database (host port `5433`) |
| `order-redis` | `redis:7` | User details cache (host port `6379`) |

## Submodule Setup

After cloning, initialise submodules:

```bash
git submodule update --init --recursive
```