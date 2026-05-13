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

### Step Definition Skeleton Guidance

Generate skeleton step definition classes only.

Skeletons may include:

- namespace
- `using Reqnroll;`
- `[Binding]`
- constructor injection for scenario context or Application-layer test facade
- method signatures for Given / When / Then steps
- `throw new PendingStepException();`

Skeletons must not include:

- full production logic
- completed assertions
- domain calculations
- repository implementations
- Godot node, label, button, signal, or scene tree access

Example skeleton:

```csharp
using Reqnroll;

namespace {AcceptanceTestNamespace}.Steps;

[Binding]
public sealed class {SuggestedStepClass}
{
    private readonly GameScenarioContext _context;

    public {SuggestedStepClass}(GameScenarioContext context)
    {
        _context = context;
    }

    [Given("{step pattern}")]
    public void GivenSomePrecondition()
    {
        throw new PendingStepException();
    }

    [When("{step pattern}")]
    public void WhenSomeActionOccurs()
    {
        throw new PendingStepException();
    }

    [Then("{step pattern}")]
    public void ThenSomeOutcomeIsObserved()
    {
        throw new PendingStepException();
    }
}
```

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
