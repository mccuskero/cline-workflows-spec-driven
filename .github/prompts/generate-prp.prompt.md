---
mode: agent
description: Generate a comprehensive Product Requirements & Plan (PRP) document through validated research and codebase analysis
---

# Generate PRP - Product Requirements & Plan

Your objective is to generate a comprehensive Product Requirements & Plan (PRP) document that provides complete context for AI-assisted implementation.

**Input:** Feature description, user story, or path to brainstorming document

## Phase 1: Initial Discovery & Task Validation

1. **Preflight Analysis**
   - Scan project structure for similar existing features
   - Analyze the task description for completeness
   - Identify gaps in requirements:
     - User flows and business logic details
     - Data relationships
     - Integration points
     - Edge cases
     - UI/UX constraints

2. **Ask Clarifying Questions**
   - Generate clarification questions in the user's language
   - Ask questions ONE at a time
   - Wait for responses before proceeding
   - Analyze each response to identify remaining gaps
   - **Ask about development phase** to determine coverage targets:
     - Phase 1/POC (20% coverage target)
     - Beta (80% coverage target)

3. **Decision Gate**
   - Only proceed to Phase 2 when gaps are adequately addressed
   - If critical information is missing, continue asking questions

## Phase 2: Comprehensive Research

4. **Codebase Analysis**
   - Find similar features and patterns
   - Identify reference files and implementations
   - Note coding conventions and standards
   - Understand existing architecture
   - Document findings thoroughly

5. **Smart External Research Decision**

   **SKIP external research if:**
   - Similar components exist in codebase
   - Implementation patterns are already established
   - Standard library/framework features suffice

   **PROCEED with external research if:**
   - Integrating new external libraries
   - Implementing complex undocumented features
   - No codebase examples exist
   - Security considerations require verification

6. **Conditional External Research** (if needed)
   - Ask user if web research is acceptable
   - Focus narrowly on identified knowledge gaps
   - Research external package documentation
   - Look for complex patterns and best practices
   - Consider security implications for new integrations

## Phase 3: PRP Document Generation

7. **Write PRP Document**
   - Save to `docs/prps/{feature-name}.md` (use kebab-case)
   - Include ALL sections from the template below

## Phase 4: Task Breakdown Generation

8. **Generate Task Breakdown**
   - Decompose requirements into manageable development tasks
   - Apply work breakdown structure principles
   - Define clear dependencies between tasks
   - Create Given-When-Then acceptance criteria for each task
   - Save to `docs/tasks/{feature-name}.md`
   - Link task breakdown back into the PRP document

## Phase 5: Quality Assurance

9. **Validate PRP Completeness**
   - Check for necessary context coverage
   - Verify executable validation commands exist
   - Confirm existing pattern references are included
   - Ensure clear implementation paths are defined
   - Validate error handling is documented

10. **Assign Confidence Score**
    - Rate 1-10 for likelihood of one-pass implementation success
    - Document reasoning for the score
    - Identify any remaining risks or uncertainties

## PRP Document Template

```markdown
# PRP: {Feature Name}

> **Version:** 1.0
> **Created:** {YYYY-MM-DD}
> **Status:** Draft
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
{relevant directory structure}

**Desired State:**
{target directory structure with new files}

### Reference Files
| File | Purpose | Key Patterns |
|------|---------|--------------|
| {path} | {why it's relevant} | {patterns to follow} |

### Library Quirks & Critical Gotchas
- {gotcha}: {explanation and how to handle}

---

## 4. Implementation Blueprint

### Data Models & Types
{TypeScript/language-specific type definitions}

### Ordered Task List
| # | Action | Target | Details |
|---|--------|--------|---------|
| 1 | CREATE | {path/file} | {description} |
| 2 | MODIFY | {path/file} | {what to change} |

### Pseudocode / Implementation Notes
{Step-by-step implementation details}

### Integration Points
| System | Integration Type | Details |
|--------|------------------|---------|
| Database | {query/mutation} | {tables, fields affected} |
| API | {endpoint} | {method, path, payload} |

### Code Standards

**File Header Template:** `.github/copilot/templates/header-{language}.{ext}`
**Code Style Guide:** `.github/copilot/code-styles/code-style-{language}.md`

All new source files must include the appropriate file header and follow the language-specific code style guide.

---

## 5. Testing Strategy (TDD)

### Development Phase
- **Phase**: {Phase 1/POC | Beta}
- **Coverage Target**: {20% for POC | 80% for Beta}

### TDD Approach
Follow the Red-Green-Refactor cycle:
1. Write failing tests first (Red)
2. Implement to pass tests (Green)
3. Refactor while keeping tests green

### Test Structure
- Test file naming convention: {convention}
- Test framework: {framework}
- Test location: {directory}

### Coverage Focus Areas
- {Critical path 1}
- {Critical path 2}
- {Error handling scenarios}

---

## 6. Validation Loop

### Lint & Type Check Commands
{lint and type check commands}

### Test Commands
{unit, integration, e2e test commands}

### Coverage Command
{coverage command with reporting}

### Build Command
{build command}

### Final Checklist
- [ ] All new code has tests written FIRST (TDD)
- [ ] Code coverage meets target ({20% POC | 80% Beta})
- [ ] Linting passes with no errors
- [ ] Type checking passes
- [ ] Build completes successfully
- [ ] Manual testing completed
- [ ] Documentation updated

### Anti-Patterns to Avoid
1. {anti-pattern}: {why it's problematic}

---

## 7. Task Breakdown

> See: docs/tasks/{feature-name}.md

### Summary of Tasks
| ID | Task | Priority | Estimate |
|----|------|----------|----------|
| T-001 | {task name} | {priority} | {effort} |

---

## 8. Risks & Mitigations

| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| {risk} | {level} | {level} | {strategy} |

---

## 9. Open Questions

- [ ] {question needing resolution}

---

## Appendix: Research Notes

### External Documentation Reviewed
- {source}: {key takeaways}

### Similar Implementations Found
- {file}: {what it does, patterns used}
```

## Code Standards Reference

When generating PRPs, always include references to the appropriate code standards:

### File Header Templates

| Language | Header Template |
|----------|-----------------|
| JavaScript | `.github/copilot/templates/header-javascript.js` |
| TypeScript | `.github/copilot/templates/header-typescript.ts` |
| C# | `.github/copilot/templates/header-csharp.cs` |
| Java | `.github/copilot/templates/header-java.java` |

### Code Style Guides

| Language | Style Guide |
|----------|-------------|
| JavaScript | `.github/copilot/code-styles/code-style-javascript.md` |
| TypeScript | `.github/copilot/code-styles/code-style-typescript.md` |
| C# | `.github/copilot/code-styles/code-style-csharp.md` |
| Java | `.github/copilot/code-styles/code-style-java.md` |

## Test-Driven Development Requirements

### Code Coverage Targets

| Development Phase | Minimum Coverage | Focus Areas |
|-------------------|------------------|-------------|
| Phase 1 / POC | 20% | Core functionality, happy paths |
| Beta Phase | 80% | Edge cases, error handling, integration |

Always ask about development phase to determine appropriate coverage target.
Include coverage commands and targets in every PRP.

## Important Guidelines

- Ask clarification questions in the user's language
- Write final PRP document in English
- Include ALL relevant documentation references
- Provide executable test/lint commands with coverage reporting
- Use existing codebase keywords and patterns
- Never assume - ask when uncertain
- **Always specify the appropriate header template and code style guide in the PRP**
- **Always include Testing Strategy section with TDD approach and coverage targets**
- **Ask about development phase to set appropriate coverage targets**
