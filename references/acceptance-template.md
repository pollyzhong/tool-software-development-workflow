# Acceptance Template

Turn each request into observable behavior before implementation.

## Feature Criteria

```markdown
## Feature: Name

Given [starting state]
When [user action]
Then [observable result]

- Data persists after reload:
- Undo/redo behavior:
- Invalid input behavior:
- Empty/read-only/failure behavior:
- Desktop behavior:
- Tablet behavior:
- Mobile behavior:
- 2D/3D or multi-view consistency:
- Out of scope:
```

## Batch Verification

```markdown
## Verification

- [ ] Syntax/type/lint checks
- [ ] Focused unit tests
- [ ] Affected end-to-end workflow
- [ ] Reload and persistence
- [ ] Undo and redo
- [ ] Import/export or sharing when affected
- [ ] Desktop screenshot
- [ ] Tablet screenshot
- [ ] Mobile screenshot
- [ ] Console/network errors
- [ ] Deployment-only checks documented separately
```

Avoid criteria such as “more intelligent”, “better”, or “works correctly” without a measurable result.
