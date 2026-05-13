# Architecture Boundaries

## Core Principle

Reqnroll BDD scenarios describe observable behavior, not implementation structure.

## Recommended Binding Path

```text
.feature
  ↓
Step Definitions
  ↓
Application Service / Use Case Facade
  ↓
Domain
```

## Forbidden Binding Path

```text
.feature
  ↓
Step Definitions
  ↓
Godot Button / Label / Node / Signal / SceneTree
```

## Layer Rules

### Domain

Use unit tests for:

- Value Object invariants
- Aggregate invariants
- rule calculations
- pure domain behavior

### Application

Use Reqnroll BDD for:

- use cases
- player-visible behavior
- business/game rule examples
- accepted/rejected actions
- workflow-level state changes

### Presentation

Do not bind BDD directly to:

- Godot nodes
- labels
- buttons
- animation players
- scene tree
- signals

Use manual QA or smoke tests for UI and animation behavior.
