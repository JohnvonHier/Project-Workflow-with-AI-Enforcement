# Phase 2 — System Design

Goal

Produce a complete implementation-independent system design. Every subsystem, interface, data contract, responsibility, and interaction is fully specified before implementation begins.

---

## 01. System Architecture

Purpose
- Define the overall system architecture.

Contents
- System Context Diagram
- Layered Architecture
- Component Diagram
- Responsibility Matrix
- Ownership Diagram
- Dependency Rules
- Extension Points
- Architectural Constraints

---

## 02. Workflow Design

Purpose
- Define the complete software development workflow.

Contents
- Workflow Graph
- Workflow Phases
- Entry Conditions
- Exit Conditions
- Optional Branches
- Cancel Paths
- Recovery Paths
- Validation Checkpoints
- Manual Actions

---

## 03. State Machine Design

Purpose
- Define deterministic execution.

Contents
- State Hierarchy
- State Definitions
- State Ownership
- State Invariants
- Transition Matrix
- Guard Conditions
- Failure States
- Recovery States
- Event Processing
- Persistence Rules

---

## 04. Data Model Design

Purpose
- Define every persistent entity.

Contents
- Entity Definitions
- Relationships
- Required Fields
- Optional Fields
- Validation Rules
- Serialization
- Versioning
- Migration Strategy

---

## 05. Interface Specification

Purpose
- Define every public interface between subsystems.

Contents
- Purpose
- Inputs
- Outputs
- Preconditions
- Postconditions
- Errors
- Ownership
- Examples

---

## 06. Pipeline Design

Purpose
- Define the complete information flow.

For every transition define
- Trigger
- Owner
- Produced Artifacts
- Consumed Artifacts
- Validation
- Failure Behaviour
- Success Behaviour

Also define
- Document Ownership
- Pipeline Inputs
- Pipeline Outputs
- LLM Responsibilities

---

## 07. Prompt System Design

Purpose
- Define prompt generation.

Contents
- Prompt Philosophy
- Prompt Templates
- Context Builder
- Variable Resolution
- Prompt Assembly
- Prompt Validation
- Token Budgeting
- Context Prioritization
- Prompt Versioning
- Response Parsing

---

## 08. Validation Design

Purpose
- Define every validation performed by the engine.

Contents
- Validation Categories
- Blocking Validations
- Warning Validations
- Informational Validations
- Validation Order
- Validation Pipeline
- Failure Behaviour

---

## 09. Capability Model

Purpose
- Define the responsibilities and permissions of every participant.

Contents
- Workflow Engine
- Architecture LLM
- Planning LLM
- Implementation LLM
- Validation LLM
- User
- Plugins

For each define
- May
- Must
- Must Not

---

## 10. Plugin Architecture

Purpose
- Define extensibility.

Contents
- Plugin Lifecycle
- Discovery
- Registration
- Interfaces
- Hooks
- Capabilities
- Permission Model
- Compatibility Rules
- Isolation

---

## 11. Persistence Design

Purpose
- Define persistent storage.

Contents
- State Storage
- Event Store
- Session Storage
- Cache
- History
- Recovery
- Backup Strategy
- Crash Consistency
- Atomic Writes

---

## 12. Git Integration Design

Purpose
- Define Git interaction.

Contents
- Git Abstraction Layer
- Repository Lifecycle
- Branch Policy
- Commit Policy
- Validation Gates
- Merge Policy
- Rollback
- Recovery

---

## 13. CLI Design

Purpose
- Define the user interface.

Contents
- Command Hierarchy
- Interactive Mode
- Non-Interactive Mode
- State-Aware Commands
- Menus
- Wizards
- Progress Reporting
- Error Messages
- Exit Codes

---

## 14. Error Handling Design

Purpose
- Define deterministic failure handling.

Contents
- Error Categories
- Internal Errors
- User Errors
- Recovery Strategies
- Retry Rules
- Abort Rules
- User Guidance

---

## 15. Logging Design

Purpose
- Define observability.

Contents
- Structured Log Format
- Log Levels
- Event Log
- State Log
- Prompt Log
- Validation Log
- Git Log
- Retention Policy

---

## 16. Project Layout

Purpose
- Define the filesystem layout.

Contents
- Directory Structure
- Persistent Files
- Generated Files
- Temporary Files
- Plugin Layout
- Workspace Layout

---

## 17. Module Architecture

Purpose
- Define internal implementation boundaries.

For every module define
- Responsibility
- Public API
- Owned Data
- Produced Events
- Consumed Events
- Dependencies
- Forbidden Dependencies
- Invariants

---

## 18. Testing Architecture

Purpose
- Define how the system architecture is verified.

Contents
- Test Pyramid
- Unit Strategy
- Integration Strategy
- State Machine Tests
- Pipeline Tests
- Interface Contract Tests
- Plugin Tests
- CLI Tests
- Regression Strategy

---

## 19. Security Architecture

Purpose
- Define trust and security boundaries.

Contents
- Trust Boundaries
- Trust Levels
- Permission Model
- Input Validation
- Output Validation
- Plugin Isolation
- Filesystem Access
- Command Execution
- Secret Handling

---

# Design Principles

1. Deterministic execution
2. Single source of truth
3. Explicit ownership
4. Explicit state
5. Validation before execution
6. Interface-first design
7. Minimal coupling
8. High cohesion
9. Plugin-first extensibility
10. Recoverability
11. Reproducibility
12. State-aware user guidance
13. Efficient LLM context usage
14. Minimal cognitive load
15. Every artifact has one owner
16. Every transition is validated
17. Every public interface is specified
18. Every module owns its own data
19. Every decision is traceable

---

# Phase 3

Implementation Planning

- Implementation Roadmap
- Milestones
- Increment Plan
- Delivery Order
- Risk Assessment
