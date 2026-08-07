# Phase 5 – Bottom-up Implementation

## Goal

Implement the system as a translation of the completed design.

The implementation should strictly follow the architecture, module boundaries, and contracts defined in the previous phases. Higher-level components are only implemented after all required lower-level dependencies exist.

The implementation should prioritize deterministic behavior, low coupling, high cohesion, and continuous validation.

---

# Core Principles

- Build from the bottom up.
- Infrastructure before orchestration.
- The Workflow Engine is the final core component.
- The CLI is a thin presentation layer with almost no business logic.
- Every module has a single responsibility.
- Prefer composition over coupling.
- Validate before executing.
- Keep implementations small and testable.
- Continuously verify the architecture through integration.

---

# Architectural Categories

These categories describe the system architecture and responsibilities. They are **not** the implementation order.

## Foundation

Core utilities used throughout the system.

- Utilities
- Configuration
- Logging

---

## Project Model

Defines and manages the project's core data model.

- Manifest / Schema
- Artifact Service
- Persistence
- State Service

---

## Domain Logic

Contains the deterministic business logic of the application.

- Validation
- State Machine
- Context Service

---

## Integration

Adapters responsible for interacting with external systems.

- Git Adapter
- Prompt Builder
- Plugin System

---

## Application

Coordinates the complete application.

- Workflow Engine

---

## Presentation

User-facing interfaces.

- CLI

---

# Implementation Order

The implementation should generally proceed in the following order:

1. Utilities
2. Configuration
3. Manifest / Schema
4. Persistence
5. Artifact Service
6. State Service
7. Validation
8. Context Service
9. State Machine
10. Git Adapter
11. Prompt Builder
12. Plugin System
13. Workflow Engine
14. CLI
15. Logging (or earlier if useful)
16. Polish & Optimization

This order may be adjusted where practical, but higher-level modules should only depend on already implemented lower-level modules.

---

# Important Architectural Distinctions

## State Service vs State Machine

These are fundamentally different concerns.

### State Service

Responsible for persisted state.

- Owns project state
- CRUD-like operations
- Snapshots
- History
- Persistence coordination

### State Machine

Responsible for workflow logic.

- Defines legal transitions
- Enforces workflow rules
- Stateless transition logic
- Determines the next valid state

The State Machine never owns or persists state.

---

## Context Service

The Context Service acts as a bridge between the project model and prompt generation.

It consumes:

- Project State
- Artifacts
- Configuration

It produces:

- Prompt Context

The Prompt Builder should never gather context itself.

---

## Prompt Builder

The Prompt Builder is an integration adapter.

It consumes:

- Context
- Workflow State
- Templates
- Capabilities

It produces prompts for external LLMs.

It should contain no workflow logic.

---

## Git Adapter

The Git Adapter wraps Git functionality only.

It should not know about workflow concepts such as:

- Checkpoints
- Workflow stages
- Transactions
- Recovery

Those concerns belong to higher layers.

---

# Dependency Rule

Higher layers may depend on lower layers.

Lower layers must never depend on higher layers.

This dependency direction must never be violated.

---

# Vertical Slice Development

After the foundational pieces exist, implementation should proceed using small vertical slices rather than completing entire categories in isolation.

Each slice should exercise multiple modules together while remaining small and independently testable.

Example slices include:

### Slice 1

- Load Configuration
- Validate Manifest
- Create Initial State
- Persist State
- Display Project Status

### Slice 2

- Load Project
- Validate State
- Execute a State Transition
- Persist Updated State
- Log Transition

### Slice 3

- Build Context
- Generate Prompt
- Parse Response
- Update Artifacts
- Persist Changes

Each completed slice should produce a working, testable increment of the system.

---

# Design Goals

The implementation should ensure:

- Stable module boundaries
- Deterministic behavior
- Single ownership of every artifact
- Minimal coupling
- High cohesion
- Strong validation before every transition
- Thin presentation layer
- Continuous architectural verification
- Easy testing
- Easy future extension

Implementation should remain a straightforward translation of the architecture defined in the previous phases rather than introducing new architectural decisions.
