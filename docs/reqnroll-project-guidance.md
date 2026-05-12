# Reqnroll Project Guidance

Recommended test location:

```text
tests/{Project}.AcceptanceTests/
  Features/
  Steps/
  TestSupport/
```

Recommended boundary:

```text
Steps call Application Services or test-facing Application facades.
Application calls Domain.
Presentation is not involved.
```

Recommended test support:

* Scenario context
* Test data builders
* In-memory repositories
* domain object mothers
* fake event dispatcher if needed
