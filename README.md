# Spec Kit Reqnroll BDD Extension

A Spec Kit extension that converts acceptance criteria into Reqnroll-oriented BDD plans, Gherkin feature files, implementation handoffs, and verification reports.

## Flow

```text
plan → generate → implement → verify
```

Commands:

```text
/speckit.reqnroll-bdd.plan
/speckit.reqnroll-bdd.generate
/speckit.implement
/speckit.reqnroll-bdd.verify
```

## Purpose

This extension helps teams move from Spec Kit requirements to executable BDD specifications for .NET projects using Reqnroll.

It does not replace `/speckit.implement`.

## Installation for Local Development

```bash
git clone https://github.com/LoogacyStudio/spec-kit-reqnroll-bdd.git
cd your-spec-kit-project
specify extension add --dev ../spec-kit-reqnroll-bdd
specify extension list
```

## Commands

### `/speckit.reqnroll-bdd.plan`

Creates:

```text
specs/{feature}/bdd-test-plan.md
```

### `/speckit.reqnroll-bdd.generate`

Creates:

```text
tests/{Project}.AcceptanceTests/Features/*.feature
specs/{feature}/bdd-traceability.md
specs/{feature}/bdd-implementation-handoff.md
```

### `/speckit.implement`

Native Spec Kit command. Implements the BDD handoff.

### `/speckit.reqnroll-bdd.verify`

Creates:

```text
specs/{feature}/bdd-verification.md
```

## Architecture Boundary

Recommended path:

```text
.feature
  ↓
Step Definitions
  ↓
Application Service / Use Case Facade
  ↓
Domain
```

Avoid:

```text
.feature
  ↓
Godot UI / Node / Signal / SceneTree
```

## Status

v0.1.0.
