# BDD Implementation Handoff

## Feature

{feature_name}

## Purpose

This handoff guides `/speckit.implement` to implement the generated Reqnroll BDD specifications.

## Required Implementation Tasks

### Test Project

- Create or update the Reqnroll acceptance test project.
- Add the required Reqnroll test framework packages if missing.
- Ensure `.feature` files are included in the test project.

### Step Definitions

| Scenario ID | Feature File | Suggested Step Class | Binding Boundary |
| --- | --- | --- | --- |

### Test Support

Create or update:

- Scenario context
- Test data builders
- In-memory repositories or fakes
- Application-layer test facade if useful

### Architecture Rules

- Step definitions may call Application Services or test-facing Application facades.
- Step definitions must not call Godot Presentation nodes.
- Feature files must remain implementation-agnostic.

### Suggested Task Insertions

| Task ID | Task | Depends On |
| --- | --- | --- |

### Required Verification

```bash
dotnet test
```
