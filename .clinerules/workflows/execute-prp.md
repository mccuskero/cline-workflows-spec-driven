# Execute PRP - Implement from PRP Specification

<task name="execute-prp">
<task_objective>
Implement features from PRP (Product Requirements & Plan) specifications with comprehensive validation and testing. Execute the complete implementation in a single pass using the detailed blueprint.
</task_objective>

<input>
Path to PRP file (e.g., `docs/prps/feature-name.md`)
</input>

<detailed_sequence_of_steps>

## Phase 1: Load PRP

1. **Read PRP Document**
   - Use `read_file` to load the designated PRP file completely
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
   - Use `search_files` to explore any mentioned reference files
   - Conduct additional codebase exploration as necessary

## Phase 2: Plan Implementation

4. **Create Implementation Plan**
   - Decompose complex tasks into manageable steps
   - Create a mental checklist of all tasks
   - Identify dependencies between tasks

5. **Study Reference Files**
   - Use `read_file` on ALL reference files specified in PRP
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
      - Use `write_to_file` for new files
      - Use `apply_diff` for modifications
      - Follow PRP specifications exactly
      - Apply established patterns from reference files

   d. **Refactor**
      - Clean up code while keeping tests green
      - Mirror reference patterns for your feature
      - Maintain consistency with existing codebase

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
      - **POC**: Minimum 10% code coverage
      - **Alpha**: Minimum 40% code coverage
      - **Beta**: Minimum 60% code coverage
      - **Production**: Minimum 80% code coverage
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

</detailed_sequence_of_steps>

<test_driven_development>
## TDD Principles

Follow the Red-Green-Refactor cycle for all implementation:
1. **Red**: Write a failing test first
2. **Green**: Write minimal code to pass the test
3. **Refactor**: Clean up while keeping tests green

## Code Coverage Targets

| Development Phase | Minimum Coverage | Focus Areas |
|-------------------|------------------|-------------|
| POC | 10% | Minimal - core functionality proof |
| Alpha | 40% | Core functionality, happy paths |
| Beta | 60% | Edge cases, error handling |
| Production | 80% | Full coverage - edge cases, error handling, integration |

## Coverage Priority
When adding tests to meet coverage targets, prioritize:
1. Public API functions and methods
2. Error handling and edge cases
3. Critical business logic
4. Integration points
</test_driven_development>

<important_guidelines>
- **Write tests before implementation** - follow TDD Red-Green-Refactor
- Never skip reading reference files before implementing
- Mirror existing patterns exactly - consistency matters
- Run validations frequently, not just at the end
- If validation fails, fix and retry - don't proceed with broken code
- Follow PRP specifications precisely
- Document any necessary deviations
- **Verify code coverage meets phase requirements before completing**
</important_guidelines>
</task>
