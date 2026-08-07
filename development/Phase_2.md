# Phase 2 — System Design

## 01. System Architecture
- System Context Diagram
- Layered Architecture
- Component Diagram
- Responsibility Matrix
- Ownership Diagram
- Dependency Rules
- Extension Points
- Architectural Constraints
- System Integration Diagram

---

## 02. Data Model Design
- Entity Definitions
- Relationships
- Required Fields
- Optional Fields
- Derived Fields
- Validation Rules
- Serialization
- Versioning
- Migration Strategy

---

## 03. Integration Specification
- CLI Interface
- Git Interface
- LLM Interface
- Plugin Interface
- Manifest Interface
- Configuration Interface

For each:
- Purpose
- Inputs
- Outputs
- Preconditions
- Postconditions
- Errors
- Ownership
- Versioning
- Examples

---

## 04. Internal Interface Specification
- Workflow Engine
- Pipeline Engine
- State Machine
- Validation Engine
- Prompt Engine
- Persistence Layer
- Logging
- Event Bus
- Configuration Manager

For each:
- Purpose
- Provider
- Consumer
- Inputs
- Outputs
- Events
- Preconditions
- Postconditions
- Errors
- Invariants

---

## 05. Workflow Design
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

## 06. State Machine Design
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

## 07. Pipeline Design

For every transition define:
- Trigger
- Owner
- Produced Artifacts
- Consumed Artifacts
- Validation
- Failure Behaviour
- Success Behaviour

Also define:
- Pipeline Inputs
- Pipeline Outputs
- Information Flow
- Document Ownership
- LLM Responsibilities

---

## 08. Authority Model

For every actor define:
- Responsibilities
- Authority
- Allowed Actions
- Forbidden Actions
- Owned Artifacts
- Produced Outputs
- Required Inputs
- Validation Responsibilities

Actors:
- Workflow Engine
- User
- Architecture LLM
- Planning LLM
- Implementation LLM
- Validation LLM
- Plugins

---

## 09. Prompt System Design
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

## 10. Validation Design
- Validation Categories
- Automatic Validation
- Manual Validation
- Blocking Validations
- Warning Validations
- Informational Validations
- Validation Order
- Failure Behaviour

---

## 11. Persistence Design
- State Storage
- Event Store
- Session Storage
- Cache
- History
- Transaction Model
- Recovery
- Backup Strategy
- Crash Consistency
- Atomic Writes

---

## 12. Git Integration Design
- Git Abstraction Layer
- Repository Lifecycle
- Branch Policy
- Commit Policy
- Validation Gates
- Merge Policy
- Rollback
- Recovery

---

## 13. Plugin Architecture
- Plugin Lifecycle
- Discovery
- Registration
- Interfaces
- Hooks
- Permission Model
- Capabilities
- Compatibility
- Isolation

---

## 14. CLI Design
- Command Hierarchy
- Interactive Mode
- Non-Interactive Mode
- State-Aware Commands
- Workflow Guidance
- Menus
- Wizards
- Progress Reporting
- Error Messages
- Exit Codes

---

## 15. Error Handling Design
- Error Categories
- Internal Errors
- User Errors
- Recovery Strategies
- Retry Rules
- Abort Rules
- User Guidance

---

## 16. Logging Design
- Structured Log Format
- Log Levels
- Event Log
- Audit Log
- State Log
- Prompt Log
- Validation Log
- Git Log
- Retention Policy

---

## 17. Configuration Resolution
- Configuration Sources
- Resolution Order
- Defaults
- Overrides
- Environment Variables
- Runtime Values
- Conflict Resolution
- Validation
- Effective Configuration

---

## 18. Project Layout
- Directory Structure
- Persistent Files
- Generated Files
- Temporary Files
- Plugin Layout
- Workspace Layout

---

## 19. Module Architecture

For every module define:
- Responsibility
- Public API
- Owned Data
- Produced Events
- Consumed Events
- Dependencies
- Forbidden Dependencies
- Stability
- Invariants

---

## 20. Testing Architecture
- Test Pyramid
- Unit Strategy
- Integration Strategy
- Interface Contract Tests
- State Machine Tests
- Pipeline Tests
- Plugin Tests
- CLI Tests
- Regression Strategy

---

## 21. Trust & Security Architecture
- Trust Boundaries
- Trust Levels
- Permission Model
- Input Validation
- Output Validation
- Plugin Isolation
- Filesystem Access
- Command Execution
- Secret Handling
