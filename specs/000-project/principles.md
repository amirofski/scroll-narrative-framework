# Engineering Principles

Version: 1.0 Draft

Status: Accepted

Related Documents:

* vision.md
* philosophy.md
* glossary.md
* architecture.md

---

# Engineering Principles

This document defines the non-negotiable engineering principles of Scroll Narrative Framework (SNF).

These principles are architectural constraints.

They are not suggestions.

Any implementation, feature, plugin, or contribution must respect these rules.

---

# Principle 01 — Experience First

## Rule

The experience is the primary artifact.

Code is an implementation detail.

## Explanation

SNF does not model animations.

SNF models experiences.

An experience contains:

* narrative structure
* scenes
* interactions
* transitions
* media
* constraints
* relationships

The implementation layer only exists to execute the experience.

## Validation

A feature is architecturally correct if the experience can be described without knowing the runtime technology.

---

# Principle 02 — Compiler Before Runtime

## Rule

Complexity belongs in compilation, not execution.

## Explanation

The compiler should perform:

* validation
* transformation
* optimization
* dependency resolution
* graph generation

The runtime should execute an already prepared execution plan.

## Avoid

Runtime interpretation of author intent.

---

# Principle 03 — Core Has Zero Platform Dependencies

## Rule

The core engine must never depend on external platforms.

Forbidden dependencies:

* React
* Vue
* Browser APIs
* DOM
* GSAP
* Three.js
* Canvas
* WebGPU

## Allowed Dependencies

Only:

* language primitives
* mathematical utilities
* internal abstractions

---

# Principle 04 — Data-Oriented Design

## Rule

Data structures define the system.

Behavior consumes data.

## Explanation

Experience definitions should be:

* serializable
* inspectable
* transformable
* versionable

Data should be the source of truth.

---

# Principle 05 — Immutable Experience Model

## Rule

Compiled experiences must be immutable.

## Reason

Immutable structures provide:

* deterministic execution
* easier debugging
* reliable caching
* reproducible builds

---

# Principle 06 — Signal Driven Architecture

## Rule

Continuous change is represented through signals.

## Examples

Signals:

* scroll position
* time
* audio level
* cursor position
* video progress

Events represent isolated occurrences.

Signals represent evolving state.

---

# Principle 07 — Scroll Is Not Special

## Rule

Scroll is only one possible driver.

The engine must not contain scroll-specific assumptions.

## Future Drivers

Examples:

* TimeDriver
* PointerDriver
* AudioDriver
* VideoDriver
* SensorDriver
* NetworkDriver
* AI Driver

---

# Principle 08 — Graph Over Timeline

## Rule

Experiences are graphs, not timelines.

## Reason

Real experiences contain:

* parallel execution
* dependencies
* branching
* synchronization
* reusable structures

Graphs represent these relationships.

---

# Principle 09 — Composition Over Inheritance

## Rule

Capabilities are composed.

They are not inherited.

## Reason

Composition provides:

* flexibility
* plugin capability
* easier maintenance
* smaller abstractions

---

# Principle 10 — Everything Extensible Through Plugins

## Rule

New capabilities must be implemented as plugins whenever possible.

Plugins may provide:

* node types
* effects
* drivers
* compiler passes
* runtime commands
* developer tools

---

# Principle 11 — Runtime Executes Commands

## Rule

The scheduler does not directly manipulate platforms.

The scheduler produces commands.

Example:

```
SetOpacity(0.5)

SeekVideo(40%)

UpdateTransform(...)
```

Runtime adapters execute commands.

---

# Principle 12 — Separation of Responsibilities

Every layer has one responsibility.

Architecture:

```
DSL
 ↓
Compiler
 ↓
IR
 ↓
Execution Graph
 ↓
VM
 ↓
Scheduler
 ↓
Command Stream
 ↓
Runtime
 ↓
Adapter
```

No layer should bypass another layer.

---

# Principle 13 — Explicit Architecture

## Rule

Important behavior must be explicit.

Avoid:

* hidden state
* implicit magic
* undocumented transformations

Developers should understand why the engine behaves a certain way.

---

# Principle 14 — Deterministic Execution

## Rule

Given identical inputs, the engine must produce identical outputs.

Determinism enables:

* testing
* debugging
* replay
* caching
* synchronization

---

# Principle 15 — AI Readable Repository

## Rule

The repository must be understandable by AI systems.

Requirements:

* architecture documentation
* ADR records
* RFC documents
* task specifications
* clear naming

The repository is a knowledge system.

---

# Principle 16 — Specification Before Implementation

## Rule

Major features require specification before code.

Workflow:

```
Idea

↓

Specification

↓

Review

↓

Implementation

↓

Testing

↓

Merge
```

---

# Principle 17 — Small Core, Large Ecosystem

## Rule

The core engine must remain minimal.

Features belong outside the core whenever possible.

The ecosystem should grow around the engine.

---

# Principle 18 — Portable Experiences

## Rule

An experience definition should not depend on one rendering technology.

The same experience should be executable through:

* DOM
* Canvas
* Three.js
* WebGPU
* future runtimes

---

# Principle 19 — Accessibility Is Architectural

## Rule

Accessibility cannot be added later.

The engine must support:

* reduced motion
* semantic content
* keyboard interaction
* alternative experiences

---

# Principle 20 — Performance Is a Design Constraint

## Rule

Performance must be considered at every architectural layer.

Important considerations:

* compilation cost
* runtime scheduling
* memory usage
* rendering workload
* asset management

---

# Principle 21 — Debuggability Is a Feature

## Rule

Every system must be inspectable.

Required future capabilities:

* graph inspection
* runtime state inspection
* signal visualization
* execution tracing
* performance profiling

---

# Principle 22 — Version Everything

## Rule

The following require versioning:

* DSL schema
* IR format
* plugin APIs
* runtime APIs
* experience files

Backward compatibility is a priority.

---

# Principle 23 — Avoid Premature Features

## Rule

Features must solve real experience requirements.

Do not add:

* abstractions without use cases
* APIs without consumers
* systems without validation

---

# Principle 24 — Real Experience Drives Development

## Rule

The production integration is the ultimate validation.

The first real website built with SNF is not a demo.

It is the engine acceptance test.

---

# Principle 25 — Architecture Must Survive Technology Change

## Rule

Technology replacement must not require rewriting the experience model.

Examples:

Replacing:

* GSAP
* Three.js
* React

should not invalidate authored experiences.

---

# Principle 26 — Prefer Stable Concepts

## Rule

Public concepts must represent long-lived ideas.

Preferred:

* Experience
* Scene
* Node
* Signal
* Graph
* Command
* Runtime

Avoid exposing temporary implementation concepts.

---

# Principle 27 — Measure Before Optimizing

## Rule

Optimization decisions require evidence.

Use:

* profiling
* benchmarks
* real experiences

Avoid theoretical optimization.

---

# Principle 28 — Open Source First

## Rule

Every architectural decision should consider external contributors.

Public APIs require:

* documentation
* examples
* stability
* migration paths

---

# Final Principle

## Build The Engine You Want To Exist

SNF should not replicate existing animation frameworks.

It should create a new abstraction layer for interactive experiences.

The goal is not to make animations easier.

The goal is to make experiences composable.
