# BDD Implementation Handoff

## Feature

Guard Card Shield Stacking

## Purpose

This handoff guides `/speckit.implement` to implement the generated Reqnroll BDD specifications.

## Required Implementation Tasks

### Test Project

- Create or update the Reqnroll acceptance test project.
- Add the required Reqnroll test framework packages if missing.
- Ensure `.feature` files are included in the test project.

Assumption:

```text
tests/AcceptanceTests/Features/
```

is used because the target project name cannot be inferred from the example alone.

### Step Definitions

| Scenario ID | Feature File | Suggested Step Class | Binding Boundary |
| --- | --- | --- | --- |
| SC-001 | GuardCard.feature | GuardCardSteps | Application |
| SC-002 | GuardCard.feature | GuardCardSteps | Application |

### Test Support

Create or update:

- Scenario context
- Battle test data builder
- Card test data builder
- In-memory battle repository or fake battle state
- Application-layer test facade if useful

### Architecture Rules

- Step definitions may call Application Services or test-facing Application facades.
- Step definitions must not call Godot Presentation nodes.
- Step definitions must not depend on UI labels, buttons, signals, or scene tree structure.
- Feature files must remain implementation-agnostic.

### Suggested Task Insertions

| Task ID | Task | Depends On |
| --- | --- | --- |
| BDD-001 | Create or update the Reqnroll acceptance test project | None |
| BDD-002 | Include GuardCard.feature in the acceptance test project | BDD-001 |
| BDD-003 | Create GuardCardSteps skeletons with Given / When / Then method signatures and `PendingStepException` | BDD-002 |
| BDD-004 | Complete GuardCardSteps through the Application boundary or an Application-layer test facade | BDD-003 |
| BDD-005 | Add scenario context, battle and card test data builders, in-memory battle state, and optional Application-layer test facade | BDD-003 |
| BDD-006 | Run acceptance tests and fix failing implementation | BDD-004, BDD-005 |

### Required Verification

Run this if a .NET test project exists:

```bash
dotnet test
```
