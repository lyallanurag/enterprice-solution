# Business Capability Map

**Version:** 1.0 (Part 1 - Foundation)
**Status:** Draft
**Owner:** Enterprise Architecture Team
**Last Updated:** July 2026

---

# Purpose

The Business Capability Map defines **what the platform is capable of doing** from a business perspective.

It provides a stable representation of business capabilities independent of organizational structure, implementation technology, programming language, or deployment architecture.

The Business Capability Map serves as the primary reference for:

* Domain-Driven Design (DDD)
* Bounded Contexts
* Aggregate Design
* System Architecture
* Nx Workspace Organization
* API Design
* Database Architecture
* Event-Driven Architecture
* AWS Service Boundaries
* Team Ownership
* Product Planning

Every capability identified in this document should eventually map to one or more bounded contexts and software modules.

---

# What is a Business Capability?

A Business Capability represents **an ability the platform must possess** to achieve its business objectives.

A capability answers the question:

> **"What must the business be able to do?"**

A capability does **not** describe:

* Screens
* APIs
* Database tables
* Microservices
* Programming languages
* User interface flows

Instead, it represents a stable business function that remains valuable even as technology changes.

---

# Capability Design Principles

Every capability defined within the platform must follow these principles.

## Business First

Capabilities describe business value rather than technical implementation.

---

## Stable

Capabilities should remain valid even when implementation changes.

---

## Independent

Each capability should own its business rules and avoid unnecessary coupling.

---

## Composable

Capabilities should work together to deliver larger business processes while remaining independently understandable.

---

## Evolvable

Capabilities should support future expansion without requiring redesign of existing business functions.

---

## Technology Agnostic

Capabilities should never reference specific frameworks, cloud providers, databases, or programming languages.

---

# Capability Classification

All platform capabilities are classified into one of four categories.

## Core Capabilities

Capabilities required for the platform itself to operate.

Examples include:

* Identity & Access Management
* Billing & Payments
* Administration

Without these capabilities, the platform cannot function.

---

## Business Capabilities

Capabilities that directly deliver value to customer organizations.

Examples include:

* Marketplace
* Software Delivery
* Ticket Management

These capabilities represent the platform's primary commercial value.

---

## Supporting Capabilities

Capabilities that enable or improve other capabilities.

Examples include:

* Notifications
* Storage
* Analytics

Supporting capabilities rarely deliver standalone customer value but are essential for platform quality.

---

## Future Capabilities

Capabilities intentionally excluded from the MVP but planned for future platform evolution.

Examples include:

* Workflow Automation
* AI Services
* Third-Party Marketplace
* Enterprise Governance

---

# Capability Maturity Levels

Each capability progresses through one of four maturity stages.

| Level      | Description                                       |
| ---------- | ------------------------------------------------- |
| MVP        | Required for initial product launch               |
| Growth     | Planned after MVP to expand platform capabilities |
| Enterprise | Required for large-scale enterprise adoption      |
| Future     | Strategic capability planned for later evolution  |

Capability maturity supports long-term planning without changing the capability model itself.

---

# Capability Hierarchy

Every capability follows the same decomposition model.

```text
Business Capability
        │
        ▼
Sub-Capability
        │
        ▼
Business Function
        │
        ▼
Business Use Case
        │
        ▼
Domain
        │
        ▼
Aggregate
```

This hierarchy ensures traceability from business strategy to implementation.

---

# Platform Capability Landscape

The platform consists of thirteen primary business capabilities.

```text
Business Software Platform
│
├── Identity & Access Management
├── Marketplace
├── Software Delivery
├── Project Management
├── Ticket Management
├── Billing & Payments
├── Notification Management
├── Storage Management
├── Administration
├── Analytics & Reporting
├── Workflow Automation
├── Integration Services
└── Platform Operations
```

These capabilities represent the highest-level view of the platform and are intentionally technology-independent.

---

# Capability Ownership Principles

Every capability must have clearly defined ownership.

Ownership exists at two levels.

## Business Ownership

Defines who is responsible for business outcomes.

Examples:

* Product Management
* Finance
* Customer Success
* Platform Operations

---

## Technical Ownership

Defines who is responsible for implementation, maintenance, and operational excellence.

Examples:

* Backend Team
* Frontend Team
* Platform Engineering
* DevOps
* Security Engineering

Business ownership and technical ownership should always be documented independently.

---

# Capability Boundaries

Each capability should clearly define:

* Responsibilities
* Business rules
* Owned data
* Domain events
* External dependencies
* Integration points

Capabilities should avoid overlapping responsibilities.

If ownership is unclear, the capability boundaries should be reviewed before implementation begins.

---

# Relationship with Domain-Driven Design

The Business Capability Map is the starting point for Domain-Driven Design.

The relationship is illustrated below.

```text
Business Strategy
        │
        ▼
Business Capability Map
        │
        ▼
Bounded Contexts
        │
        ▼
Domains
        │
        ▼
Aggregates
        │
        ▼
Entities
        │
        ▼
Repositories
```

Business capabilities define **what** the platform must achieve.

Domain models define **how** those capabilities are implemented.

---

# Architectural Principles

The following principles govern every capability.

* Single Business Responsibility
* Explicit Ownership
* High Cohesion
* Low Coupling
* Clear Boundaries
* Event-Driven Collaboration
* Independent Evolution
* Documentation First
* Secure by Default
* Observable by Design

These principles apply regardless of implementation technology.

---

# What This Document Does Not Define

This document intentionally excludes:

* Detailed business processes
* User journeys
* Workflow diagrams
* API specifications
* Database schemas
* AWS architecture
* UI design
* Source code organization

Those subjects are documented in dedicated architecture documents.

---

# Document Roadmap

The complete Business Capability Map will be developed in the following stages.

## Part 1 — Foundation

* Purpose
* Principles
* Classification
* Capability Hierarchy
* Ownership Model

**Status:** Complete

---

## Part 2 — Capability Catalog

A complete catalog describing every primary capability, including:

* Capability ID
* Description
* Business Value
* Scope
* Sub-Capabilities
* Maturity
* Dependencies

---

## Part 3 — Capability Relationships

Defines how capabilities collaborate to deliver end-to-end business outcomes.

---

## Part 4 — Capability Dependency Matrix

Maps dependencies between capabilities and identifies foundational capabilities.

---

## Part 5 — Capability Traceability Matrix

Maps capabilities to:

* Bounded Contexts
* Domains
* Aggregates
* APIs
* Domain Events
* Nx Libraries
* AWS Services

This matrix becomes the architectural bridge between business and implementation.

---

# Related Documents

* `bounded-context-map.md`
* `business-processes.md`
* `../../00-product/vision.md`
* `../../00-product/business-model.md`
* `../../02-software-architecture/system-overview.md`
* `../../03-architecture-decisions/ADR-0008-domain-driven-design.md`
