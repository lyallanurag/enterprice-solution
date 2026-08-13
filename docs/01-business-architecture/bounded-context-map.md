# Bounded Context Map

**Document ID:** BA-BCM-001
**Version:** 1.0 (Foundation)
**Status:** Draft
**Owner:** Enterprise Architecture Team
**Last Updated:** July 2026

---

# Purpose

The Bounded Context Map defines how the platform's bounded contexts collaborate while maintaining clear business boundaries.

It is the primary architectural document describing context relationships, integration patterns, dependency directions, and communication styles.

Unlike the Context Registry, which defines each context individually, the Bounded Context Map focuses on **how contexts interact**.

---

# Objectives

The Bounded Context Map exists to:

* Define collaboration between business domains.
* Prevent accidental coupling.
* Establish ownership boundaries.
* Guide API and event design.
* Guide Nx dependency rules.
* Guide future service decomposition.
* Maintain Domain-Driven Design integrity.

---

# Architectural Principles

Every relationship between contexts must follow these principles.

## Explicit Ownership

Every business concept has exactly one owning context.

---

## No Shared Domain Models

Contexts never share entities or aggregates.

Communication occurs only through:

* APIs
* Domain Events
* Published Contracts
* Anti-Corruption Layers

---

## Stable Dependencies

Dependencies should always point toward more stable contexts.

---

## Asynchronous First

Use asynchronous events whenever immediate consistency is not required.

---

## Synchronous Only When Necessary

REST APIs should be reserved for:

* Authentication
* Authorization
* Immediate validation
* User-facing synchronous operations

---

## Independent Evolution

Contexts should evolve independently without forcing simultaneous changes in dependent contexts.

---

# Context Collaboration Landscape

```text
                                     BC-001
                         Identity & Access Management
                                      │
          ┌───────────────────────────┼────────────────────────────┐
          │                           │                            │
          ▼                           ▼                            ▼
     BC-002                      BC-003                      BC-005
   Marketplace             Software Delivery         Ticket Management
          │                           │                            │
          │                           ▼                            │
          │                     BC-004 Project Management          │
          │                           │                            │
          └───────────────┬───────────┴───────────────┐            │
                          ▼                           ▼            ▼
                 BC-006 Billing & Payments     BC-008 Storage  BC-007 Notifications
                          │                           │            ▲
                          └──────────────┬────────────┘            │
                                         ▼                         │
                               BC-010 Analytics & Reporting ───────┘

                    BC-009 Administration supports all contexts

      BC-011 Workflow Automation
      BC-012 Integration Services
      BC-013 Platform Operations

            Cross-cutting capabilities supporting the entire platform
```

---

# Relationship Classification

The platform adopts the following Domain-Driven Design relationship patterns.

| Relationship                | Purpose                                            |
| --------------------------- | -------------------------------------------------- |
| Customer / Supplier         | Preferred collaboration model                      |
| Published Language          | Stable contracts shared between contexts           |
| Open Host Service           | Public integration interface                       |
| Anti-Corruption Layer (ACL) | Protect internal models from external influence    |
| Conformist                  | Consumer accepts supplier's model when appropriate |
| Shared Kernel               | Avoid whenever possible                            |

Shared Kernel should be considered a last resort.

---

# Communication Patterns

| Communication Style | Usage                                   |
| ------------------- | --------------------------------------- |
| REST API            | Immediate synchronous interactions      |
| Domain Events       | Business state changes                  |
| EventBridge         | Platform-wide asynchronous routing      |
| SQS                 | Reliable asynchronous processing        |
| ACL                 | Translation between incompatible models |

---

# Context Relationship Matrix

| Source Context                 | Target Context           | Relationship        | Integration Style |
| ------------------------------ | ------------------------ | ------------------- | ----------------- |
| BC-002 Marketplace             | BC-001 Identity          | Customer / Supplier | REST              |
| BC-003 Software Delivery       | BC-001 Identity          | Customer / Supplier | REST              |
| BC-005 Ticket Management       | BC-001 Identity          | Customer / Supplier | REST              |
| BC-004 Project Management      | BC-003 Software Delivery | Customer / Supplier | Domain Events     |
| BC-006 Billing & Payments      | BC-002 Marketplace       | Published Language  | Domain Events     |
| BC-006 Billing & Payments      | BC-003 Software Delivery | Published Language  | Domain Events     |
| BC-007 Notification Management | All Contexts             | Subscriber          | EventBridge       |
| BC-008 Storage Management      | Multiple Contexts        | Service Provider    | REST              |
| BC-010 Analytics & Reporting   | All Contexts             | Subscriber          | EventBridge       |
| BC-009 Administration          | All Contexts             | Platform Governance | REST              |

---

# Dependency Direction

Dependencies must always flow toward stable providers.

```text
Business Contexts
        │
        ▼
Platform Contexts
```

Example:

Marketplace depends on Identity.

Identity never depends on Marketplace.

---

# Context Independence Rules

Every context must:

* Own its own domain model.
* Own its own aggregates.
* Own its own persistence model.
* Publish meaningful domain events.
* Consume events without leaking external models.
* Avoid direct database access to another context.

---

# Future Service Extraction Strategy

The current implementation targets a **modular monolith**.

Future extraction candidates include:

| Context                      | Extraction Candidate |
| ---------------------------- | -------------------- |
| Identity & Access Management | High                 |
| Marketplace                  | High                 |
| Software Delivery            | High                 |
| Ticket Management            | High                 |
| Billing & Payments           | Medium               |
| Notification Management      | Medium               |
| Analytics & Reporting        | Medium               |

Extraction decisions should be based on business growth and operational needs, not premature optimization.

---

# Nx Dependency Alignment

Each bounded context maps to a dedicated domain library.

Example:

```text
libs/
└── domains/
    ├── identity/
    ├── marketplace/
    ├── software-delivery/
    ├── project-management/
    ├── ticket-management/
    ├── billing/
    ├── notification/
    ├── storage/
    ├── administration/
    ├── analytics/
    ├── workflow/
    ├── integration/
    └── platform-operations/
```

Nx dependency constraints should prevent domain libraries from introducing circular dependencies.

---

# AWS Alignment

Each context is designed so it can eventually become an independently deployable ECS service.

Typical mapping:

```text
Bounded Context
        ↓
Nx Domain Library
        ↓
REST API
        ↓
Docker Image
        ↓
Amazon ECR
        ↓
Amazon ECS Service
```

The deployment topology should evolve independently of business boundaries.

---

# Governance

Changes to context relationships require:

1. Architecture review.
2. Dependency impact analysis.
3. ADR if a boundary changes.
4. Updates to the Context Registry and related registries.

---

# Out of Scope

This document intentionally excludes:

* Aggregate design
* Entity modeling
* Database schemas
* API specifications
* Event payloads

These concerns are addressed in dedicated architecture artifacts.

---

# Related Documents

* `business-capability-map.md`
* `capability-catalog.md`
* `context-registry.md`
* `../../04-domain-model/README.md`
* `../../03-architecture-decisions/ADR-0008-domain-driven-design.md`
