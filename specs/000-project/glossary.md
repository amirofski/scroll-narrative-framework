# Glossary

Version: 1.0 Draft

Status: Accepted

Related Documents:

* vision.md
* philosophy.md
* principles.md

---

# Overview

This document defines the official terminology used throughout the Scroll Narrative Framework (SNF) architecture.

The purpose of this glossary is to establish a shared language between:

* developers
* contributors
* AI agents
* plugin authors
* documentation writers

Architectural discussions, specifications, pull requests, and implementation decisions should use these definitions consistently.

---

# Experience

## Definition

An Experience is the highest-level representation of an interactive narrative.

It describes what an audience should experience without defining how the experience is rendered.

An Experience may contain:

* scenes
* nodes
* relationships
* signals
* interactions
* transitions
* constraints
* effects

An Experience is the primary artifact in SNF.

---

## Example

Conceptually:

```
Experience
    |
    ├── Scene
    |
    ├── Scene
    |
    └── Interaction
```

---

# Author

## Definition

An Author is any entity that creates an Experience definition.

An Author may be:

* a developer
* a designer
* a visual editor
* an AI system
* another software system

The Author does not directly control runtime execution.

---

# Experience DSL

## Definition

Experience DSL is the declarative language used to describe experiences.

The DSL represents intent.

The DSL should not contain:

* rendering instructions
* browser APIs
* animation library calls
* runtime-specific code

---

# Scene

## Definition

A Scene is a meaningful section of an Experience.

A Scene represents a narrative or visual unit.

Examples:

* hero introduction
* product explanation
* chapter transition
* conclusion

---

## Properties

A Scene may contain:

* Nodes
* Transitions
* Constraints
* Local Signals
* Effects

---

# Node

## Definition

A Node is the smallest composable unit in an Experience graph.

A Node represents something that exists or participates in an experience.

Examples:

* text
* image
* video
* audio
* 3D object
* container
* SVG
* canvas element

---

# Node Type

## Definition

A Node Type defines the behavior and capabilities of a specific kind of node.

Examples:

```
VideoNode

TextNode

ImageNode

ThreeNode

LottieNode
```

Node Types are extensible through plugins.

---

# Effect

## Definition

An Effect describes a transformation applied to a property of a Node.

Effects do not directly manipulate rendering systems.

Examples:

* opacity change
* transformation
* blur
* color change
* video seeking
* frame selection

---

## Example

Concept:

```
Node:
    Hero Video

Effect:
    Change playback position based on progress
```

---

# Signal

## Definition

A Signal represents a continuously changing value that influences an Experience.

Signals are the primary input mechanism of SNF.

Examples:

* scroll progress
* time
* pointer position
* audio level
* video progress

---

## Important Rule

Scroll is a Signal.

It is not a special architectural concept.

---

# Driver

## Definition

A Driver converts an external source into Signals.

Drivers are responsible for observing external systems.

Examples:

```
ScrollDriver

TimeDriver

MouseDriver

AudioDriver

VideoDriver
```

---

# State

## Definition

State represents the current condition of an executing Experience.

State is produced from:

* signals
* internal execution
* interactions

---

# Experience Store

## Definition

Experience Store is the centralized state container for an executing Experience.

Responsibilities:

* storing state
* updating state
* providing state snapshots
* supporting debugging

---

# Event

## Definition

An Event represents a discrete occurrence.

Examples:

* user clicked
* scene completed
* asset loaded

Events are different from Signals.

Signals represent continuous values.

Events represent moments.

---

# Graph

## Definition

A Graph is a structure containing nodes and relationships.

SNF uses graphs because experiences are not always linear.

A graph can represent:

* dependencies
* parallel execution
* branching
* synchronization

---

# Experience Graph

## Definition

Experience Graph is the compiled structural representation of an Experience.

It describes:

* entities
* relationships
* execution dependencies

It is produced by the Compiler.

---

# Execution Graph

## Definition

Execution Graph is the optimized graph used by the runtime engine.

It is generated from the Experience IR.

It contains information required for efficient execution.

---

# AST

## Definition

Abstract Syntax Tree.

AST is the structured representation of the original DSL input.

Pipeline:

```
DSL

↓

AST
```

AST represents author intent.

---

# IR

## Definition

Intermediate Representation.

IR is the compiler internal representation between author input and execution output.

Pipeline:

```
AST

↓

IR

↓

Execution Graph
```

IR enables:

* optimization
* validation
* transformation

---

# Compiler

## Definition

Compiler transforms Experience definitions into executable structures.

Responsibilities:

* parsing
* validation
* optimization
* graph generation

The compiler understands intent.

---

# Compiler Pass

## Definition

A Compiler Pass is a transformation stage inside the compiler pipeline.

Examples:

* validation pass
* optimization pass
* asset pass
* accessibility pass

---

# Optimizer

## Definition

A compiler component responsible for improving execution efficiency without changing experience behavior.

Examples:

* removing unused nodes
* merging operations
* optimizing assets

---

# Experience VM

## Definition

Experience Virtual Machine is the execution abstraction between compiled experiences and runtimes.

The VM interprets execution structures.

Responsibilities:

* managing execution state
* evaluating graph operations
* producing commands

---

# Scheduler

## Definition

Scheduler determines when and how execution updates happen.

Responsibilities:

* processing signals
* evaluating state
* triggering execution updates

The Scheduler does not know rendering details.

---

# Command

## Definition

A Command is an abstract instruction generated by the engine.

Commands describe what should happen.

Examples:

```
SetOpacity

UpdateTransform

SeekVideo

UpdateText
```

---

# Command Stream

## Definition

A sequence of Commands produced during execution.

The Command Stream is consumed by Runtime adapters.

---

# Runtime

## Definition

Runtime executes commands against a specific environment.

Examples:

* DOM Runtime
* Canvas Runtime
* Three.js Runtime

---

# Platform Adapter

## Definition

A Platform Adapter connects SNF Runtime concepts to a specific platform.

Examples:

```
React Adapter

Browser Adapter

Native Adapter
```

---

# Plugin

## Definition

A Plugin extends SNF functionality without modifying the core engine.

Plugins may provide:

* Node Types
* Effects
* Drivers
* Compiler Passes
* Runtime Commands
* Tools

---

# Runtime Backend

## Definition

A Runtime Backend is a specific execution implementation.

Examples:

* DOM
* Canvas
* WebGL
* WebGPU
* Three.js

---

# Constraint

## Definition

A Constraint defines a relationship or rule between parts of an Experience.

Examples:

* positioning
* synchronization
* dependency rules
* lifecycle conditions

---

# Transition

## Definition

A Transition defines how an Experience moves between states or scenes.

Examples:

* scene change
* visual transformation
* narrative progression

---

# Authoring Layer

## Definition

The layer where Experiences are created.

Contains:

* DSL
* visual tools
* AI generators

---

# Compilation Layer

## Definition

The layer responsible for transforming authored Experiences into executable representations.

Contains:

* parser
* AST
* IR
* optimization

---

# Execution Layer

## Definition

The layer responsible for running Experiences.

Contains:

* VM
* Scheduler
* Commands
* Runtime

---

# Rendering Layer

## Definition

The layer responsible for producing visible output.

Contains:

* DOM
* Canvas
* WebGL
* WebGPU
* other rendering technologies

---

# Single Source of Truth

## Definition

The authoritative location where project knowledge exists.

For SNF:

* Specifications define architecture.
* Code implements specifications.
* ADRs explain decisions.

---

# Architecture Decision Record (ADR)

## Definition

A document explaining an important architectural decision.

Every major decision should have an ADR.

---

# Request For Comment (RFC)

## Definition

A proposal document describing a possible feature or architectural change before implementation.

---

# Integration Experience

## Definition

A real-world application built using SNF to validate the engine.

The first Integration Experience is the official production website implementation.

---

# Final Vocabulary Rule

When introducing a new concept into SNF, the concept must:

1. Have a clear definition.
2. Have a documented purpose.
3. Have a defined relationship with existing concepts.
4. Be added to this glossary.

The vocabulary of SNF is part of the architecture.
