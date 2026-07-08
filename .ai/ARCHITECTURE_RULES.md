# Architecture Rules

These rules are mandatory for every human and AI contributor.

## Core Rules
1. Core packages must not depend on browser APIs.
2. Narrative concepts come before implementation details.
3. Progress is the universal driver abstraction.
4. Renderers are adapters, never the source of truth.
5. All public APIs require architectural review.
6. Package boundaries are strict.
7. Favor composition over inheritance.
8. Prefer immutable data models.
9. Every feature starts with a specification.
10. Narrative > Runtime > Renderer.

## Forbidden
- Business logic inside adapters.
- Direct dependencies on GSAP, React or browser APIs from core.
- Runtime-specific concepts in the domain model.
- Breaking package boundaries.
