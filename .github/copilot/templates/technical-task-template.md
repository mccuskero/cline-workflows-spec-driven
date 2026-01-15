# Task Breakdown: {Feature Name}

> **Source PRP:** `docs/prps/{feature-name}.md`
> **Created:** {YYYY-MM-DD}
> **Status:** {Not Started | In Progress | Complete}

---

## Overview

**Feature:** {Feature name}
**Total Tasks:** {count}
**Estimated Effort:** {XS/S/M/L/XL}

### Task Summary

| ID | Task | Priority | Status | Dependencies |
|----|------|----------|--------|--------------|
| T-001 | {name} | {priority} | {status} | {deps} |
| T-002 | {name} | {priority} | {status} | T-001 |

---

## Task Details

### T-001: {Task Name}

**Priority:** {Critical | High | Medium | Low}
**Status:** {Not Started | In Progress | Complete | Blocked}
**Estimated Effort:** {XS/S/M/L/XL}

#### Context & Background

**Source PRP Section:** {section reference}
**Feature Overview:** {brief context}

**Purpose:**
> As a {user type},
> I need {capability},
> So that {benefit}.

**Dependencies:**
- {prerequisite task or system}

#### Technical Requirements

**Functional Requirements:**
- WHEN {condition}, THEN {expected behavior}
- WHEN {condition}, THEN {expected behavior}

**Non-Functional Requirements:**
- Performance: {requirement}
- Security: {requirement}
- Accessibility: {requirement}

**Technical Constraints:**
- Stack: {technologies to use}
- Patterns: {patterns to follow}
- Standards: {coding standards}

#### Implementation Details

**Files to Modify/Create:**

| Action | File | Purpose |
|--------|------|---------|
| CREATE | `{path}` | {purpose} |
| MODIFY | `{path}` | {what changes} |

**Key Implementation Steps:**
1. {step with detail}
2. {step with detail}
3. {step with detail}

**Code Patterns to Follow:**

Reference: `{path/to/reference/file}`
```
{pattern example or description}
```

**API Specifications (if applicable):**

| Aspect | Value |
|--------|-------|
| Method | {GET/POST/PUT/DELETE} |
| Path | `{/api/path}` |
| Headers | {required headers} |
| Request Body | {schema} |
| Response | {schema} |

#### Acceptance Criteria

**Scenario 1: {Happy Path}**
```gherkin
Given {precondition}
When {action}
Then {expected result}
```

**Scenario 2: {Edge Case}**
```gherkin
Given {precondition}
When {action}
Then {expected result}
```

**Scenario 3: {Error Case}**
```gherkin
Given {precondition}
When {action}
Then {expected error handling}
```

#### Validation Checklist

**Functional:**
- [ ] {criterion}

**UI/UX:**
- [ ] {criterion}

**Performance:**
- [ ] {criterion}

**Security:**
- [ ] {criterion}

**Error Handling:**
- [ ] {criterion}

**Integration:**
- [ ] {criterion}

#### Quality Gates

**Code Quality Commands:**
```bash
# Lint
{command}

# Type check
{command}

# Test
{command}
```

**Definition of Done:**
- [ ] Code complete and self-reviewed
- [ ] All acceptance criteria verified
- [ ] Tests written and passing
- [ ] No linting errors
- [ ] No type errors
- [ ] Code follows established patterns

#### Resources & References

**Documentation:**
- {link}

**Code References:**
- `{path}`: {description}

**External Resources:**
- {link}: {description}

#### Notes & Comments

**Implementation Notes:**
- {note}

**Gotchas:**
- {gotcha to watch for}

---

### T-002: {Task Name}

{Repeat structure for each task}

---

## Completion Checklist

- [ ] All tasks marked complete
- [ ] All acceptance criteria verified
- [ ] Integration testing complete
- [ ] Documentation updated
- [ ] PRP status updated to Complete
