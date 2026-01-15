# GitHub Copilot Custom Instructions

This repository uses a specification-driven development workflow with four main slash commands:

- `/brainstorm` - Facilitate structured feature planning sessions
- `/generate-prp` - Generate Product Requirements & Plan documents
- `/execute-prp` - Implement features from PRP specifications
- `/generate-task` - Execute individual development tasks

## Project Structure

```
docs/
├── brainstorming/    # Brainstorming session outputs
├── prps/             # Product Requirements & Plan documents
└── tasks/            # Task breakdown documents

.github/
├── copilot/
│   └── templates/    # Document templates for workflows
└── prompts/          # Slash command definitions
```

## Workflow Sequence

For new features, follow this recommended sequence:

1. `/brainstorm` - Explore and plan the feature
2. `/generate-prp` - Create detailed implementation blueprint
3. `/execute-prp` - Implement simple features in one pass
   OR use `/generate-task` for complex features requiring step-by-step execution

## Key Principles

1. **Progressive Questioning**: Ask ONE question at a time, analyze responses thoughtfully
2. **Pattern Mirroring**: Always read reference files before implementing, mirror existing patterns
3. **Validation-First**: Run validations frequently throughout implementation
4. **Scope Discipline**: Stay within task boundaries, no feature creep
5. **Documentation**: Generate comprehensive documentation for future reference

## Coding Standards

- Follow existing codebase conventions and patterns
- Use consistent naming conventions (check existing files)
- Include proper error handling
- Write tests for new functionality
- Keep code clean and maintainable

## Output Locations

| Workflow | Output Location |
|----------|-----------------|
| Brainstorm | `docs/brainstorming/YYYY-MM-DD-{feature-name}.md` |
| Generate PRP | `docs/prps/{feature-name}.md` |
| Task Breakdown | `docs/tasks/{feature-name}.md` |
