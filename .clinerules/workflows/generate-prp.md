# Generate PRP - Product Requirements & Plan

<task name="generate-prp">
<task_objective>
Generate a comprehensive Product Requirements & Plan (PRP) document through validated research and codebase analysis. The PRP provides complete context for AI-assisted implementation.
</task_objective>

<input>
Feature description, user story, or path to brainstorming document
</input>

<detailed_sequence_of_steps>

## Phase 1: Initial Discovery & Task Validation

1. **Preflight Analysis**
   - Scan project structure for similar existing features using `search_files`
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
   - Use `<thinking>` blocks to analyze each response

3. **Decision Gate**
   - Only proceed to Phase 2 when gaps are adequately addressed
   - If critical information is missing, continue asking questions

## Phase 2: Comprehensive Research

4. **Codebase Analysis**
   - Use `search_files` and `read_file` to:
     - Find similar features and patterns
     - Identify reference files and implementations
     - Note coding conventions and standards
     - Understand existing architecture
   - Document findings in `<thinking>` blocks

5. **Smart External Research Decision**
   - **SKIP external research if:**
     - Similar components exist in codebase
     - Implementation patterns are already established
     - Standard library/framework features suffice

   - **PROCEED with external research if:**
     - Integrating new external libraries
     - Implementing complex undocumented features
     - No codebase examples exist
     - Security considerations require verification

6. **Conditional External Research** (if needed)
   - Use `ask_followup_question` to ask user if web research is acceptable
   - Focus narrowly on identified knowledge gaps
   - Research external package documentation
   - Look for complex patterns and best practices
   - Consider security implications for new integrations

## Phase 3: PRP Document Generation

7. **Prepare Document Structure**
   - Read template from `.clinerules/templates/prp_document_template.md`
   - Ensure all research phases are complete
   - Gather complete codebase context

8. **Write PRP Document** with these sections:

   ### Discovery Summary
   - Initial task analysis (original request)
   - User clarifications (Q&A from discovery)
   - Missing requirements identified

   ### Goal, Why, What
   - Clear articulation of what needs building
   - Business value and integration context
   - Success criteria as measurable outcomes

   ### All Needed Context
   - Research findings summary
   - Documentation and reference links
   - Current and desired codebase structure
   - Library quirks and critical gotchas

   ### Implementation Blueprint
   - Data models and type structures
   - Ordered task list with specific modifications
   - Pseudocode with critical details
   - Integration points (database, API, routing, state)

   ### Validation Loop
   - Lint and type-check commands
   - Test commands
   - Final checklist (tests, linting, builds, manual verification)
   - Anti-patterns to avoid

9. **Save PRP Document**
   - Save to `docs/prps/{feature-name}.md`
   - Use kebab-case for filename

## Phase 4: Task Breakdown Generation

10. **Generate Task Breakdown**
    - Decompose requirements into manageable development tasks
    - Apply work breakdown structure principles
    - Define clear dependencies between tasks
    - Create Given-When-Then acceptance criteria for each task
    - Use template from `.clinerules/templates/technical-task-template.md`

11. **Save Task Document**
    - Save to `docs/tasks/{feature-name}.md`
    - Link task breakdown back into the PRP document

## Phase 5: Quality Assurance

12. **Validate PRP Completeness**
    - Check for necessary context coverage
    - Verify executable validation commands exist
    - Confirm existing pattern references are included
    - Ensure clear implementation paths are defined
    - Validate error handling is documented

13. **Assign Confidence Score**
    - Rate 1-10 for likelihood of one-pass implementation success
    - Document reasoning for the score
    - Identify any remaining risks or uncertainties

</detailed_sequence_of_steps>

<important_guidelines>
- Ask clarification questions in the user's language
- Write final PRP document in English
- Include ALL relevant documentation references
- Provide executable test/lint commands
- Use existing codebase keywords and patterns
- Never assume - ask when uncertain
</important_guidelines>
</task>
