# Spec Kit Reqnroll BDD Extension

A Spec Kit extension for turning acceptance criteria into Reqnroll-oriented BDD plans, Gherkin feature files, traceability reports, implementation handoffs, and verification reports.

This extension is intentionally small. It does not replace `/speckit.implement`. It prepares a clean BDD construction plan so the native Spec Kit implementation command can build the test project, step definitions, and production code.

Spec Kit Reqnroll BDD v1.0.0 is a community-ready extension for turning acceptance criteria into Reqnroll BDD plans, Gherkin files, traceability, safe task injection, implementation handoffs, and verification reports without replacing `/speckit.implement`.

## Workflow

```text
/speckit.specify
/speckit.plan
/speckit.tasks
/speckit.reqnroll-bdd.plan
/speckit.reqnroll-bdd.generate
/speckit.implement
  ↳ before_implement hook: /speckit.reqnroll-bdd.inject-tasks
/speckit.reqnroll-bdd.verify
```

The practical BDD loop is:

```text
plan → generate → implement → verify
```

## Commands

### `/speckit.reqnroll-bdd.plan`

Reads the active feature specification artifacts and creates:

```text
specs/{feature}/bdd-test-plan.md
```

This command classifies acceptance criteria into:

- BDD
- Domain Unit Test
- Application Test
- Integration Test
- Manual / Smoke Test
- Not Testable Yet

It must not generate `.feature` files or C# code.

### `/speckit.reqnroll-bdd.generate`

Reads `bdd-test-plan.md` and creates:

```text
tests/{Project}.AcceptanceTests/Features/*.feature
specs/{feature}/bdd-traceability.md
specs/{feature}/bdd-implementation-handoff.md
```

If the target acceptance test project cannot be inferred, it uses:

```text
tests/AcceptanceTests/Features/
```

The generated handoff is written for `/speckit.implement`.

### `/speckit.reqnroll-bdd.verify`

Checks:

- acceptance criteria coverage
- scenario traceability
- Gherkin quality
- architecture boundary leakage
- optional `dotnet test` execution when a Reqnroll test project is present

It creates:

```text
specs/{feature}/bdd-verification.md
```

## Hook-driven Task Injection

v0.2.0 adds optional task injection through the `before_implement` hook.

Before `/speckit.implement` runs, the extension may trigger:

```text
/speckit.reqnroll-bdd.inject-tasks
```

The command injects a bounded BDD task block into:

```text
specs/{feature}/tasks.md
```

The block is idempotent and only modifies `tasks.md` when these files exist:

- `specs/{feature}/bdd-implementation-handoff.md`
- `specs/{feature}/bdd-traceability.md`
- `specs/{feature}/tasks.md`

If `tasks.md` is missing but handoff and traceability exist, the command does not create `tasks.md`; it writes the proposed BDD task block to `bdd-implementation-handoff.md` instead.

## Step Definition Skeleton Guidance

The generated implementation handoff may include suggested Reqnroll step definition skeletons.

These skeletons are intentionally incomplete. They may include `[Binding]` classes, constructor dependencies, Given/When/Then method signatures, and `PendingStepException`, but they must not include full business logic or production implementation.

Full step implementation remains the responsibility of `/speckit.implement`.

## What this extension does

- Analyze acceptance criteria.
- Produce a BDD test plan.
- Generate Reqnroll-compatible `.feature` files.
- Generate traceability.
- Generate an implementation handoff for `/speckit.implement`.
- Verify BDD artifact quality and architecture boundaries.

## What this extension does not do

- It does not provide `/speckit.reqnroll-bdd.implement`.
- It does not automatically install NuGet packages.
- It does not generate complete C# step definitions.
- It does not modify production code.
- It does not automate Godot UI tests.
- Community catalog submission is prepared separately through the official Spec Kit extension submission process.

## Installation from GitHub Release

Install from the GitHub release archive for tag `v1.0.0`:

```bash
specify extension add reqnroll-bdd --from https://github.com/LoogacyStudio/spec-kit-reqnroll-bdd/archive/refs/tags/v1.0.0.zip
```

## Installation for Local Development

From a Spec Kit project:

```bash
specify extension add --dev /path/to/spec-kit-reqnroll-bdd
```

Then restart or reload your coding agent if the commands do not appear immediately.

## Configuration

The extension ships with an optional configuration template:

```text
config-template.yml
```

The extension installs an optional config file at:

```text
.specify/extensions/reqnroll-bdd/reqnroll-bdd-config.yml
```

Key options:

- `target_test_project`
- `default_feature_output_path`
- `test_boundary`
- `dotnet_test_execution`
- `task_injection.enabled`
- `task_injection.fallback_to_handoff`
- `task_injection.replace_existing_block`

## Architecture boundary

Recommended binding path:

```text
.feature
  ↓
Step Definitions
  ↓
Application Service / Use Case Facade
  ↓
Domain
```

Forbidden binding path:

```text
.feature
  ↓
Step Definitions
  ↓
Godot Button / Label / Node / Signal / SceneTree
```

BDD scenarios should describe observable behavior, not implementation structure.

## Troubleshooting

### The hook runs but no tasks are injected

Run `/speckit.reqnroll-bdd.generate` first. Task injection only modifies `tasks.md` when these files exist:

- `bdd-implementation-handoff.md`
- `bdd-traceability.md`
- `tasks.md`

### Tests are skipped in verify

`/speckit.reqnroll-bdd.verify` only runs `dotnet test` when a .NET test project appears configured.

### Feature files mention implementation details

Run `/speckit.reqnroll-bdd.verify` and remove architecture leakage such as `Aggregate`, `Repository`, `Godot`, `Node`, `Button`, or `SceneTree`.

## Compatibility

Target Spec Kit version:

```text
>=0.8.0
```

The extension is designed around the native Spec Kit workflow where `/speckit.implement` executes tasks from `tasks.md`.

## License

MIT
