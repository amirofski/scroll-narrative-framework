# Scroll Narrative Framework (SNF)

## Vision

Version: 1.0 Draft

Status: Accepted

---

# Overview

Scroll Narrative Framework (SNF) is an Open Experience Composition Engine.

SNF is not a scroll animation library.

SNF is not a GSAP wrapper.

SNF is not a collection of visual effects.

SNF is a platform for describing, compiling, and executing interactive experiences.

The primary goal of SNF is to allow authors to define narrative and interactive experiences using a high-level declarative language while delegating execution details to the engine.

Authors describe intent.

The engine determines execution.

---

# Mission

Enable developers, designers, storytellers, and AI systems to build cinematic, narrative-driven, and interactive web experiences without directly manipulating browser APIs, animation libraries, rendering engines, or timeline implementations.

SNF abstracts implementation details behind a compiler-driven architecture.

---

# Problem Statement

Current web experience development relies heavily on low-level implementation details.

Developers often build experiences directly on top of:

* GSAP
* CSS Animations
* CSS Scroll Timelines
* Framer Motion
* Lottie
* Three.js
* Rive
* Browser APIs

This creates several problems:

* Tight coupling between authoring and implementation.
* Difficult migration between runtimes.
* Poor maintainability.
* Lack of portability.
* Limited AI-assisted generation.
* High implementation complexity.

Experiences become code.

Experiences should become data.

---

# Core Idea

An experience should be authored once and executed anywhere.

The author describes:

* scenes
* transitions
* media
* interactions
* effects
* constraints

The engine decides:

* scheduling
* optimization
* runtime execution
* rendering strategy

---

# North Star

A developer should never need to directly manipulate:

* GSAP timelines
* ScrollTrigger instances
* CSS keyframes
* browser animation loops
* requestAnimationFrame orchestration

Instead they define an experience.

SNF compiles and executes that experience.

---

# What SNF Is

SNF is:

* an Experience Composition Engine
* a Compiler Platform
* an Execution Engine
* a Runtime Abstraction Layer
* a Narrative Framework
* a Signal-Driven System
* an Open Source Platform

---

# What SNF Is Not

SNF is not:

* a React animation library
* a GSAP wrapper
* a visual editor
* a CMS
* a page builder
* a website template

Those may be built on top of SNF.

---

# Design Philosophy

SNF is built around the following principles:

## Experience First

Experiences are the primary artifact.

Implementation is secondary.

---

## Compiler Before Runtime

All interpretation, validation, optimization, and transformation should happen before runtime whenever possible.

---

## Data Over Configuration

Experiences should be represented as data structures.

Behavior emerges from data.

---

## Signals Over Events

Signals represent state evolution.

Events represent isolated occurrences.

The engine is fundamentally signal-driven.

---

## Composition Over Inheritance

Capabilities are composed through graph structures and plugins.

---

## Runtime Independence

Core systems must remain independent from:

* React
* DOM
* Browser APIs
* GSAP
* Canvas
* Three.js

---

## Plugin Everything

Every non-essential capability should be implemented as a plugin.

---

## AI Native

The repository should be understandable and operable by AI agents.

All architectural decisions must be machine-readable.

---

# Primary Audience

SNF serves:

## Developers

Building interactive applications.

## Designers

Building narrative experiences.

## Motion Designers

Creating cinematic sequences.

## Creative Agencies

Producing award-winning digital experiences.

## AI Systems

Generating experiences automatically.

---

# Long-Term Vision

SNF evolves toward a complete ecosystem.

Potential future components include:

* Visual Editor
* AI Experience Generator
* Marketplace
* Experience Templates
* Cloud Compiler
* Collaboration Tools
* Asset Pipelines
* Runtime Marketplace

---

# Target Use Cases

Examples include:

* Product storytelling websites
* Editorial experiences
* Interactive reports
* Data narratives
* Brand campaigns
* Landing pages
* Portfolio experiences
* Educational content
* Technical storytelling
* Presentation systems

---

# First Production Validation

The first official validation of SNF is a real-world storytelling website for a content-writing company.

This project is not a demo.

It is the first production integration.

Every architectural decision should be evaluated against this integration.

---

# Success Criteria

SNF succeeds when:

* Experiences can be described declaratively.
* Experiences compile into executable artifacts.
* Multiple runtimes can execute the same experience.
* AI systems can generate experiences.
* Developers no longer work directly with animation engines.
* New runtimes can be added without changing authoring syntax.

---

# Guiding Principle

Authors describe experiences.

The compiler creates execution plans.

The engine executes those plans.

The runtime renders the result.
