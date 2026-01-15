---
mode: agent
description: Execute individual development tasks from task breakdown documents with focused, incremental implementation
---

# Execute Task - Individual Task Implementation

Your objective is to execute individual development tasks from task breakdown documents. This provides focused, incremental implementation for complex features that benefit from step-by-step execution.

**Input:** Path to task file (e.g., `docs/tasks/feature-name.md`) and optionally a specific task ID (e.g., `T-001`)

## Step 1: Load Task Document

1. **Read Task File**
   - Load the task document completely
   - Parse the document structure
   - Identify all tasks and their statuses

2. **Review Referenced Files**
   - Read any PRP or brainstorming documents referenced
   - Understand broader feature context

3. **Identify Target Task**
   - If task ID provided, locate that specific task
   - If no ID provided, identify the next incomplete task
   - Confirm task selection with user if ambiguous

## Step 2: Task Analysis

4. **Extract Specific Requirements**
   - Parse task description and objectives
   - List all functional requirements
   - Note non-functional requirements (performance, security, etc.)

5. **Review Acceptance Criteria**
   - Identify all Given-When-Then scenarios
   - Understand expected behaviors
   - Note edge cases to handle

6. **Study Dependencies**
   - Identify prerequisite tasks
   - Check if dependencies are completed
   - Note downstream tasks that depend on this one

7. **Examine Code Patterns**
   - Read reference files mentioned in task
   - Find similar implementations in codebase
   - Document patterns to follow

## Step 3: Implementation Planning

8. **Create Focused Plan**
   - Break task into specific implementation steps
   - Order steps by dependency
   - Identify files to create or modify

9. **Study All Referenced Files**
   - Read each referenced file thoroughly
   - Understand existing structure and patterns
   - Note integration points

10. **Identify Patterns to Mirror**
    - Document code patterns from existing implementations
    - Note naming conventions
    - Understand error handling approaches

## Step 4: Focused Implementation (Test-Driven Development)

11. **Write Tests First (Red)**
    - Create test file before implementation code
    - Write failing tests based on acceptance criteria
    - Convert Given-When-Then scenarios to test cases
    - Tests should fail initially (no implementation yet)

12. **Read Reference Files Before Coding**
    - Always examine reference implementation first
    - Understand the pattern being used
    - Review how similar features are tested
    - Note any edge cases handled

13. **Implement to Pass Tests (Green)**
    - Write minimal code to make tests pass
    - Stay within task boundaries
    - Don't add unrequested features
    - Don't refactor unrelated code

14. **Refactor and Mirror Patterns**
    - Clean up code while keeping tests green
    - Use same code structure as references
    - Follow established naming conventions
    - Apply consistent error handling
    - **Apply file headers to all new files** (see Code Standards below)
    - **Follow language-specific code style guides**

15. **Test Incrementally**
    - Run tests after each significant change
    - Verify functionality as you go
    - Don't wait until the end to test

## Step 5: Acceptance Criteria Validation

16. **Execute Given-When-Then Scenarios**
    For each acceptance criterion:
    - Set up the Given conditions
    - Perform the When actions
    - Verify the Then outcomes

17. **Verify All Criteria Complete**
    - Check off each acceptance criterion
    - Document any criteria that couldn't be met
    - Note any issues or edge cases discovered

18. **Run Validation Commands**
    - Execute commands specified in task document
    - Run relevant test suites
    - Check for regressions

## Step 6: Quality Gates

19. **Run Code Quality Checks**
    - Execute lint commands
    - Run type checking
    - Check for code style violations

20. **Verify Code Coverage**
    - Run coverage report command
    - Check coverage meets phase requirements:
      - **POC**: Minimum 10% code coverage
      - **Alpha**: Minimum 40% code coverage
      - **Beta**: Minimum 60% code coverage
      - **Production**: Minimum 80% code coverage
    - If coverage is below target for new code:
      - Add tests for uncovered paths
      - Prioritize error handling and edge cases

21. **Fix Any Issues**
    - Address linting errors
    - Fix type checking failures
    - Resolve style violations
    - Add tests if coverage is insufficient

22. **Verify Definition of Done**
    - Check all DoD criteria from task document
    - Ensure code is complete and tested
    - Verify coverage targets are met
    - Verify documentation is updated if required

## Step 7: Task Completion

23. **Mark Task Complete**
    - Update task status in document if applicable
    - Note completion in conversation

24. **Document Implementation Notes**
    - Record any deviations from original plan
    - Note decisions made during implementation
    - Document any discovered issues

25. **Report Results**
    - Summarize what was implemented
    - List files created/modified
    - Report validation results
    - **Report code coverage for new code**
    - Identify any follow-up items

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
| POC | 10% | Minimal - core functionality proof |
| Alpha | 40% | Core functionality, happy paths |
| Beta | 60% | Edge cases, error handling |
| Production | 80% | Full coverage - edge cases, error handling, integration |

### Coverage Priority

When adding tests to meet coverage targets, prioritize:
1. Public API functions and methods
2. Error handling and edge cases
3. Critical business logic
4. Integration points

## Important Guidelines

- **Write tests before implementation** - follow TDD Red-Green-Refactor
- **Stay within task boundaries** - no scope creep
- **Reference existing patterns extensively**
- **Test incrementally** - don't batch testing
- **Follow specified file structures**
- **Verify dependencies before starting**
- **Document everything** for future reference
- **Apply file headers to all new source files**
- **Follow the appropriate code style guide for the language**
- **Verify code coverage meets phase requirements before completing**

## Task Completion Report Format

```markdown
## Task Complete: {Task ID}

### Summary
- Task: {task name}
- Status: {Complete | Partial | Blocked}
- Development Phase: {POC | Alpha | Beta | Production}

### Implementation
- Files Created: {list}
- Files Modified: {list}

### Test Coverage
- Coverage Target: {10% for POC | 40% for Alpha | 60% for Beta | 80% for Production}
- Coverage Achieved: {X%}
- Coverage Status: {Met | Not Met}

### Acceptance Criteria
- [ ] {criterion 1}: {Pass/Fail}
- [ ] {criterion 2}: {Pass/Fail}

### Validation Results
- Lint: {Pass/Fail}
- Type Check: {Pass/Fail}
- Tests: {Pass/Fail}

### Notes
- Deviations: {any deviations from plan}
- Discoveries: {issues or insights found}
- Follow-ups: {items for future attention}
```
