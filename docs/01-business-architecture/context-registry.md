# Context Registry

**Document ID:** BA-CTX-001
**Version:** 1.0 (Part 1 – Foundation)
**Status:** Draft
**Owner:** Enterprise Architecture Team
**Last Updated:** July 2026

---

# Purpose

The Context Registry is the authoritative catalog of all Bounded Contexts within the platform.

It defines the business boundaries, ownership, responsibilities, ubiquitous language, and architectural relationships of each context.

The Context Registry bridges Business Architecture and Domain-Driven Design by translating Business Capabilities into independently understandable and evolvable software models.

Every Bounded Context documented here is expected to evolve into one or more implementation modules while preserving its business autonomy.

---

# Objectives

The Context Registry exists to:

* Define explicit business boundaries.
* Prevent domain model leakage between contexts.
* Establish ownership of business concepts.
* Support Domain-Driven Design.
* Enable modular software architecture.
* Guide Nx workspace organization.
* Guide future service extraction.
* Provide traceability across the Architecture Knowledge Base.

---

# What is a Bounded Context?

A Bounded Context is the boundary within which a particular business model, terminology, and set of business rules are valid.

Within a context:

* Business language has one meaning.
* Aggregates enforce business consistency.
* Business rules are internally consistent.
* Data ownership is explicit.

Communication with other contexts occurs through well-defined integration mechanisms rather than shared domain models.

---

# Context Design Principles

Every Bounded Context must follow these principles.

## Single Business Responsibility

Each context owns one cohesive business capability or closely related set of responsibilities.

---

## Explicit Ownership

Every business concept has exactly one owning context.

No business object may have multiple owners.

---

## Independent Evolution

Contexts should evolve independently whenever possible.

Changes within one context should have minimal impact on others.

---

## Ubiquitous Language

Every context defines and owns its own business terminology.

The same word may have different meanings in different contexts.

---

## High Cohesion

Business concepts that change together belong together.

---

## Low Coupling

Contexts collaborate through events, APIs, or Anti-Corruption Layers—not shared domain objects.

---

## Traceability

Every context must map to:

* Business Capability
* Domain Model
* Aggregates
* APIs
* Events
* Nx Modules
* Infrastructure

---

# Domain Classification

The platform classifies contexts into five domain types.

| Type              | Description                                                         |
| ----------------- | ------------------------------------------------------------------- |
| Core Domain       | Represents the platform's primary competitive advantage.            |
| Platform Domain   | Provides foundational capabilities required for platform operation. |
| Supporting Domain | Enables or enhances core business capabilities.                     |
| Generic Domain    | Commodity functionality reused across the platform.                 |
| Future Domain     | Planned for future platform evolution.                              |

---

# Context Registry Index

| Context ID | Context Name                 | Domain Type       | Primary Capability | Status |
| ---------- | ---------------------------- | ----------------- | ------------------ | ------ |
| BC-001     | Identity & Access Management | Platform Domain   | CAP-001            | MVP    |
| BC-002     | Marketplace                  | Core Domain       | CAP-002            | MVP    |
| BC-003     | Software Delivery            | Core Domain       | CAP-003            | MVP    |
| BC-004     | Project Management           | Core Domain       | CAP-004            | MVP    |
| BC-005     | Ticket Management            | Core Domain       | CAP-005            | MVP    |
| BC-006     | Billing & Payments           | Supporting Domain | CAP-006            | MVP    |
| BC-007     | Notification Management      | Generic Domain    | CAP-007            | MVP    |
| BC-008     | Storage Management           | Generic Domain    | CAP-008            | MVP    |
| BC-009     | Administration               | Platform Domain   | CAP-009            | MVP    |
| BC-010     | Analytics & Reporting        | Supporting Domain | CAP-010            | Growth |
| BC-011     | Workflow Automation          | Future Domain     | CAP-011            | Future |
| BC-012     | Integration Services         | Future Domain     | CAP-012            | Growth |
| BC-013     | Platform Operations          | Platform Domain   | CAP-013            | MVP    |

---

# Context Ownership Model

Every Bounded Context must define:

* Business Owner
* Technical Owner
* Owned Business Concepts
* Owned Aggregates
* Published Events
* Consumed Events
* Integration Style
* Future Evolution Strategy

Ownership should never be ambiguous.

---

# Context Relationship Principles

Contexts communicate through clearly defined boundaries.

Approved collaboration mechanisms include:

* Domain Events
* REST APIs
* Asynchronous Messaging
* Anti-Corruption Layers (ACL)

Contexts must never directly manipulate another context's aggregates or persistence models.

---

# Ubiquitous Language

Every context maintains its own business vocabulary.

Examples include:

**Identity**

* User
* Organization
* Role
* Permission
* Session

**Marketplace**

* Product
* Subscription
* Pricing Plan
* Trial

**Software Delivery**

* Requirement
* Proposal
* Quotation
* Milestone

These vocabularies are documented in each domain's `ubiquitous-language.md`.

---

# Context Lifecycle

Each context progresses through four maturity stages.

| Stage      | Description                                    |
| ---------- | ---------------------------------------------- |
| MVP        | Initial implementation.                        |
| Growth     | Functional expansion.                          |
| Enterprise | Enterprise-grade capabilities and scalability. |
| Future     | Strategic roadmap initiatives.                 |

---

# Traceability Model

Every context participates in the following architectural traceability chain:

```text
Business Capability
        ↓
Bounded Context
        ↓
Subdomain
        ↓
Aggregate
        ↓
Entity
        ↓
Repository
        ↓
Application Service
        ↓
REST API
        ↓
Domain Event
        ↓
Nx Library
        ↓
AWS Infrastructure
```

This traceability model ensures architectural consistency across the platform.

---

# Governance

The Context Registry is maintained by the Enterprise Architecture Team.

Changes to context boundaries require:

1. Architecture review.
2. Impact analysis.
3. Approval through an Architecture Decision Record (ADR) when applicable.
4. Updates to related registries.

---

# Out of Scope

This document does not define:

* Aggregate implementation.
* Entity structures.
* Database schemas.
* REST APIs.
* Event payloads.
* Infrastructure deployment.

Those concerns are documented in their respective registries and architecture documents.

---

# Roadmap

This registry will evolve through the following stages:

**Part 1 – Foundation**

* Purpose
* Principles
* Classification
* Registry Index
* Governance

**Status:** Complete

---

**Part 2 – Context Specifications**

Each Bounded Context will be documented with:

* Mission
* Ownership
* Ubiquitous Language
* Aggregates
* Dependencies
* Integration Strategy
* Quality Attributes
* Future Extraction Strategy

---

**Part 3 – Context Collaboration**

* Upstream/Downstream Relationships
* Published Language
* Anti-Corruption Layers
* Event Flows

---

**Part 4 – Architecture Traceability**

Complete mapping to:

* Capability Registry
* Aggregate Registry
* Event Registry
* API Registry
* Nx Workspace
* AWS Architecture

---

# Related Documents

* `business-capability-map.md`
* `capability-catalog.md`
* `bounded-context-map.md`
* `../../04-domain-model/README.md`
* `../../03-architecture-decisions/ADR-0008-domain-driven-design.md`
