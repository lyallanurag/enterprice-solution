# Git Strategy

**Document ID:** DEV-GIT-001
**Version:** 1.0
**Status:** Approved
**Owner:** Platform Engineering Team
**Last Updated:** July 2026

---

# Purpose

This document defines the Git strategy for the Enterprise Business Platform.

It establishes the repository model, branching philosophy, collaboration workflow, release process, and deployment alignment used throughout the project.

The goal is to provide a scalable Git workflow that supports:

* Enterprise Architecture
* Domain-Driven Design
* Nx Monorepo
* AWS ECS Deployments
* Continuous Integration
* Continuous Delivery

---

# Guiding Principles

The Git workflow follows these principles.

* One source of truth.
* Small and frequent changes.
* Short-lived branches.
* Continuous integration.
* Continuous deployment readiness.
* Trunk-Based Development.
* Documentation as Code.
* Architecture as Code.

Git history should clearly communicate the evolution of the platform.

---

# Repository Model

The platform uses a single Git repository.

```text
Enterprise Business Platform

├── apps/
├── libs/
├── infrastructure/
├── tools/
├── scripts/
└── docs/
```

The repository contains:

* Product documentation
* Architecture documentation
* Source code
* Infrastructure code
* Deployment configuration
* Development tooling

All artifacts evolve together.

---

# Monorepo Strategy

The project uses an Nx Monorepo.

Reasons include:

* Shared domain libraries.
* Consistent dependency management.
* Incremental builds.
* Incremental testing.
* Incremental deployments.
* Shared tooling.
* Simplified developer experience.

The Git strategy is optimized for monorepo development.

---

# Branching Philosophy

The project follows **Trunk-Based Development**.

Permanent branch:

```text
main
```

Temporary branches:

```text
feature/*
bugfix/*
hotfix/*
docs/*
infra/*
release/*
```

No long-lived development branches are maintained.

---

# Branch Types

## main

The main branch always represents the latest stable architecture and implementation.

Every commit to main must be deployable.

---

## feature/*

Used for new capabilities.

Examples:

```text
feature/identity

feature/platform-product-management

feature/ticket-management

feature/custom-software-delivery

feature/delivery-provider
```

Feature branches should remain short-lived.

---

## bugfix/*

Used for non-critical defects.

Example:

```text
bugfix/session-timeout
```

---

## hotfix/*

Used for urgent production fixes.

Example:

```text
hotfix/payment-failure
```

---

## docs/*

Used for documentation updates.

Examples:

```text
docs/business-model

docs/context-registry

docs/aws-architecture
```

Documentation changes follow the same review process as source code.

---

## infra/*

Used for infrastructure changes.

Examples:

```text
infra/networking

infra/ecs

infra/codepipeline
```

---

## release/*

Created only when preparing a production release.

Example:

```text
release/v1.0.0
```

Release branches are temporary.

---

# Environment Strategy

Git branches do not represent deployment environments.

Deployment environments are managed independently through CI/CD pipelines.

| Environment | Deployment Source |
| ----------- | ----------------- |
| Development | main              |
| Staging     | release/*         |
| Production  | Git Tag           |

This separation simplifies deployment management.

---

# Git Workflow

```text
Create Feature Branch

↓

Develop

↓

Commit Frequently

↓

Push

↓

Pull Request

↓

Code Review

↓

Continuous Integration

↓

Merge into main

↓

Automatic Development Deployment

↓

Release Branch (when required)

↓

Staging Deployment

↓

Git Tag

↓

Production Deployment
```

---

# Pull Request Policy

Every change must be submitted through a Pull Request.

Direct commits to the main branch are prohibited.

Every Pull Request must:

* Pass CI.
* Pass linting.
* Pass automated tests.
* Pass code review.
* Resolve merge conflicts.
* Update documentation when necessary.

---

# Documentation as Code

Architecture documents are version-controlled alongside source code.

Documentation changes follow the same lifecycle as implementation.

Architecture documentation must evolve together with the software.

---

# Architecture as Code

The repository treats architectural artifacts as first-class engineering assets.

Examples include:

* Architecture Decision Records
* Domain Models
* Context Registries
* Capability Catalogs
* Software Architecture Documents

Architecture evolves through Pull Requests rather than isolated documents.

---

# Commit Strategy

The project adopts Conventional Commits.

Examples:

```text
feat(identity): add user registration

feat(ticket-management): implement ticket aggregate

docs(product): refine business model

fix(billing): resolve invoice calculation

refactor(notification): simplify event publisher

infra(ecs): configure auto scaling
```

Commit messages should clearly communicate intent.

---

# Release Strategy

Production deployments occur only from version tags.

Example:

```text
v1.0.0
```

Release branches exist solely to stabilize production releases.

---

# Branch Protection

The main branch should enforce:

* Pull Request required
* Passing CI required
* Successful code review
* No direct pushes
* Linear history preferred

---

# Nx Integration

Feature development should align with domain boundaries.

Examples:

```text
feature/identity

feature/marketplace

feature/billing

feature/platform-product-management
```

Git branches should reflect business capabilities rather than UI pages.

---

# CI/CD Integration

Every Pull Request triggers:

* Lint
* Unit Tests
* Build
* Nx Affected Analysis
* Docker Build (affected applications only)
* Security Checks

Every merge to main triggers:

* Docker Image Build
* Push to Amazon ECR
* Deployment to Development Environment

---

# Versioning

The project follows Semantic Versioning.

Examples:

```text
v1.0.0

v1.0.1

v1.1.0

v2.0.0
```

Production releases are identified by Git tags.

---

# Governance

Git is the single source of truth for:

* Architecture
* Source Code
* Infrastructure
* Documentation
* Deployment Configuration

All changes must be traceable through Git history.

---

# Related Documents

* branching-strategy.md
* development-workflow.md
* commit-conventions.md
* pull-request.md
* release-strategy.md
* ../08-devops/cicd.md
* ../02-software-architecture/nx-workspace.md
