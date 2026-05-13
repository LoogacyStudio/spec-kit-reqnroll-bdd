# Changelog

## [0.2.0] - 2026-05-13

### Added

- Added `/speckit.reqnroll-bdd.inject-tasks`.
- Added optional `before_implement` hook for BDD task injection.
- Added `artifact-templates/bdd-task-block-template.md`.
- Added `docs/task-injection-rules.md`.
- Added task injection configuration defaults to `config-template.yml`.

### Changed

- Extended the recommended workflow so BDD tasks can be injected before `/speckit.implement`.

### Safety

- Task injection skips without changing files when BDD generate artifacts are missing.
- Task injection uses bounded marker comments for idempotent updates.

## [0.1.0] - 2026-05-13

### Added

- Added optional `config-template.yml` and manifest `provides.config` entry following the official extension template.
- Initial Reqnroll BDD extension manifest.
- Added `/speckit.reqnroll-bdd.plan`.
- Added `/speckit.reqnroll-bdd.generate`.
- Added `/speckit.reqnroll-bdd.verify`.
- Added artifact templates for BDD planning, traceability, handoff, and verification.
- Added architecture, Gherkin, implementation handoff, and Reqnroll project guidance docs.
- Added Guard Card example artifacts.
