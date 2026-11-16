# Architecture Template

Use this structure for `ARCHITECTURE.md` or an architecture proposal.

```markdown
# Architecture

## Context

- Required platforms:
- Distribution:
- Offline/cloud needs:
- Performance constraints:
- Existing stack:

## Decision

- Chosen platform and stack:
- Why it is the lowest total-cost fit:
- Rejected alternatives and reasons:

## Module Boundaries

- Domain model:
- Geometry/business rules:
- Application state:
- Rendering/views:
- Persistence:
- Integrations:

## Canonical Data Model

| Entity | Owner | Persisted fields | Derived fields |
| --- | --- | --- | --- |
| Example | Domain | id, dimensions | area |

## Invariants

- Canonical unit and coordinate system
- Stable ID rules
- Validation rules
- Undo/redo transaction boundaries
- Schema version and migration behavior

## Data Flow

Describe how every view reads and writes the same model.

## Persistence And Sharing

- Local storage:
- Large asset storage:
- Autosave:
- Import/export:
- Share format:

## Test Strategy

- Unit:
- Integration:
- End-to-end:
- Visual/responsive:

## Risks

| Risk | Impact | Mitigation |
| --- | --- | --- |
```

Choose architecture that reduces future coupling instead of predicting every future feature.
