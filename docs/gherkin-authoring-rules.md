# Gherkin Authoring Rules

## Good Scenario

```gherkin
@AC-001
Scenario: Playing two Guard cards stacks shield
  Given the player has 0 shield
  And the player has 2 Guard cards in hand
  When the player plays both Guard cards
  Then the player should have 10 shield
```

## Bad Scenario

```gherkin
Scenario: BattleAggregate applies GuardCardEffect
  Given BattleAggregate has PlayerStats.Shield = 0
  When BattleAppService.Handle PlayCardCommand
  Then PlayerStats.Shield.Value should be 10
```

## Rules

* Use user/player language.
* Use domain language only when it is part of the product vocabulary.
* Avoid class names and method names.
* Prefer one main `When`.
* Keep each scenario focused.
* Tag every scenario with its source acceptance criterion.
