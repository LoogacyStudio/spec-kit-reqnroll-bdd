# Step Definitions Skeleton Guidance

## Purpose

This section provides suggested Reqnroll step definition skeletons for `/speckit.implement`.

The skeletons are intentionally incomplete. They define class shape, binding attributes, constructor dependencies, and pending step methods only.

They must not contain full business logic, production code implementation, domain calculations, repository implementation, or Godot Presentation binding.

## Suggested Step Definition Classes

| Step Class | Feature File | Scenario IDs | Binding Boundary | Notes |
| --- | --- | --- | --- | --- |
| {StepClassName} | {FeatureFile} | {ScenarioIds} | Application | Bind to Application service or test-facing facade |

## Skeleton Example

```csharp
using Reqnroll;

namespace {AcceptanceTestNamespace}.Steps;

[Binding]
public sealed class {StepClassName}
{
    private readonly {ScenarioContextClass} _context;

    public {StepClassName}({ScenarioContextClass} context)
    {
        _context = context;
    }

    [Given("{given_step_pattern}")]
    public void Given{StepMethodName}()
    {
        throw new PendingStepException();
    }

    [When("{when_step_pattern}")]
    public void When{StepMethodName}()
    {
        throw new PendingStepException();
    }

    [Then("{then_step_pattern}")]
    public void Then{StepMethodName}()
    {
        throw new PendingStepException();
    }
}
```

## Skeleton Rules

- Use `[Binding]` classes.
- Group related steps by feature or business capability.
- Inject only test support objects such as scenario context, test data builders, or an Application-layer test facade.
- Step methods may be generated with `throw new PendingStepException();`.
- Do not fill in assertions.
- Do not call production methods directly unless `/speckit.implement` later decides the correct Application boundary.
- Do not bind to Godot nodes, labels, buttons, signals, or scene tree structure.
- Do not implement domain calculations inside step definitions.
