# Step Definitions Skeleton Rules

## Purpose

Step definition skeleton guidance helps `/speckit.implement` create the Reqnroll binding surface without over-generating production logic.

## Allowed

Skeletons may include:

- namespace suggestion
- `using Reqnroll;`
- `[Binding]`
- class declaration
- constructor injection
- scenario context dependency
- Application-layer test facade dependency
- Given / When / Then method signatures
- `throw new PendingStepException();`

## Forbidden

Skeletons must not include:

- completed assertions
- domain calculations
- production code internals
- repository implementation
- infrastructure setup beyond test support placeholders
- Godot node access
- label/button/signal/scene tree access
- animation or UI assertions

## Recommended Pattern

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

    [Given("{step pattern}")]
    public void GivenSomePrecondition()
    {
        throw new PendingStepException();
    }
}
```

## Boundary

Skeletons define the binding surface only.

The actual implementation should be completed later through Application Services or test-facing Application facades.
