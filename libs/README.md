# libs

Shared internal libraries consumed by services in `apps/`. These are plain JAR libraries — not executable Spring Boot applications.

## Modules

### shared-utils

`groupId: com.khush` | `artifactId: shared-utils`

Provides cross-cutting concerns that every service needs:

| Package | Contents |
|---|---|
| `com.khush.security` | `SecurityConfig` — BCrypt `PasswordEncoder` bean, `SecurityFilterChain` (all `/api/**` routes are open) |
| `com.khush.exceptions` | `GlobalExceptionHandler` — `@RestControllerAdvice` for validation errors; `ErrorResponse` DTO |
| `com.khush.common` | `Categories` enum — canonical list of product category types |

**Database schema** — `database/sql/create_tables.sql` defines the full PostgreSQL schema: `users`, `categories`, `products`, `inventory`, `carts`, `addresses`, `transactions`, and the `category_type` native enum.

## Using a library in a service

1. The library version is managed in the root `pom.xml` `<dependencyManagement>` block.
2. Add it to the service's `<dependencies>`:

```xml
<dependency>
    <groupId>com.khush</groupId>
    <artifactId>shared-utils</artifactId>
</dependency>
```

3. Because `SecurityConfig` lives under `com.khush`, it is picked up automatically by `@SpringBootApplication` component scanning in any service whose main class is also in the `com.khush` base package.

## Building

```bash
cd libs/shared-utils
./mvnw clean install
```