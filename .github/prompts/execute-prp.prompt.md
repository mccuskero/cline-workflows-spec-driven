---
mode: agent
description: Implement features from PRP (Product Requirements & Plan) specifications with comprehensive validation and testing
---

# Execute PRP - Implement from PRP Specification

Your objective is to implement features from PRP (Product Requirements & Plan) specifications with comprehensive validation and testing. Execute the complete implementation in a single pass using the detailed blueprint.

**Input:** Path to PRP file (e.g., `docs/prps/feature-name.md`)

## Phase 1: Load PRP

1. **Read PRP Document**
   - Load the designated PRP file completely
   - Parse and understand all sections:
     - Discovery Summary
     - Goal, Why, What
     - All Needed Context
     - Implementation Blueprint
     - Validation Loop

2. **Understand Requirements**
   - Review all context and requirements
   - Note any critical gotchas or constraints
   - Identify integration points

3. **Extend Research if Needed**
   - If PRP references external documentation, review it
   - Explore any mentioned reference files
   - Conduct additional codebase exploration as necessary

## Phase 2: Plan Implementation

4. **Create Implementation Plan**
   - Decompose complex tasks into manageable steps
   - Create a mental checklist of all tasks
   - Identify dependencies between tasks

5. **Study Reference Files**
   - Read ALL reference files specified in PRP
   - Understand structure, patterns, and organization
   - Note naming conventions and code style

6. **Pattern Mirroring Preparation**
   - Document patterns to follow from reference implementations:
     - File organization
     - Naming conventions
     - Component structure
     - Code patterns
     - Error handling approaches

## Phase 3: Execute the Plan (Test-Driven Development)

7. **Implement Each Component Using TDD**
   For each implementation task, follow the Red-Green-Refactor cycle:

   a. **Write Tests First (Red)**
      - Create test file before implementation
      - Write failing tests that define expected behavior
      - Cover happy path, edge cases, and error scenarios
      - Tests should fail initially (no implementation yet)

   b. **Read Reference First**
      - Always read corresponding reference files before coding
      - Examine reference implementations and their tests thoroughly

   c. **Implement to Pass Tests (Green)**
      - Write minimal code to make tests pass
      - Create new files as needed
      - Modify existing files carefully
      - Follow PRP specifications exactly
      - Apply established patterns from reference files

   d. **Refactor**
      - Clean up code while keeping tests green
      - Mirror reference patterns for your feature
      - Maintain consistency with existing codebase
      - **Apply file headers to all new files** (see Code Standards below)
      - **Follow language-specific code style guides**

8. **Handle Integration Points**
   - Database: Follow existing schema patterns
   - API: Match existing endpoint conventions
   - Routing: Use established routing patterns
   - State Management: Mirror existing state patterns

## Phase 4: Validate

9. **Run Validation Commands**
   - Execute each validation command from the PRP:
     - Lint checks
     - Type checking
     - Unit tests
     - Integration tests
     - Build commands

10. **Verify Code Coverage**
    - Run coverage report command
    - Check coverage meets phase requirements:
      - **Phase 1 / POC**: Minimum 20% code coverage
      - **Beta Phase**: Minimum 80% code coverage
    - If coverage is below target:
      - Identify uncovered code paths
      - Add tests for critical uncovered areas
      - Prioritize error handling and edge cases

11. **Fix Failures**
    - If any validation fails:
      - Analyze error messages
      - Use error patterns from PRP to guide fixes
      - Apply corrections
      - Re-run validation

12. **Iterate Until Pass**
    - Continue fix-validate cycle until all checks pass
    - Ensure coverage targets are met
    - Document any issues encountered and solutions applied

## Phase 5: Complete

13. **Final Checklist Verification**
    - Review each item in the PRP's final checklist
    - Ensure all acceptance criteria are met
    - Verify all integration points work correctly

14. **Execute Final Validation Suite**
    - Run complete test suite
    - Verify build succeeds
    - Confirm code coverage meets phase target
    - Check for any warnings or issues

15. **Re-read PRP for Completeness**
    - Reference PRP document again
    - Confirm every requirement has been addressed
    - Check nothing was missed

16. **Report Completion Status**
    - Summarize what was implemented
    - Note any deviations from PRP (with reasoning)
    - List any follow-up items identified
    - Report final validation results
    - **Report code coverage percentage achieved**

## Code Standards

### File Header Templates

All new source files MUST include the appropriate header template. Select based on language:

| Language | Header Template |
|----------|-----------------|
| JavaScript | `.github/copilot/templates/header-javascript.js` |
| TypeScript | `.github/copilot/templates/header-typescript.ts` |
| C# | `.github/copilot/templates/header-csharp.cs` |
| Java | `.github/copilot/templates/header-java.java` |

Header fields to populate:
- `@file` - Filename
- `@description` - Brief purpose description
- `@author` - Developer name
- `@date` - Creation date (YYYY-MM-DD)
- `@ai-generated` - Set to `true`
- `@ai-client` - Set to `GitHub Copilot`
- `@ai-model` - Model used
- `@copyright` - Organization copyright

### Code Style Guides

Follow language-specific coding standards from `.github/copilot/code-styles/`:

| Language | Style Guide |
|----------|-------------|
| JavaScript | `code-style-javascript.md` |
| TypeScript | `code-style-typescript.md` |
| C# | `code-style-csharp.md` |
| Java | `code-style-java.md` |

Style guides cover:
- Naming conventions
- Formatting rules
- Best practices
- Documentation standards
- Testing conventions

## Test-Driven Development

### TDD Principles

Follow the Red-Green-Refactor cycle for all implementation:
1. **Red**: Write a failing test first
2. **Green**: Write minimal code to pass the test
3. **Refactor**: Clean up while keeping tests green

### Code Coverage Targets

| Development Phase | Minimum Coverage | Focus Areas |
|-------------------|------------------|-------------|
| Phase 1 / POC | 20% | Core functionality, happy paths |
| Beta Phase | 80% | Edge cases, error handling, integration |

### Coverage Priority

When adding tests to meet coverage targets, prioritize:
1. Public API functions and methods
2. Error handling and edge cases
3. Critical business logic
4. Integration points

## Important Guidelines

- **Write tests before implementation** - follow TDD Red-Green-Refactor
- **Never skip reading reference files before implementing**
- **Mirror existing patterns exactly** - consistency matters
- **Run validations frequently**, not just at the end
- If validation fails, **fix and retry** - don't proceed with broken code
- **Follow PRP specifications precisely**
- **Document any necessary deviations** with clear reasoning
- **Apply file headers to all new source files**
- **Follow the appropriate code style guide for the language**
- **Verify code coverage meets phase requirements before completing**

## Completion Report Format

When implementation is complete, provide a summary:

```markdown
## Implementation Complete

### Summary
- Feature: {feature name}
- PRP: {path to PRP}
- Status: {Complete | Partial}
- Development Phase: {POC | Beta}

### Files Created
- {path}: {description}

### Files Modified
- {path}: {what changed}

### Test Coverage
- Coverage Target: {20% for POC | 80% for Beta}
- Coverage Achieved: {X%}
- Coverage Status: {Met | Not Met}

### Validation Results
- Lint: {Pass/Fail}
- Type Check: {Pass/Fail}
- Tests: {Pass/Fail}
- Build: {Pass/Fail}

### Deviations from PRP
- {deviation}: {reasoning}

### Follow-up Items
- {item needing attention}
```
