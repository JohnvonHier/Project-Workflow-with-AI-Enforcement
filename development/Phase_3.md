# Phase 3 – Decompose into Independent Modules

## Goal

Decompose the workflow engine into cohesive, independently implementable modules with clear responsibilities, minimal coupling, and well-defined public interfaces.

The architecture should follow a service-oriented approach where the workflow engine orchestrates high-level behavior while each module encapsulates its own implementation details.

---

# Architectural Principles

* Single Responsibility Principle for every module.
* One public façade (service) per module.
* Modules communicate only through public interfaces.
* Internal implementation details remain private.
* High cohesion, low coupling.
* Utilities may only depend on the Python standard library.
* The workflow engine coordinates services but contains minimal business logic.

---

# Module Structure

```text
workflow_engine/
│
├── cli/
│
├── configuration/
│   ├── manifests/
│   ├── settings/
│   └── schema/
│
├── workflow/
│   ├── engine/
│   ├── state_machine/
│   ├── execution/
│   └── transitions/
│
├── pipeline/
│   ├── prompt_builder/
│   ├── routing/
│   ├── parsing/
│   ├── extraction/
│   ├── validation/
│   └── adapters/
│
├── validation/
│   ├── input/
│   ├── output/
│   ├── workflow/
│   ├── artifacts/
│   └── manifests/
│
├── artifacts/
│
├── context/
│
├── guidance/
│
├── git/
│
├── persistence/
│   └── transactions/
│
├── plugins/
│
├── plugin_api/
│
├── contracts/
│
├── domain/
│   ├── models/
│   ├── value_objects/
│   ├── enums/
│   ├── events/
│   └── exceptions/
│
├── logging/
│
└── utils/
```

---

# Module Responsibilities

## CLI

Responsible for all user interaction.

Responsibilities:

* Command parsing
* Interactive user interface
* Progress display
* User input

Does **not** contain workflow logic.

---

## Configuration

Responsible for loading and validating project configuration.

Responsibilities:

* Project manifests
* Global settings
* Configuration schemas

Plugin loading is intentionally **not** handled here.

---

## Workflow

Responsible for orchestrating the software development process.

Submodules:

### Engine

Coordinates the workflow.

Responsibilities:

* Execute current workflow state
* Coordinate services
* Handle state transitions

### State Machine

Defines the deterministic workflow.

Responsibilities:

* State definitions
* Allowed transitions
* State metadata

### Execution

Executes workflow states.

Responsibilities:

* Invoke required services
* Execute workflow actions
* Handle execution flow

### Transitions

Determines the next valid state.

Responsibilities:

* Transition rules
* Transition validation
* Next-state computation

---

## Pipeline

Responsible for all LLM interactions.

Responsibilities:

* Prompt generation
* Context preparation
* LLM routing
* Response parsing
* Structured extraction
* Response validation

The workflow engine interacts only with the pipeline, never directly with prompt generation or parsing.

---

## Validation

Responsible for validating all workflow boundaries.

Submodules:

* Input validation
* Output validation
* Workflow validation
* Artifact validation
* Manifest validation

Validation occurs before every workflow transition.

---

## Artifacts

Responsible for managing project artifacts as first-class domain concepts.

Examples:

* Project Constitution
* Architecture Summary
* Sprint Plan
* Current Task
* Completion Report
* Validation Report

Artifacts are domain objects rather than arbitrary files.

---

## Context

Responsible for context management across the workflow.

Responsibilities:

* Context selection
* Context compression
* Summarization
* History reduction
* Token budgeting

---

## Guidance

Responsible for guiding required human interaction.

Responsibilities:

* Manual instructions
* Checklists
* Confirmations
* Required actions
* Next-step guidance
* Reminders

---

## Git

Responsible for repository management.

Responsibilities:

* Commits
* Branches
* Tags
* Checkpoints
* Repository validation
* Recovery support

---

## Persistence

Responsible for storing workflow state.

Responsibilities:

* Project state
* Snapshots
* Workflow history
* Serialization
* Atomic transactions

State updates should be transactional whenever possible.

---

## Plugins

Responsible for plugin discovery and execution.

Responsibilities:

* Plugin loading
* Plugin lifecycle
* Plugin registration
* Plugin execution

---

## Plugin API

Defines the interfaces used by plugins.

Responsibilities:

* Plugin contracts
* Extension interfaces
* Version compatibility

The Plugin API is infrastructure, not a plugin.

---

## Contracts

Defines all public service interfaces shared across modules.

Examples:

* ValidationService
* PipelineService
* ArtifactService
* GitService
* ContextService

Modules communicate through contracts rather than concrete implementations.

---

## Domain

Contains shared domain concepts.

Responsibilities:

* Models
* Value Objects
* Enums
* Events
* Exceptions

Domain does **not** contain service interfaces.

---

## Logging

Responsible for auditability and diagnostics.

Responsibilities:

* Event logging
* Audit log
* Diagnostics
* Error reporting

---

## Utilities

Contains generic helper functions.

Rules:

* May only depend on the Python standard library.
* Must never depend on any project module.
* Any module may depend on utilities.

---

# Dependency Architecture

```text
                 CLI
                  │
                  ▼
          Workflow Engine
                  │
      ┌───────────┼───────────┐
      ▼           ▼           ▼
 Pipeline   Validation   Guidance
      │           │
      ▼           ▼
   Context    Artifacts
      │           │
      └──────┬────┘
             ▼
       Persistence
             │
      ┌──────┼──────┐
      ▼      ▼      ▼
     Git   Logging Plugins

All modules communicate through Contracts.
```

---

# Design Rules

1. Every module exposes a single public service façade.
2. Modules communicate only through public contracts.
3. The workflow engine contains orchestration logic only.
4. Business logic belongs inside the owning module.
5. Validation precedes every workflow transition.
6. Workflow state is deterministic.
7. Persistence operations should be atomic.
8. Artifacts are first-class domain objects.
9. Internal module implementation details remain private.
10. Utilities are dependency leaves and may only use the Python standard library.

---

# Expected Outcome

The resulting architecture provides:

* Independent module implementation
* Deterministic workflow orchestration
* Minimal coupling
* High cohesion
* Strong validation boundaries
* Clear extension points
* Plugin support
* Robust state management
* Improved maintainability
* Future support for additional languages, tools, and workflows without architectural changes.
