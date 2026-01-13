# Brainstorm - Feature Planning Session

<task name="brainstorm">
<task_objective>
Facilitate a structured brainstorming session for feature development using Scrum Master techniques. Guide the user through progressive questioning to transform feature ideas into actionable development plans.
</task_objective>

<detailed_sequence_of_steps>

## Phase 1: Context Discovery

1. **Greet and Set Context**
   - Introduce yourself as an experienced Scrum Master facilitator
   - Ask the user to describe the feature or problem they want to explore
   - Establish the session goals

2. **Progressive Questioning**
   - Ask ONE question at a time
   - Wait for user response before proceeding
   - Analyze each response thoroughly using `<thinking>` blocks to:
     - Identify specific insights revealed
     - Assess completeness of the answer
     - Determine remaining knowledge gaps
     - Select the highest-value follow-up question

3. **Core Discovery Questions** (ask adaptively, not all may be needed):
   - What problem are we trying to solve?
   - Who are the target users (primary and secondary)?
   - What does success look like? (business, user, technical metrics)
   - What constraints exist? (technical, business, regulatory)
   - What assumptions are we making?

## Phase 2: User & Requirements Deep Dive

4. **Build on Initial Insights**
   - Ask targeted follow-up questions based on Phase 1 answers
   - Explore user journeys and workflows
   - Identify edge cases and error scenarios
   - Understand integration points with existing systems

5. **Use `search_files` and `read_file`** to:
   - Find existing similar features in the codebase
   - Identify patterns and conventions to follow
   - Understand current architecture constraints

## Phase 3: Solution Exploration

6. **Collaborative Ideation**
   - Present 2-3 potential approaches based on gathered context
   - For each approach, discuss:
     - Key features and benefits
     - Pros and cons
     - Effort estimate (XS/S/M/L/XL)
     - Risk assessment
     - Dependencies

7. **Guide Decision Making**
   - Help user evaluate trade-offs
   - Document reasoning for chosen approach
   - Identify what's being sacrificed and why

## Phase 4: Implementation Planning

8. **Define MVP Scope**
   - Core features for Phase 1
   - Acceptance criteria
   - Definition of done checklist

9. **Plan Future Enhancements**
   - Phase 2+ features with deferral reasoning
   - Nice-to-have improvements

10. **Identify Risks & Dependencies**
    - Technical risks with mitigation strategies
    - External dependencies
    - Knowledge gaps requiring research

## Phase 5: Documentation

11. **Generate Session Document**
    - Use the template from `.clinerules/templates/brainstorming_session_template.md`
    - Save to `docs/brainstorming/YYYY-MM-DD-{feature-name}.md`
    - Include all sections:
      - Context & Problem Statement
      - Brainstormed Ideas & Options
      - Decision Outcome
      - Implementation Plan
      - Action Items & Next Steps
      - Risks & Dependencies
      - Resources & References
      - Session Notes & Insights

</detailed_sequence_of_steps>

<important_guidelines>
- Never rush through questions - quality of information gathering determines session success
- Use `<thinking>` blocks between each user response to analyze and plan next question
- Conduct the session in the user's language
- Write final documentation in English
- Reference existing codebase patterns when discussing implementation
</important_guidelines>
</task>
