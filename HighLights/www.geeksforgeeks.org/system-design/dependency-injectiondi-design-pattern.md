---
title: Dependency Injection(DI) Design Pattern - GeeksforGeeks
url: https://www.geeksforgeeks.org/system-design/dependency-injectiondi-design-pattern/
domain: www.geeksforgeeks.org
created: 2026-08-23 06:23
tags:
  - web-highlight
  - notaty
---

# Dependency Injection(DI) Design Pattern - GeeksforGeeks

- **Source URL:** [https://www.geeksforgeeks.org/system-design/dependency-injectiondi-design-pattern/](https://www.geeksforgeeks.org/system-design/dependency-injectiondi-design-pattern/)
- **Captured:** 2026-08-23 06:23

---

## Highlights

> "is a design pattern where an object receives its dependencies from an external source instead of creating them itself. It separates dependency creation from usage, improving flexibility, testability, and maintainability." `[YELLOW]`
— *Captured at 2026-08-23 06:14*

> "1. Client

The client is the class or component that depends on a service to perform its operations.

    It does not create or manage its dependencies
    It receives required services from the injector" `[YELLOW]`
— *Captured at 2026-08-23 06:15*

> "2. Service

The service is the class or component that provides specific functionality needed by the client.

    It contains the actual business logic
    It is designed to be independent of the client" `[YELLOW]`
— *Captured at 2026-08-23 06:15*

> "3. Injector

The injector is responsible for creating service instances and supplying them to the client.

    It manages dependency creation and lifecycle
    It injects required services at runtime" `[YELLOW]`
— *Captured at 2026-08-23 06:15*

> "4. Interface

The interface defines a contract that specifies what methods a service must implement.

    Clients depend on interfaces, not concrete classes
    It allows easy replacement of service implementations" `[YELLOW]`
— *Captured at 2026-08-23 06:16*

> "improved testability: easily inject mocks or test doubles to test components in isolation." `[YELLOW]`
— *Captured at 2026-08-23 06:16*

> "cross-cutting concerns: conveniently inject services like logging, security, or caching across multiple components." `[YELLOW]`
— *Captured at 2026-08-23 06:16*

> "With Constructor Injection, dependencies are provided to a class through its constructor when the object is created. This is the most common form of DI because it makes dependencies clear, mandatory, and immutable after the object is constructed." `[YELLOW]`
— *Captured at 2026-08-23 06:22*

