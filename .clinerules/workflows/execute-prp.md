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

## Phase 3: Execute the Plan

7. **Implement Each Component**
   For each implementation task:

   a. **Read Reference First**
      - Always read corresponding reference files before coding
      - Examine reference implementations thoroughly

   b. **Adapt Patterns**
      - Mirror reference patterns for your feature
      - Maintain consistency with existing codebase

   c. **Write Code**
      - Use `write_to_file` for new files
      - Use `apply_diff` for modifications
      - Follow PRP specifications exactly
      - Apply established patterns from reference files

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

10. **Fix Failures**
    - If any validation fails:
      - Analyze error messages
      - Use error patterns from PRP to guide fixes
      - Apply corrections
      - Re-run validation

11. **Iterate Until Pass**
    - Continue fix-validate cycle until all checks pass
    - Document any issues encountered and solutions applied

## Phase 5: Complete

12. **Final Checklist Verification**
    - Review each item in the PRP's final checklist
    - Ensure all acceptance criteria are met
    - Verify all integration points work correctly

13. **Execute Final Validation Suite**
    - Run complete test suite
    - Verify build succeeds
    - Check for any warnings or issues

14. **Re-read PRP for Completeness**
    - Reference PRP document again
    - Confirm every requirement has been addressed
    - Check nothing was missed

15. **Report Completion Status**
    - Summarize what was implemented
    - Note any deviations from PRP (with reasoning)
    - List any follow-up items identified
    - Report final validation results

</detailed_sequence_of_steps>

<important_guidelines>
- Never skip reading reference files before implementing
- Mirror existing patterns exactly - consistency matters
- Run validations frequently, not just at the end
- If validation fails, fix and retry - don't proceed with broken code
- Follow PRP specifications precisely
- Document any necessary deviations
</important_guidelines>
</task>
