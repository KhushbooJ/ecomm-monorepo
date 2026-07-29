# ecomm-monorepo

A Maven multi-module monorepo for a mini e-commerce platform built with Spring Boot, PostgreSQL, and Kafka.

## Structure

```
ecomm-monorepo/
├── apps/               # Deployable Spring Boot services
│   └── order-service   # Handles orders and user registration
└── libs/               # Shared internal libraries
    └── shared-utils    # Security config, exception handling, common types
```

## Prerequisites

- Java 17+
- Maven 3.9+
- PostgreSQL 15+
- Apache Kafka

## Building

Build all modules from the root:

```bash
./mvnw clean install
```

Modules are built in dependency order: `libs/shared-utils` is installed first, then `apps/order-service`.

## Modules

| Module | Type | Description |
|---|---|---|
| [`libs/shared-utils`](libs/shared-utils/README.md) | Library | Security, exception handling, shared enums |
| [`apps/order-service`](apps/order-service/README.md) | Service | Order management and user registration API |

## Database Setup

The database schema (PostgreSQL) is defined in `libs/shared-utils/database/sql/create_tables.sql`.
Run it against your PostgreSQL instance before starting any service.

```bash
psql -U <user> -d <database> -f libs/shared-utils/database/sql/create_tables.sql
```