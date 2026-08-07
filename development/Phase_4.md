# Phase 4 – Freeze Module Contracts

## Goal

Define stable contracts for each module before implementation begins.

This phase freezes the architectural boundaries of the system by defining each module's purpose, responsibilities, ownership, dependencies, and guarantees. It intentionally does **not** freeze concrete method names or implementation details.

The objective is to ensure that every module can be implemented independently while preserving a stable overall architecture.

---

# Architectural Principles

* One public façade per module.
* One primary responsibility per module.
* Modules communicate only through public façades.
* Internal implementation details remain private.
* Freeze responsibilities, ownership, and boundaries—not method names.
* Business logic belongs to the module that owns it.
* The Workflow Service coordinates modules but never implements their business logic.

---

# Module Contract Template

Every module contract should define:

* Purpose
* Responsibilities
* Owned Data
* Capabilities
* Consumes
* Produces
* Errors
* Required Dependencies
* Optional Dependencies
* Public Façade
* Architectural Guarantees
* Stability Guarantees

---

# Workflow Service

## Purpose

Coordinate the deterministic software development workflow.

## Responsibilities

* Coordinate workflow execution.
* Execute the current workflow state.
* Determine valid state transitions.
* Coordinate module façades.
* Handle workflow recovery.

## Owned Data

None.

The Workflow Service orchestrates the workflow but does not own workflow state or business data.

## Capabilities

* Start a workflow.
* Resume a workflow.
* Execute the current state.
* Coordinate state transitions.
* Recover from failed execution.

## Consumes

* Current workflow state
* Validation results
* Pipeline results
* Configuration

## Produces

* Workflow transitions
* Workflow events

## Errors

* Invalid transition
* Missing prerequisite
* Workflow execution failure

## Required Dependencies

* State Service
* Validation Service
* Pipeline Service
* Context Service
* Artifact Service
* Persistence Service
* Git Service

## Optional Dependencies

* Plugin Service

## Public Façade

WorkflowService

## Architectural Guarantees

* At most one workflow transition executes at a time.
* Every transition is validated before execution.
* Every completed transition is persisted.
* The Workflow Service never implements business logic belonging to another module.

## Stability Guarantees

* Coordinates modules only.
* Module ownership remains stable.

---

# State Service

## Purpose

Own and manage project workflow state.

## Responsibilities

* Store current workflow state.
* Maintain workflow history.
* Record transitions.
* Provide state queries.

## Owned Data

* Current workflow state
* State history
* Transition history

## Capabilities

* Query current state.
* Update workflow state.
* Restore previous state.
* Record transition history.

## Consumes

* Workflow transitions

## Produces

* Current workflow state
* State events

## Errors

* Invalid state
* Corrupted state

## Required Dependencies

* Persistence Service

## Optional Dependencies

None

## Public Façade

StateService

## Architectural Guarantees

* Exactly one active workflow state always exists.
* Every state transition is recorded.
* State history is append-only.

## Stability Guarantees

* Sole owner of workflow state.

---

# Pipeline Service

## Purpose

Coordinate all interactions with LLMs.

## Responsibilities

* Generate prompts.
* Route requests.
* Parse responses.
* Extract structured information.

Validation is intentionally handled by the Validation Service.

## Owned Data

* Pipeline execution metadata

## Capabilities

* Generate prompts.
* Route requests.
* Parse responses.
* Extract structured artifacts.

## Consumes

* Context
* Workflow state
* Artifacts

## Produces

* Parsed pipeline results
* Extracted artifacts

## Errors

* Prompt generation failure
* Routing failure
* Parsing failure
* Extraction failure

## Required Dependencies

* Context Service

## Optional Dependencies

* Plugin Service

## Public Façade

PipelineService

## Architectural Guarantees

* Pipeline execution is deterministic for identical inputs.
* Pipeline does not perform validation.
* Pipeline does not modify workflow state.

## Stability Guarantees

* Owns all LLM interaction logic.

---

# Validation Service

## Purpose

Validate workflow boundaries and system consistency.

## Responsibilities

* Validate workflow transitions.
* Validate inputs.
* Validate outputs.
* Validate cross-artifact consistency.
* Validate manifests.

## Owned Data

None.

## Capabilities

* Validate before transitions.
* Validate after transitions.
* Validate workflow consistency.
* Validate manifests.
* Validate cross-artifact relationships.

## Consumes

* Workflow state
* Pipeline results
* Artifacts
* Configuration

## Produces

* Validation results

## Errors

* Validation failure

## Required Dependencies

None

## Optional Dependencies

* Plugin Service

## Public Façade

ValidationService

## Architectural Guarantees

* Every workflow transition is validated.
* Validation never mutates system state.
* Validation performs only consistency checks.

## Stability Guarantees

* Owns all workflow-level validation.

---

# Artifact Service

## Purpose

Manage project artifacts as first-class domain objects.

## Responsibilities

* Manage artifact lifecycle.
* Manage artifact versions.
* Perform structural artifact validation.

## Owned Data

* Project Constitution
* Architecture Summary
* Sprint Plan
* Current Task
* Completion Report
* Other project artifacts

## Capabilities

* Read artifacts.
* Write artifacts.
* Version artifacts.
* Validate artifact structure.

## Consumes

* Pipeline outputs

## Produces

* Project artifacts

## Errors

* Invalid artifact
* Version conflict

## Required Dependencies

* Persistence Service

## Optional Dependencies

None

## Public Façade

ArtifactService

## Architectural Guarantees

* Every artifact has exactly one owner.
* Structural validation belongs to the Artifact Service.
* Artifact history remains versioned.

## Stability Guarantees

* Sole owner of artifact lifecycle.

---

# Context Service

## Purpose

Manage project context for LLM interactions.

## Responsibilities

* Build context.
* Select relevant context.
* Compress context.
* Manage token budgets.

## Owned Data

* Context representations
* Context cache

## Capabilities

* Build context.
* Select context.
* Compress context.
* Estimate token usage.

## Consumes

* Workflow state
* Artifacts

## Produces

* Optimized context

## Errors

* Context generation failure

## Required Dependencies

* Artifact Service

## Optional Dependencies

* Plugin Service

## Public Façade

ContextService

## Architectural Guarantees

* Context is derived from project artifacts.
* Multiple context representations may coexist.
* Context generation is reproducible.

## Stability Guarantees

* Sole owner of project context.

---

# Guidance Service

## Purpose

Guide required human interaction throughout the workflow.

## Responsibilities

* Present instructions.
* Present checklists.
* Request confirmations.
* Recommend next actions.
* Display reminders.

## Owned Data

None.

## Capabilities

* Generate user guidance.
* Generate checklists.
* Generate instructions.
* Confirm manual actions.

## Consumes

* Current workflow state

## Produces

* Guidance instructions

## Errors

None

## Required Dependencies

* State Service

## Optional Dependencies

None

## Public Façade

GuidanceService

## Architectural Guarantees

* Guidance never changes workflow state.
* Guidance is derived from the current workflow state.

## Stability Guarantees

* Sole owner of user guidance.

---

# Git Service

## Purpose

Interact with the Git repository.

## Responsibilities

* Repository interaction.
* Commit management.
* Branch management.
* Recovery support.
* Repository validation.

## Owned Data

None.

## Capabilities

* Inspect repository state.
* Commit changes.
* Roll back changes.
* Manage branches.
* Manage tags.

## Consumes

* Workflow events

## Produces

* Repository updates

## Errors

* Git operation failure

## Required Dependencies

None

## Optional Dependencies

None

## Public Façade

GitService

## Architectural Guarantees

* Never modifies workflow state.
* Repository operations remain isolated from orchestration logic.

## Stability Guarantees

* Sole owner of Git interaction.

---

# Persistence Service

## Purpose

Persist project data safely and atomically.

## Responsibilities

* Persist workflow state.
* Persist artifacts.
* Manage snapshots.
* Support transactions.

## Owned Data

Persistent project storage.

## Capabilities

* Load data.
* Save data.
* Restore snapshots.
* Execute transactional operations.

## Consumes

* Workflow state
* Artifacts

## Produces

* Persistent storage

## Errors

* Persistence failure
* Transaction failure

## Required Dependencies

None

## Optional Dependencies

None

## Public Façade

PersistenceService

## Architectural Guarantees

* Atomic writes.
* Crash consistency.
* Version-compatible persistence.
* Transactional updates.

## Stability Guarantees

* Sole owner of persistent storage.

---

# Configuration Service

## Purpose

Manage project configuration.

## Responsibilities

* Read manifests.
* Read settings.
* Validate configuration.
* Resolve configuration.

## Owned Data

* Project manifest
* Global settings

## Capabilities

* Read configuration.
* Validate configuration.
* Resolve configuration.

## Consumes

* Configuration files

## Produces

* Resolved configuration

## Errors

* Invalid configuration

## Required Dependencies

None

## Optional Dependencies

* Plugin Service

## Public Façade

ConfigurationService

## Architectural Guarantees

* Configuration resolution is deterministic.
* Configuration remains immutable during execution.

## Stability Guarantees

* Sole owner of configuration.

---

# Plugin Service

## Purpose

Manage the plugin ecosystem.

## Responsibilities

* Discover plugins.
* Load plugins.
* Register plugins.
* Manage plugin lifecycle.

## Owned Data

* Plugin registry
* Plugin metadata

## Capabilities

* Discover plugins.
* Register plugins.
* Load plugins.
* Unload plugins.
* Reload plugins.

## Consumes

* Plugin definitions

## Produces

* Active plugin registry

## Errors

* Plugin load failure
* Compatibility failure

## Required Dependencies

* Plugin API

## Optional Dependencies

None

## Public Façade

PluginService

## Architectural Guarantees

* Plugins are isolated from core modules.
* Plugin lifecycle is centrally managed.

## Stability Guarantees

* Sole owner of plugin management.

---

# Logging Service

## Purpose

Record system activity for diagnostics and auditing.

## Responsibilities

* Record workflow events.
* Record state transitions.
* Record validation results.
* Record errors.
* Maintain audit history.

## Owned Data

* Audit log
* Diagnostic log

## Capabilities

* Record structured log events.
* Record transitions.
* Record validation activity.
* Export logs.

## Consumes

* Structured log events

## Produces

* Structured logs

## Errors

* Logging failure

## Required Dependencies

None

## Optional Dependencies

None

## Public Façade

LoggingService

## Architectural Guarantees

* Logging never modifies business state.
* Logging is append-only.
* Log severity is an implementation detail.

## Stability Guarantees

* Sole owner of system logging.

---

# Cross-Module Architectural Rules

## Ownership

Every piece of business data has exactly one owning module.

Other modules may consume the data but may not own or modify it directly.

---

## Communication

Modules communicate only through public façades.

Direct access to another module's internal implementation is prohibited.

---

## Business Logic

Business logic belongs exclusively to the owning module.

The Workflow Service coordinates modules but never performs another module's responsibilities.

---

## Validation

Validation is performed before every workflow transition.

Structural validation belongs to the owning module.

Cross-module consistency validation belongs to the Validation Service.

---

## State

The State Service is the single source of truth for workflow state.

No other module may own workflow state.

---

## Persistence

All persistent changes must be atomic.

The Persistence Service is solely responsible for durability and consistency.

---

## Utilities

Utility modules may depend only on the Python standard library.

Every other module may depend on utilities.

Utilities may never depend on project modules.

---

# Expected Outcome

After completing this phase:

* Module boundaries are frozen.
* Ownership is explicitly defined.
* Responsibilities are clearly separated.
* Dependencies are documented.
* Architectural guarantees are established.
* Every module exposes a single stable public façade.
* Implementation teams can develop modules independently without changing the overall architecture.
