# Execute Task - Individual Task Implementation

<task name="execute-task">
<task_objective>
Execute individual development tasks from task breakdown documents. Provides focused, incremental implementation for complex features that benefit from step-by-step execution.
</task_objective>

<input>
Path to task file (e.g., `docs/tasks/feature-name.md`) and optionally a specific task ID (e.g., `T-001`)
</input>

<detailed_sequence_of_steps>

## Step 1: Load Task Document

1. **Read Task File**
   - Use `read_file` to load the task document
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
   - Use `search_files` to find similar implementations
   - Document patterns to follow

## Step 3: Implementation Planning

8. **Create Focused Plan**
   - Break task into specific implementation steps
   - Order steps by dependency
   - Identify files to create or modify

9. **Study All Referenced Files**
   - Use `read_file` on each referenced file
   - Understand existing structure and patterns
   - Note integration points

10. **Identify Patterns to Mirror**
    - Document code patterns from existing implementations
    - Note naming conventions
    - Understand error handling approaches

## Step 4: Focused Implementation

11. **Read Reference Files Before Coding**
    - Always examine reference implementation first
    - Understand the pattern being used
    - Note any edge cases handled

12. **Implement Only Specified Requirements**
    - Stay within task boundaries
    - Don't add unrequested features
    - Don't refactor unrelated code

13. **Mirror Existing Patterns**
    - Use same code structure as references
    - Follow established naming conventions
    - Apply consistent error handling

14. **Test Incrementally**
    - Run tests after each significant change
    - Verify functionality as you go
    - Don't wait until the end to test

## Step 5: Acceptance Criteria Validation

15. **Execute Given-When-Then Scenarios**
    For each acceptance criterion:
    - Set up the Given conditions
    - Perform the When actions
    - Verify the Then outcomes

16. **Verify All Criteria Complete**
    - Check off each acceptance criterion
    - Document any criteria that couldn't be met
    - Note any issues or edge cases discovered

17. **Run Validation Commands**
    - Execute commands specified in task document
    - Run relevant test suites
    - Check for regressions

## Step 6: Quality Gates

18. **Run Code Quality Checks**
    - Execute lint commands
    - Run type checking
    - Check for code style violations

19. **Fix Any Issues**
    - Address linting errors
    - Fix type checking failures
    - Resolve style violations

20. **Verify Definition of Done**
    - Check all DoD criteria from task document
    - Ensure code is complete and tested
    - Verify documentation is updated if required

## Step 7: Task Completion

21. **Mark Task Complete**
    - Update task status in document if applicable
    - Note completion in conversation

22. **Document Implementation Notes**
    - Record any deviations from original plan
    - Note decisions made during implementation
    - Document any discovered issues

23. **Report Results**
    - Summarize what was implemented
    - List files created/modified
    - Report validation results
    - Identify any follow-up items

</detailed_sequence_of_steps>

<important_guidelines>
- Stay within task boundaries - don't scope creep
- Reference existing patterns extensively
- Test incrementally - don't batch testing
- Follow specified file structures
- Verify dependencies before starting
- Document everything for future reference
</important_guidelines>
</task>
