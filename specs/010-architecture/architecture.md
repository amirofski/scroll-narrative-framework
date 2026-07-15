# Architecture

Version: 1.0 Draft

Status: Accepted

Related Documents:

* `/specs/000-project/vision.md`
* `/specs/000-project/philosophy.md`
* `/specs/000-project/principles.md`
* `/specs/000-project/glossary.md`

---

# 1. Overview

Scroll Narrative Framework (SNF) is an **Open Experience Composition Engine**.

SNF is designed to transform declarative experience definitions into optimized executable experiences through a compiler-driven architecture.

Unlike traditional animation frameworks, SNF separates authoring from execution.

Authors describe **what** an experience should be.

The engine determines **how** the experience should execute.

This separation allows the same experience definition to execute on multiple rendering technologies without changing the authored experience.

The architecture is intentionally divided into independent layers that communicate through well-defined contracts.

Each layer has a single responsibility.

Each layer can evolve independently.

---

# 2. Purpose

The purpose of the architecture is to establish a deterministic pipeline from human intent to executable interactive experiences.

Every experience follows the same lifecycle:

```text
Author
    ↓
Experience Definition
    ↓
Compilation
    ↓
Execution Plan
    ↓
Virtual Machine
    ↓
Scheduler
    ↓
Command Stream
    ↓
Runtime
    ↓
Platform Adapter
    ↓
Platform
```

Each transformation increases execution readiness while reducing ambiguity.

---

# 3. Why SNF Exists

Modern frontend development couples interactive experiences directly to implementation technologies.

Typical applications often look like this:

```text
Application

↓

React

↓

Animation Library

↓

Browser APIs

↓

DOM
```

As projects grow, experience logic becomes scattered across:

* Components
* Hooks
* Timelines
* Event listeners
* Browser callbacks
* Animation libraries

The experience itself disappears into implementation details.

This creates several problems:

* Tight coupling
* Difficult maintenance
* Runtime lock-in
* Poor portability
* Limited optimization
* Difficult AI generation
* Difficult testing

SNF exists to separate the experience from its implementation.

---

# 4. Architectural Objectives

The architecture is designed around the following objectives.

## Declarative Authoring

Authors describe intent rather than implementation.

The engine determines execution.

---

## Compiler-Driven Execution

Compilation is responsible for:

* validation
* optimization
* dependency analysis
* execution planning

Runtime execution should remain lightweight.

---

## Runtime Independence

Experiences should not depend on:

* DOM
* React
* Canvas
* Three.js
* WebGPU
* GSAP

Rendering technologies are implementation details.

---

## Deterministic Behavior

Given identical input:

* compilation
* execution
* scheduling

must always produce identical results.

---

## Extensibility

New capabilities should be added through plugins rather than modifications to the core engine.

---

## AI Readability

Every architectural concept should be understandable through documentation.

Architecture should never exist only inside source code.

---

# 5. Architectural Non-Goals

SNF intentionally avoids solving problems outside its domain.

SNF is not:

* a frontend framework
* a React framework
* a CMS
* a visual website builder
* an animation library
* a game engine
* a rendering engine
* a design tool

These systems may integrate with SNF but are not part of the core architecture.

---

# 6. Architectural Principles

The architecture is founded on several core principles.

## Separation of Concerns

Every layer owns one responsibility.

Responsibilities must never overlap.

---

## Stable Contracts

Communication between layers occurs only through defined interfaces.

Layers should not depend on implementation details of neighboring layers.

---

## Dependency Direction

Dependencies always point toward lower-level abstractions.

No layer may depend on a layer above it.

---

## Immutable Compilation

Compilation outputs are immutable.

Execution never modifies compiled structures.

---

## Runtime Isolation

Platform-specific behavior exists only inside adapters and runtimes.

---

## Progressive Transformation

Each layer transforms information into a more executable representation.

The architecture is therefore a transformation pipeline rather than a collection of unrelated systems.

---

# 7. High-Level Architecture

The complete execution pipeline is illustrated below.

```text
                AUTHORING

 Author
    │
    ▼
 Experience DSL
    │
    ▼

            COMPILATION

 Parser
    │
    ▼
 AST
    │
    ▼
 Experience IR
    │
    ▼
 Optimizer
    │
    ▼
 Execution Plan
    │
    ▼

            EXECUTION

 Experience VM
    │
    ▼
 Scheduler
    │
    ▼
 Command Stream
    │
    ▼

             RUNTIME

 Runtime
    │
    ▼
 Platform Adapter
    │
    ▼

            PLATFORM

 Browser
 Canvas
 WebGL
 WebGPU
 Native
```

Each section has a clearly defined responsibility.

No section should bypass another.

---

# 8. Architecture Layers

The system is divided into five major layers.

## 1. Authoring Layer

Purpose:

Describe experiences.

Contains:

* Experience DSL
* Visual Editor (future)
* AI Authoring
* Templates

This layer never executes experiences.

---

## 2. Compilation Layer

Purpose:

Transform authored experiences into executable representations.

Contains:

* Parser
* AST
* Validation
* Experience IR
* Optimization
* Execution Plan Generation

This layer has no runtime responsibilities.

---

## 3. Execution Layer

Purpose:

Evaluate execution plans.

Contains:

* Experience VM
* Scheduler
* State Evaluation
* Command Generation

This layer has no rendering responsibilities.

---

## 4. Runtime Layer

Purpose:

Execute commands.

Contains:

* Runtime
* Asset Management
* Command Dispatch
* Runtime Services

This layer never parses author input.

---

## 5. Platform Layer

Purpose:

Communicate with real rendering technologies.

Examples:

* Browser DOM
* Canvas
* WebGL
* WebGPU
* React
* Vue
* Native Platforms

This layer contains no business logic.

---

# 9. Layer Responsibilities

| Layer     | Responsibility             | Must Never           |
| --------- | -------------------------- | -------------------- |
| Authoring | Describe experiences       | Execute              |
| Compiler  | Transform definitions      | Render               |
| VM        | Evaluate execution plans   | Access platform APIs |
| Scheduler | Produce execution updates  | Parse DSL            |
| Runtime   | Execute commands           | Compile              |
| Adapter   | Communicate with platforms | Own business logic   |
| Platform  | Render output              | Know SNF internals   |

This separation is mandatory.

---

# 10. Architectural Flow

Information flows through the engine in one direction.

```text
Intent

↓

Definition

↓

Compilation

↓

Optimization

↓

Execution Plan

↓

Evaluation

↓

Commands

↓

Rendering
```

Every stage reduces ambiguity.

Every stage increases execution specificity.

By the time information reaches the Runtime, no author intent remains unresolved.

The Runtime executes decisions.

It does not make decisions.
# 11. Dependency Architecture

SNF follows a strict unidirectional dependency model.

Every dependency moves toward lower architectural layers.

No dependency may point upward.

The architecture intentionally prevents circular dependencies.

```text
Authoring
    │
    ▼
Compilation
    │
    ▼
Execution
    │
    ▼
Runtime
    │
    ▼
Platform
```

This rule guarantees that implementation details never leak into higher-level abstractions.

---

## Allowed Dependencies

```text
DSL
    ↓
Compiler
    ↓
Execution
    ↓
Runtime
    ↓
Adapter
```

---

## Forbidden Dependencies

The following relationships are forbidden.

```text
Runtime
    ✕ imports Compiler

Compiler
    ✕ imports Runtime

Core
    ✕ imports Browser APIs

Core
    ✕ imports React

VM
    ✕ imports DOM

DSL
    ✕ imports Runtime

Platform Adapter
    ✕ imports Compiler
```

Violating these rules breaks architectural isolation.

---

# 12. Package Architecture

The repository is organized as independent packages.

Each package represents one architectural responsibility.

```text
packages/

core/
dsl/
compiler/
vm/
scheduler/
runtime/
signals/
plugin-api/

adapters/
    react/

plugins/

examples/
```

Packages communicate only through public interfaces.

Internal implementation details must never be imported directly.

---

## Core

The Core package contains the domain model.

Examples:

* Experience
* Scene
* Node
* Signal
* Command
* Constraint

Core owns no platform knowledge.

---

## DSL

The DSL package defines how authors describe experiences.

Responsibilities:

* syntax
* parsing entry point
* validation entry point

It does not execute anything.

---

## Compiler

The Compiler transforms experience definitions into executable representations.

Responsibilities include:

* parsing
* semantic analysis
* optimization
* plan generation

The Compiler never renders.

---

## VM

The Experience Virtual Machine evaluates execution plans.

Responsibilities:

* execution state
* graph evaluation
* dependency resolution
* command generation

The VM does not know platform details.

---

## Scheduler

The Scheduler coordinates execution.

Responsibilities:

* receive signals
* evaluate execution
* produce command batches

The Scheduler never manipulates the DOM.

---

## Runtime

The Runtime executes commands.

Responsibilities:

* asset loading
* command dispatch
* lifecycle management

The Runtime never parses experiences.

---

## Platform Adapter

Adapters connect Runtime commands to real rendering systems.

Examples:

* React Adapter
* Browser Adapter
* Canvas Adapter
* Three.js Adapter

Adapters contain platform-specific code only.

---

# 13. Execution Lifecycle

Every experience follows the same lifecycle.

```text
Author

↓

Experience Definition

↓

Compile

↓

Validate

↓

Optimize

↓

Generate Execution Plan

↓

Instantiate VM

↓

Receive Signals

↓

Evaluate

↓

Generate Commands

↓

Execute Runtime

↓

Render
```

This lifecycle is deterministic.

The same experience must always produce the same execution plan.

---

# 14. Data Flow

SNF distinguishes between data flow and execution flow.

Data moves forward through transformations.

```text
Experience

↓

AST

↓

IR

↓

Execution Plan

↓

Runtime Commands
```

Each transformation produces a richer and more executable representation.

Data never flows backward.

---

## Immutable Transformations

Each stage produces a new representation.

For example:

```text
DSL

↓

AST

↓

IR

↓

Execution Plan
```

The previous representation remains unchanged.

This enables:

* caching
* debugging
* replay
* testing
* optimization

---

# 15. Control Flow

Control Flow is different from Data Flow.

Data is compiled once.

Execution happens continuously.

Runtime loop:

```text
Signal

↓

Scheduler

↓

VM

↓

Command Stream

↓

Runtime

↓

Platform
```

Signals continuously update execution state.

Compilation never happens inside the runtime loop.

---

# 16. State Management Model

SNF distinguishes between two kinds of state.

## Static State

Created during compilation.

Examples:

* scenes
* node hierarchy
* dependencies
* constraints
* execution plan

Static state never changes while an experience executes.

---

## Runtime State

Created during execution.

Examples:

* current progress
* active scene
* signal values
* playback position
* interaction state

Runtime state evolves continuously.

---

## Principle

Compiled data is immutable.

Runtime state is mutable.

These responsibilities must never be mixed.

---

# 17. Signal Processing Model

Signals are the primary input of the engine.

Every external stimulus becomes a Signal.

Examples:

```text
Scroll

↓

Signal
```

```text
Mouse

↓

Signal
```

```text
Video

↓

Signal
```

```text
Time

↓

Signal
```

The Scheduler treats all signals equally.

Signal origin is irrelevant.

Only signal values matter.

---

## Signal Pipeline

```text
Driver

↓

Signal

↓

Scheduler

↓

VM

↓

Commands

↓

Runtime
```

Drivers observe the outside world.

Schedulers evaluate signal changes.

The Runtime executes the resulting commands.

---

## Signal Characteristics

Every Signal should have the following properties:

* Continuous
* Observable
* Deterministic
* Serializable
* Replayable
* Time-aware

Signals should not contain platform-specific behavior.

---

## Signal Independence

Signals must never know:

* DOM
* React
* Browser APIs
* Rendering Technologies

Signals represent information only.

They do not produce visual output.

---

# Summary

At this point, the architecture establishes three fundamental rules:

1. **Dependencies always flow downward.**
2. **Compilation and execution are completely separated.**
3. **Signals drive execution, while runtimes only execute commands.**

These rules form the foundation of every package, plugin, runtime, and future extension of SNF.
# 18. Execution Plan

## Overview

The Execution Plan is the final output of the compilation pipeline.

It is the contract between the Compiler and the Execution Layer.

The Compiler is responsible for producing a complete Execution Plan.

The Execution Layer is responsible for executing it.

Neither layer should know how the other is implemented.

---

## Purpose

The Execution Plan removes ambiguity from the authored experience.

After compilation, the runtime should never need to answer questions such as:

* What does the author mean?
* Which scene comes next?
* Which dependencies exist?
* Which constraints should be evaluated?

Those decisions belong to the Compiler.

The Execution Layer receives a fully prepared execution model.

---

## Characteristics

An Execution Plan must be:

* Immutable
* Serializable
* Deterministic
* Inspectable
* Optimizable
* Versioned

The Execution Plan is an internal representation.

It is not intended to be authored manually.

---

## Conceptual Structure

The internal representation is implementation-defined.

Conceptually it contains:

```text id="v1e2q3"
Execution Plan

├── Metadata

├── Resources

├── Scene Definitions

├── Execution Units

├── Dependencies

├── Constraints

├── Signal Bindings

├── Command Definitions

└── Runtime Hints
```

Future compiler versions may change the internal representation without affecting authored experiences.

---

# 19. Experience Virtual Machine

## Overview

The Experience Virtual Machine (Experience VM) is responsible for evaluating an Execution Plan.

It is the execution engine of SNF.

The VM does not render.

The VM does not know the DOM.

The VM does not know React.

The VM evaluates execution state and produces abstract commands.

---

## Responsibilities

The VM is responsible for:

* evaluating execution state
* resolving dependencies
* evaluating constraints
* processing signal updates
* generating commands
* maintaining execution context

The VM never performs rendering.

---

## Inputs

The VM receives:

* Execution Plan
* Runtime State
* Signal Values

---

## Outputs

The VM produces:

* Command Stream
* State Updates
* Execution Events

---

## Architectural Rule

The VM must remain platform-independent.

A VM implementation should execute identically regardless of whether the target platform is:

* Browser
* Canvas
* Three.js
* WebGPU
* Native

---

# 20. Scheduler Architecture

## Overview

The Scheduler coordinates execution.

It determines **when** evaluation happens.

It does not determine **how** rendering occurs.

---

## Responsibilities

The Scheduler:

* receives signal updates
* batches changes
* schedules evaluation
* invokes the VM
* forwards generated commands

The Scheduler owns timing.

The VM owns evaluation.

---

## Scheduling Cycle

Conceptually:

```text id="a8b5d1"
Signal Update

↓

Scheduler

↓

VM Evaluation

↓

Command Generation

↓

Runtime
```

---

## Design Goals

The Scheduler should:

* minimize unnecessary work
* avoid duplicate evaluations
* support batching
* remain deterministic
* support future scheduling strategies

---

## Future Scheduling Strategies

Possible implementations include:

* frame-based
* event-driven
* fixed timestep
* adaptive scheduling

These strategies are implementation details.

The architecture does not mandate a specific scheduler algorithm.

---

# 21. Command Stream

## Overview

The Command Stream is the communication contract between the Execution Layer and the Runtime.

Commands describe desired state changes.

Commands never describe implementation details.

---

## Examples

Conceptually:

```text id="n4j6x7"
SetOpacity

UpdateTransform

SeekVideo

PlayAudio

PauseVideo

SetText

ShowNode

HideNode
```

These commands are abstract.

Platform adapters determine how they are executed.

---

## Characteristics

Commands should be:

* deterministic
* serializable
* inspectable
* replayable
* platform-independent

---

## Command Pipeline

```text id="r2m8c9"
VM

↓

Command Stream

↓

Runtime

↓

Platform Adapter

↓

Platform
```

---

## Architectural Constraint

The VM must never manipulate rendering systems directly.

All visual changes pass through Commands.

---

# 22. Runtime Pipeline

## Overview

The Runtime executes Commands.

It transforms abstract execution instructions into platform-specific operations.

The Runtime does not understand authored experiences.

It only understands Commands.

---

## Responsibilities

The Runtime is responsible for:

* command execution
* resource management
* lifecycle management
* runtime services

The Runtime never:

* parses DSL
* optimizes experiences
* evaluates compiler rules

---

## Runtime Lifecycle

```text id="m9p2w5"
Initialize

↓

Load Resources

↓

Receive Commands

↓

Execute

↓

Update Platform

↓

Dispose
```

---

## Runtime Independence

Different runtimes may exist.

Examples:

* DOM Runtime
* Canvas Runtime
* WebGL Runtime
* WebGPU Runtime
* Native Runtime

Each Runtime implements the same architectural contract.

---

# 23. Error Handling Strategy

## Philosophy

Errors should be detected as early as possible.

Compilation is preferred over runtime failure.

---

## Error Categories

### Authoring Errors

Detected while authoring.

Examples:

* invalid syntax
* missing references
* invalid properties

Handled by:

Compiler

---

### Compilation Errors

Detected during compilation.

Examples:

* incompatible nodes
* dependency cycles
* invalid constraints

Handled by:

Compiler

Compilation stops.

---

### Runtime Errors

Detected during execution.

Examples:

* missing assets
* unavailable platform features
* adapter failures

Handled by:

Runtime

The Runtime should fail gracefully whenever possible.

---

## Error Reporting

Errors should include:

* unique identifier
* severity
* human-readable message
* source location (when available)
* recovery suggestion (when possible)

This improves both developer experience and AI-assisted debugging.

---

# 24. Extension Points

## Overview

The architecture is intentionally extensible.

The Core should remain small.

New capabilities should be added through extension points.

---

## Supported Extension Types

Examples include:

* Node Types
* Drivers
* Compiler Passes
* Runtime Backends
* Platform Adapters
* Effects
* Asset Loaders
* Developer Tools

---

## Architectural Rule

Extensions should integrate through public APIs.

They must never modify internal Core behavior.

---

## Benefits

A stable extension model provides:

* long-term compatibility
* ecosystem growth
* independent innovation
* maintainable upgrades

---

# 25. Architectural Contracts

Every layer communicates through explicit contracts.

These contracts define:

* accepted inputs
* produced outputs
* lifecycle expectations
* ownership boundaries

Contracts are versioned.

Breaking changes require a documented migration strategy.

---

# Summary

The Execution Layer transforms a compiled Experience into platform-independent Commands.

The Runtime executes those Commands.

The Platform renders the final result.

At no point does execution depend on authoring technologies or rendering implementations.

This separation allows Experiences to remain portable while enabling multiple runtimes and future rendering backends without changing the authored definition.
# 26. Plugin Architecture

## Overview

The Plugin System enables SNF to grow without increasing the complexity of the Core Engine.

The Core defines architectural contracts.

Plugins provide capabilities.

The Core should remain intentionally small.

Most functionality should exist outside the Core.

---

## Objectives

The Plugin System exists to:

* extend the engine safely
* isolate optional functionality
* encourage ecosystem development
* reduce core maintenance
* enable third-party innovation

---

## Plugin Categories

The architecture recognizes multiple categories of plugins.

Examples include:

* Node Plugins
* Effect Plugins
* Driver Plugins
* Runtime Plugins
* Compiler Pass Plugins
* Asset Plugins
* DevTools Plugins
* Platform Adapter Plugins

Additional categories may be introduced in future versions without modifying the Core architecture.

---

## Plugin Lifecycle

Every plugin follows the same conceptual lifecycle.

```text id="p1g7hd"
Register

↓

Validate

↓

Initialize

↓

Execute

↓

Dispose
```

Plugins should not execute before successful registration.

---

## Plugin Isolation

Plugins must never:

* modify internal engine state directly
* bypass public APIs
* depend on undocumented behavior
* patch Core implementations

The Core owns the architecture.

Plugins extend the architecture.

---

# 27. Platform Adapters

## Overview

Platform Adapters translate Runtime Commands into platform-specific operations.

They are the only architectural layer allowed to communicate directly with rendering technologies.

---

## Examples

Potential adapters include:

* React Adapter
* Browser Adapter
* Canvas Adapter
* SVG Adapter
* Three.js Adapter
* WebGPU Adapter
* Native Adapter

---

## Responsibilities

Platform Adapters are responsible for:

* creating platform objects
* updating platform state
* resource binding
* event translation
* lifecycle synchronization

They should not contain business logic.

---

## Architectural Constraint

Every adapter should implement the same architectural contract.

Changing the adapter must not require changes to:

* the DSL
* the Compiler
* the VM
* the Scheduler

---

# 28. Asset Pipeline

## Overview

Interactive experiences rely on external resources.

Examples include:

* images
* videos
* audio
* fonts
* Lottie files
* 3D models
* shaders

The Asset Pipeline defines how these resources enter the Runtime.

---

## Responsibilities

The Asset Pipeline is responsible for:

* discovery
* validation
* loading
* caching
* disposal

Compilation may analyze assets.

Execution consumes assets.

---

## Design Principles

Assets should be:

* uniquely identifiable
* cacheable
* preloadable
* versionable
* replaceable

Asset loading strategies remain implementation-specific.

---

# 29. Performance Model

## Philosophy

Performance is an architectural requirement.

It is not an optimization phase performed after implementation.

Architectural decisions should reduce unnecessary work before execution begins.

---

## Compiler Responsibilities

The Compiler should reduce runtime work whenever possible.

Examples include:

* dead node elimination
* dependency simplification
* static analysis
* execution planning

---

## Runtime Responsibilities

The Runtime should focus on efficient execution.

The Runtime should avoid:

* expensive interpretation
* repeated dependency resolution
* unnecessary allocations
* redundant rendering operations

---

## Scheduler Responsibilities

The Scheduler should:

* batch updates
* avoid duplicate evaluations
* minimize command generation
* process only affected execution units

---

## Design Objective

The majority of computational complexity should occur during compilation rather than execution.

---

# 30. Security Considerations

## Overview

SNF executes authored experiences.

Execution must not compromise application security.

---

## Architectural Rules

The Core should never execute arbitrary source code.

Experience definitions are data.

They are not executable scripts.

---

## Compiler Validation

The Compiler is responsible for validating authored definitions before execution.

Invalid definitions should never reach the Runtime.

---

## Plugin Trust

Plugins execute inside the application environment.

Applications are responsible for deciding which plugins are trusted.

The Core does not guarantee plugin safety.

---

# 31. Testing Strategy

## Philosophy

Every architectural layer should be testable independently.

Testing should not require a browser unless the Platform Layer is being tested.

---

## Compiler Testing

Compiler tests verify:

* parsing
* validation
* optimization
* Execution Plan generation

---

## VM Testing

VM tests verify:

* state evaluation
* dependency resolution
* command generation

No rendering environment should be required.

---

## Runtime Testing

Runtime tests verify:

* command execution
* lifecycle management
* resource handling

---

## Adapter Testing

Platform Adapter tests verify correct integration with rendering technologies.

---

## Integration Testing

Integration tests validate complete experiences.

A production experience is the highest level of architectural validation.

---

# 32. Observability

## Overview

Complex systems require visibility.

The architecture should support inspection at every stage.

---

## Inspectable Layers

Future tooling should allow inspection of:

* Experience Definition
* AST
* Experience IR
* Execution Plan
* Runtime State
* Signal Values
* Command Stream

---

## Benefits

Observability improves:

* debugging
* performance analysis
* education
* AI-assisted development

Observability is considered an architectural capability rather than an optional tool.

---

# 33. Architectural Decision Process

Major architectural changes follow a defined process.

```text id="d6s9ke"
Problem

↓

Discussion

↓

RFC

↓

Review

↓

ADR

↓

Implementation

↓

Release
```

Architecture should evolve deliberately.

Implementation must follow documented decisions.

---

# 34. Future Evolution

The architecture is designed to evolve without invalidating authored Experiences.

Possible future capabilities include:

* Visual Experience Editor
* AI Experience Generation
* Cloud Compilation
* Remote Runtime Execution
* Collaborative Authoring
* Multi-Platform Synchronization
* Live Experience Editing
* Distributed Rendering

Future evolution should extend existing architectural contracts rather than replace them.

---

# 35. Backward Compatibility

Architectural evolution should prioritize stability.

The following artifacts require explicit versioning:

* Experience DSL
* Experience Schema
* Compiler Interfaces
* Plugin APIs
* Runtime Contracts
* Adapter Contracts

Breaking changes require:

* documentation
* migration guidance
* version transition strategy

Long-term compatibility is a design objective.

---

# Summary

The final architectural layers ensure that SNF remains:

* extensible through plugins
* portable across platforms
* observable during execution
* testable in isolation
* performant by design
* secure by default
* stable over time

The Core defines the architecture.

The ecosystem extends it.

Neither should compromise the other.
# 36. Architecture Invariants

The following architectural rules are invariant.

They define the identity of SNF.

These rules must remain true regardless of implementation language, runtime technology, or future evolution.

---

## Invariant 01

Experiences are authored.

They are never directly programmed against rendering technologies.

---

## Invariant 02

Compilation always happens before execution.

Runtime execution must never interpret author intent.

---

## Invariant 03

The Core remains platform independent.

Platform knowledge belongs exclusively to Platform Adapters.

---

## Invariant 04

The Compiler owns transformation.

The Runtime owns execution.

These responsibilities never overlap.

---

## Invariant 05

Execution is driven by Signals.

Signals represent state.

Commands represent actions.

---

## Invariant 06

Every architectural layer communicates through explicit contracts.

Hidden dependencies are prohibited.

---

## Invariant 07

Experience Definitions are portable.

Changing rendering technology must not require rewriting an Experience.

---

## Invariant 08

The architecture is Specification-first.

The Specification defines the system.

The Reference Implementation implements the Specification.

---

# 37. Reference Architecture

The following diagram summarizes the complete architecture.

```text
                    ┌────────────────────┐
                    │      AUTHOR        │
                    └─────────┬──────────┘
                              │
                              ▼
                    ┌────────────────────┐
                    │   Experience DSL   │
                    └─────────┬──────────┘

                    ───── COMPILATION ─────

                              ▼
                    ┌────────────────────┐
                    │      Parser        │
                    └─────────┬──────────┘
                              ▼
                    ┌────────────────────┐
                    │        AST         │
                    └─────────┬──────────┘
                              ▼
                    ┌────────────────────┐
                    │   Experience IR    │
                    └─────────┬──────────┘
                              ▼
                    ┌────────────────────┐
                    │     Optimizer      │
                    └─────────┬──────────┘
                              ▼
                    ┌────────────────────┐
                    │   Execution Plan   │
                    └─────────┬──────────┘

                     ───── EXECUTION ─────

                              ▼
                    ┌────────────────────┐
                    │   Experience VM    │
                    └─────────┬──────────┘
                              ▼
                    ┌────────────────────┐
                    │     Scheduler      │
                    └─────────┬──────────┘
                              ▼
                    ┌────────────────────┐
                    │   Command Stream   │
                    └─────────┬──────────┘

                      ───── RUNTIME ─────

                              ▼
                    ┌────────────────────┐
                    │      Runtime       │
                    └─────────┬──────────┘
                              ▼
                    ┌────────────────────┐
                    │ Platform Adapter   │
                    └─────────┬──────────┘
                              ▼

                     ───── PLATFORM ─────

          Browser · Canvas · WebGL · WebGPU · Native
```

The architecture intentionally exposes only stable concepts.

Implementation details remain hidden behind architectural contracts.

---

# 38. Relationship to Other Specifications

This document defines the highest level of the system architecture.

The following specifications expand individual architectural areas.

| Specification           | Purpose                                     |
| ----------------------- | ------------------------------------------- |
| `layers.md`             | Defines every architectural layer in detail |
| `execution-model.md`    | Describes execution semantics               |
| `package-boundaries.md` | Defines package ownership and boundaries    |
| `dependency-rules.md`   | Defines dependency constraints              |
| `data-flow.md`          | Defines information flow through the engine |
| `020-model/*`           | Defines the domain model                    |
| `030-language/*`        | Defines the Experience DSL                  |
| `040-compiler/*`        | Defines the compilation pipeline            |
| `050-engine/*`          | Defines execution internals                 |
| `060-runtime/*`         | Defines runtime behavior                    |
| `070-platform/*`        | Defines platform adapters                   |
| `080-plugins/*`         | Defines the extension system                |

This document should be read before any lower-level specification.

---

# 39. Architectural Evolution

The architecture is intentionally designed to support future evolution.

Evolution should occur through:

* new compiler passes
* additional runtimes
* new platform adapters
* new plugin categories
* improved tooling
* language evolution

The architecture should evolve without changing its fundamental principles.

Stable abstractions are preferred over frequent redesign.

---

# 40. Governance

Changes to the architecture require architectural review.

Any proposal affecting:

* public APIs
* architectural layers
* compiler contracts
* runtime contracts
* plugin interfaces
* platform abstractions

should be documented through an RFC before implementation.

Accepted architectural decisions should be recorded as ADRs.

Implementation should never become the source of architectural truth.

The Specification remains the authoritative reference.

---

# 41. Architecture Manifesto

SNF is built on a simple idea.

Interactive experiences deserve the same level of architectural rigor that programming languages, databases, and operating systems have received for decades.

Experiences should not be tightly coupled to frameworks.

They should not depend on rendering technologies.

They should not disappear into imperative animation code.

Instead, experiences should be:

* declarative
* composable
* deterministic
* portable
* inspectable
* optimizable
* testable

The architecture exists to preserve those qualities.

Every design decision should strengthen them.

Every implementation should respect them.

---

# 42. Closing Statement

Scroll Narrative Framework is not defined by its runtime.

It is not defined by its compiler.

It is not defined by a rendering technology.

It is defined by its architecture.

The architecture separates authoring from execution.

The compiler transforms intent into an executable plan.

The execution engine evaluates that plan.

The runtime executes abstract commands.

The platform renders the final experience.

Each layer has one responsibility.

Each responsibility has one owner.

This separation allows experiences to outlive technologies.

As platforms evolve, implementations may change.

As rendering engines improve, runtimes may change.

As authoring tools become more powerful, the DSL may evolve.

The architecture remains the constant foundation that enables this evolution.

SNF is therefore an **Open Experience Composition Engine** whose primary responsibility is to transform human intent into deterministic, portable, and executable interactive experiences.

---

# Normative Requirements

The keywords **MUST**, **MUST NOT**, **SHOULD**, **SHOULD NOT**, and **MAY** in this specification are to be interpreted as described in RFC 2119.

---

# Document Status

This document defines the normative architecture of the Scroll Narrative Framework Reference Specification.

Any implementation claiming architectural compliance with SNF MUST satisfy the constraints described in this document.

Future specifications may extend this architecture but MUST remain compatible with the architectural principles established here unless a new major specification version explicitly states otherwise.
