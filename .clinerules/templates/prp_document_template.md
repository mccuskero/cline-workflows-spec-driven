# PRP: {Feature Name}

> **Version:** 1.0
> **Created:** {YYYY-MM-DD}
> **Status:** {Draft | Ready | In Progress | Complete}
> **Confidence Score:** {1-10}/10

---

## 1. Discovery Summary

### Initial Task Analysis
**Original Request:**
{The exact user request or story that initiated this PRP}

### User Clarifications
| Question | Answer |
|----------|--------|
| {question asked} | {user response} |

### Missing Requirements Identified
- {requirement discovered during planning}

---

## 2. Goal, Why, What

### Goal
{Clear, concise statement of what needs to be built}

### Why (Business Value)
{Business justification and value proposition}

### What (Scope)
**In Scope:**
- {feature/capability 1}
- {feature/capability 2}

**Out of Scope:**
- {explicitly excluded item}

### Success Criteria
| Criterion | Measurement | Target |
|-----------|-------------|--------|
| {criterion} | {how measured} | {target value} |

---

## 3. All Needed Context

### Research Findings Summary
{Key discoveries from codebase and external research}

### Documentation & Reference Links
| Resource | Section | URL/Path |
|----------|---------|----------|
| {doc name} | {relevant section} | {link} |

### Codebase Structure

**Current State:**
```
{relevant directory structure}
```

**Desired State:**
```
{target directory structure with new files}
```

### Reference Files
| File | Purpose | Key Patterns |
|------|---------|--------------|
| `{path}` | {why it's relevant} | {patterns to follow} |

### Library Quirks & Critical Gotchas
- {gotcha 1}: {explanation and how to handle}
- {gotcha 2}: {explanation and how to handle}

---

## 4. Implementation Blueprint

### Data Models & Types

```typescript
// {Description of types needed}
interface {TypeName} {
  {field}: {type};
}
```

### Ordered Task List

| # | Action | Target | Details |
|---|--------|--------|---------|
| 1 | CREATE | `{path/file}` | {description} |
| 2 | MODIFY | `{path/file}` | {what to change} |
| 3 | INJECT | `{path/file}` | {what to add and where} |

### Pseudocode / Implementation Notes

```
// {Component/Feature Name}
1. {step 1}
2. {step 2}
   - {critical detail}
   - {constraint to respect}
3. {step 3}
```

### Integration Points

| System | Integration Type | Details |
|--------|------------------|---------|
| Database | {query/mutation} | {tables, fields affected} |
| API | {endpoint} | {method, path, payload} |
| Routing | {route} | {path, guards, params} |
| State | {store/context} | {what state changes} |

---

## 5. Validation Loop

### Lint & Type Check Commands
```bash
# Linting
{lint command}

# Type checking
{type check command}
```

### Test Commands
```bash
# Unit tests
{unit test command}

# Integration tests
{integration test command}

# E2E tests (if applicable)
{e2e test command}
```

### Build Command
```bash
{build command}
```

### Final Checklist

- [ ] All new code has tests
- [ ] Linting passes with no errors
- [ ] Type checking passes
- [ ] Build completes successfully
- [ ] Manual testing completed for:
  - [ ] {scenario 1}
  - [ ] {scenario 2}
- [ ] Documentation updated
- [ ] No console errors/warnings

### Anti-Patterns to Avoid

1. {anti-pattern}: {why it's problematic}
2. {anti-pattern}: {why it's problematic}
3. {anti-pattern}: {why it's problematic}

---

## 6. Task Breakdown

> See: `docs/tasks/{feature-name}.md`

### Summary of Tasks
| ID | Task | Priority | Estimate |
|----|------|----------|----------|
| T-001 | {task name} | {Critical/High/Medium/Low} | {XS/S/M/L/XL} |

---

## 7. Risks & Mitigations

| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| {risk} | {High/Medium/Low} | {High/Medium/Low} | {strategy} |

---

## 8. Open Questions

- [ ] {question needing resolution}
- [ ] {question needing resolution}

---

## Appendix: Research Notes

### External Documentation Reviewed
- {source}: {key takeaways}

### Similar Implementations Found
- `{file}`: {what it does, patterns used}

### Decisions Made
| Decision | Rationale | Alternatives Considered |
|----------|-----------|------------------------|
| {decision} | {why} | {other options} |
