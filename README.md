# Spec Kit Reqnroll BDD Extension

A Spec Kit extension for turning acceptance criteria into Reqnroll-oriented BDD plans, Gherkin feature files, traceability reports, implementation handoffs, and verification reports.

This extension is intentionally small. It does not replace `/speckit.implement`. It prepares a clean BDD construction plan so the native Spec Kit implementation command can build the test project, step definitions, and production code.

## Workflow

```text
/speckit.specify
/speckit.plan
/speckit.tasks
/speckit.reqnroll-bdd.plan
/speckit.reqnroll-bdd.generate
/speckit.implement
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

## What this extension does

- Analyze acceptance criteria.
- Produce a BDD test plan.
- Generate Reqnroll-compatible `.feature` files.
- Generate traceability.
- Generate an implementation handoff for `/speckit.implement`.
- Verify BDD artifact quality and architecture boundaries.

## What this extension does not do in v0.1.0

- It does not provide `/speckit.reqnroll-bdd.implement`.
- It does not automatically install NuGet packages.
- It does not generate complete C# step definitions.
- It does not modify production code.
- It does not automate Godot UI tests.
- It does not define hooks.
- It is not submitted to the community catalog yet.


## Optional configuration

The extension ships with an optional configuration template:

```text
config-template.yml
```

When installed, this may be copied as:

```text
.specify/extensions/reqnroll-bdd/reqnroll-bdd-config.yml
```

The MVP does not require configuration. The config file is mainly for project-specific defaults such as:

- target acceptance test project
- fallback `.feature` output path
- Application-layer binding boundary
- whether verification should auto-run `dotnet test`
- forbidden implementation terms for `.feature` files

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

## Installation for local development

From a Spec Kit project:

```bash
specify extension add --dev /path/to/spec-kit-reqnroll-bdd
```

Then restart or reload your coding agent if the commands do not appear immediately.

## Suggested release flow

```bash
git init
git add .
git commit -m "Initial v0.1.0"
git tag v0.1.0
git remote add origin https://github.com/LoogaCY-Studio/spec-kit-reqnroll-bdd.git
git push -u origin main
git push origin v0.1.0
```

## Compatibility

Target Spec Kit version:

```text
>=0.8.0
```

The extension is designed around the native Spec Kit workflow where `/speckit.implement` executes tasks from `tasks.md`.

## License

MIT
