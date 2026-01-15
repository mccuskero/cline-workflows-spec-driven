# AI-Assisted Specification-Driven Development Workflows

A collection of structured workflows for AI-assisted feature development, supporting both **Cline** and **GitHub Copilot**.

Based on [cc-blueprint-toolkit](https://github.com/croffasia/cc-blueprint-toolkit) by croffasia.

## Overview

This repository provides four core workflows for blueprint-driven development:

| Workflow | Purpose |
|----------|---------|
| **Brainstorm** | Facilitate structured feature planning sessions |
| **Generate PRP** | Create comprehensive Product Requirements & Plans |
| **Execute PRP** | Implement features from PRP specifications |
| **Execute Task** | Execute individual tasks from task breakdowns |

### Recommended Workflow Sequence

```
1. brainstorm       → Explore and plan the feature
2. generate-prp     → Create detailed implementation blueprint
3. execute-prp      → Implement simple features in one pass
   OR
3. execute-task     → Implement complex features task by task
```

### Key Principles

1. **Progressive Questioning**: Ask ONE question at a time, analyze responses thoughtfully
2. **Pattern Mirroring**: Always read reference files before implementing, mirror existing patterns
3. **Validation-First**: Run validations frequently throughout implementation
4. **Scope Discipline**: Stay within task boundaries, no feature creep
5. **Documentation**: Generate comprehensive documentation for future reference
6. **Test-Driven Development**: Write tests before implementation code

---

## Test-Driven Development (TDD)

All workflows enforce Test-Driven Development practices with phased code coverage targets.

### TDD Principles

Follow the **Red-Green-Refactor** cycle for all implementation:

1. **Red**: Write a failing test first that defines expected behavior
2. **Green**: Write minimal code to make the test pass
3. **Refactor**: Clean up code while keeping tests green

### Code Coverage Targets

| Development Phase | Minimum Coverage | Focus Areas |
|-------------------|------------------|-------------|
| **Phase 1 / POC** | 20% | Core functionality, happy paths |
| **Beta Phase** | 80% | Edge cases, error handling, integration |

### Coverage Priority

When writing tests to meet coverage targets, prioritize:

1. Public API functions and methods
2. Error handling and edge cases
3. Critical business logic
4. Integration points

### How TDD is Enforced

- **`/generate-prp`** asks about development phase and includes coverage targets in the PRP
- **`/execute-prp`** and **`/execute-task`** verify coverage before marking implementation complete
- Completion reports include coverage achieved vs. target

### Example Workflow

```
1. /generate-prp
   → "What development phase is this? (POC or Beta)"
   → User: "POC"
   → PRP includes: Coverage Target: 20%

2. /execute-prp docs/prps/feature.md
   → Write failing tests for first component (Red)
   → Implement to pass tests (Green)
   → Refactor and clean up
   → Verify 20% coverage achieved
   → Report: "Coverage: 23% (Target: 20%) ✓"
```

---

## Cline Workflows

Cline workflows are defined in `.clinerules/workflows/` and use Cline's task-based prompt structure.

### Setup for Cline

#### 1. Copy to Your Project

```bash
cp -r .clinerules /path/to/your/project/
```

#### 2. Create Output Directories

```bash
mkdir -p docs/brainstorming docs/prps docs/tasks
```

#### 3. Verify Structure

```
your-project/
├── .clinerules/
│   ├── workflows/
│   │   ├── brainstorm.md
│   │   ├── generate-prp.md
│   │   ├── execute-prp.md
│   │   └── execute-task.md
│   ├── templates/
│   │   ├── brainstorming_session_template.md
│   │   ├── prp_document_template.md
│   │   ├── technical-task-template.md
│   │   └── header-*.{js,ts,cs,java}
│   └── code-styles/
│       └── code-style-*.md
├── docs/
│   ├── brainstorming/
│   ├── prps/
│   └── tasks/
└── ... your project files
```

### Cline Commands

#### Start a Brainstorming Session

```
/brainstorm
```

Guides you through structured feature discovery:
- Progressive questioning (one question at a time)
- Context discovery and requirements gathering
- Solution exploration with trade-off analysis
- Outputs to `docs/brainstorming/YYYY-MM-DD-feature-name.md`

#### Generate a PRP

```
/generate-prp
```

Then describe your feature or provide a user story. The workflow will:
- Analyze your codebase for similar patterns
- Ask clarifying questions
- Research external documentation if needed
- Generate a comprehensive PRP in `docs/prps/feature-name.md`
- Create a task breakdown in `docs/tasks/feature-name.md`

#### Execute a PRP

```
/execute-prp docs/prps/feature-name.md
```

Implements the feature following the PRP:
- Reads and follows all specifications
- Studies reference files before coding
- Mirrors existing patterns
- Runs validation commands
- Iterates until all checks pass

#### Execute Individual Tasks

```
/execute-task docs/tasks/feature-name.md
```

Or specify a task ID:

```
/execute-task docs/tasks/feature-name.md T-001
```

Focused implementation of single tasks:
- Stays within task boundaries
- Validates acceptance criteria
- Runs quality gates

### Cline File Structure

| Directory | Contents |
|-----------|----------|
| `.clinerules/workflows/` | Workflow definitions with task XML structure |
| `.clinerules/templates/` | Document templates and code header templates |
| `.clinerules/code-styles/` | Language-specific coding standards |

---

## GitHub Copilot Workflows

GitHub Copilot workflows are defined in `.github/prompts/` as `.prompt.md` files, following GitHub's custom prompt conventions.

### Setup for GitHub Copilot

#### 1. Copy to Your Project

```bash
cp -r .github /path/to/your/project/
mkdir -p docs/brainstorming docs/prps docs/tasks
```

#### 2. Verify Structure

```
your-project/
├── .github/
│   ├── copilot-instructions.md      # Project-wide Copilot instructions
│   ├── prompts/
│   │   ├── brainstorm.prompt.md     # /brainstorm command
│   │   ├── generate-prp.prompt.md   # /generate-prp command
│   │   ├── execute-prp.prompt.md    # /execute-prp command
│   │   └── execute-task.prompt.md   # /execute-task command
│   └── copilot/
│       ├── templates/               # Document & header templates
│       │   ├── brainstorming_session_template.md
│       │   ├── prp_document_template.md
│       │   ├── technical-task-template.md
│       │   └── header-*.{js,ts,cs,java}
│       └── code-styles/             # Language-specific coding standards
│           └── code-style-*.md
├── docs/
│   ├── brainstorming/
│   ├── prps/
│   └── tasks/
└── ... your project files
```

### GitHub Copilot Commands

In VS Code with GitHub Copilot Chat, use these slash commands:

#### Start a Brainstorming Session

```
/brainstorm
```

Facilitates structured feature planning using Scrum Master techniques:
- Progressive discovery questioning
- Solution exploration with 2-3 approaches
- Trade-off analysis and decision documentation
- Outputs to `docs/brainstorming/YYYY-MM-DD-feature-name.md`

#### Generate a PRP

```
/generate-prp
```

Creates comprehensive Product Requirements & Plan documents:
- Codebase analysis for patterns
- Clarifying questions (one at a time)
- Smart external research decisions
- Generates PRP in `docs/prps/feature-name.md`
- Creates task breakdown in `docs/tasks/feature-name.md`

#### Execute a PRP

```
/execute-prp docs/prps/feature-name.md
```

Implements features from PRP specifications:
- Loads and parses complete PRP
- Studies all reference files
- Mirrors existing patterns
- Runs validation commands
- Reports completion status

#### Execute Individual Tasks

```
/execute-task docs/tasks/feature-name.md
```

Or with a specific task ID:

```
/execute-task docs/tasks/feature-name.md T-001
```

Focused task implementation:
- Analyzes task requirements and acceptance criteria
- Implements within task boundaries
- Validates Given-When-Then scenarios
- Runs quality gates

### GitHub Copilot File Structure

| Directory/File | Purpose |
|----------------|---------|
| `.github/copilot-instructions.md` | Project-wide custom instructions (auto-included in all requests) |
| `.github/prompts/*.prompt.md` | Slash command definitions |
| `.github/copilot/templates/` | Document templates and code header templates |
| `.github/copilot/code-styles/` | Language-specific coding standards |

### Prompt File Format

GitHub Copilot prompt files use frontmatter with markdown content:

```yaml
---
mode: agent
description: Brief description of the command
---

# Command Title

Detailed instructions...
```

---

## Templates

### Brainstorming Session Template

Used by brainstorm workflows to document:
- Context & problem statement
- Brainstormed options with pros/cons/effort/risk
- Decision outcome and rationale
- Implementation plan and action items
- Risks and dependencies

### PRP Document Template

Used by generate-prp workflows to create:
- Discovery summary and clarifications
- Goals, scope, and success criteria
- Complete implementation context
- Ordered task list with pseudocode
- Validation commands and checklists

### Technical Task Template

Used for task breakdowns containing:
- Task identification and priority
- Functional and non-functional requirements
- Implementation details and patterns
- Given-When-Then acceptance criteria
- Quality gates and definition of done

---

## Code Standards

Both Cline and GitHub Copilot workflows enforce consistent code standards through header templates and style guides.

### File Locations

| Tool | Style Guides | Header Templates |
|------|--------------|------------------|
| Cline | `.clinerules/code-styles/` | `.clinerules/templates/` |
| GitHub Copilot | `.github/copilot/code-styles/` | `.github/copilot/templates/` |

### Supported Languages

| Language | Style Guide | Header Template |
|----------|-------------|-----------------|
| JavaScript | `code-style-javascript.md` | `header-javascript.js` |
| TypeScript | `code-style-typescript.md` | `header-typescript.ts` |
| C# | `code-style-csharp.md` | `header-csharp.cs` |
| Java | `code-style-java.md` | `header-java.java` |

### Code Style Contents

Each style guide covers:
- Naming conventions (variables, functions, classes, etc.)
- Formatting rules (indentation, braces, line length)
- Language-specific best practices
- Documentation standards
- Testing conventions

### File Header Templates

All new source files created by workflows MUST include the appropriate header. Headers include:

| Field | Description |
|-------|-------------|
| `@file` | Filename |
| `@description` | Brief purpose description |
| `@author` | Developer name |
| `@date` | Creation date (YYYY-MM-DD) |
| `@ai-generated` | Set to `true` for AI-generated code |
| `@ai-client` | Tool used (Cline, GitHub Copilot, Claude Code, etc.) |
| `@ai-model` | Model used (claude-3-opus, gpt-4, etc.) |
| `@copyright` | Organization copyright notice |
| `@version` | Version number |

**Example header (JavaScript):**
```javascript
/**
 * @file        user-service.js
 * @description User management service
 *
 * @author      John Doe
 * @date        2025-01-14
 *
 * @ai-generated  true
 * @ai-client     GitHub Copilot
 * @ai-model      gpt-4
 *
 * @copyright   Copyright (c) 2025 Acme Corp
 *              All rights reserved.
 *
 * @version     1.0.0
 */
```

### Using Code Standards in Workflows

When executing `/execute-prp` or `/execute-task`, the workflows automatically:
1. Reference the appropriate header template for the language
2. Apply the corresponding code style guide
3. Populate header fields with current context

PRPs generated by `/generate-prp` include a Code Standards section specifying which templates and guides to use.

---

## Output Locations

Both Cline and GitHub Copilot workflows output to the same directories:

| Output Type | Location |
|-------------|----------|
| Brainstorming Sessions | `docs/brainstorming/YYYY-MM-DD-{feature-name}.md` |
| PRP Documents | `docs/prps/{feature-name}.md` |
| Task Breakdowns | `docs/tasks/{feature-name}.md` |

---

## Customization

### Modify Templates

- **Cline**: Edit files in `.clinerules/templates/`
- **Copilot**: Edit files in `.github/copilot/templates/`

### Modify Code Standards

- **Cline**: Edit files in `.clinerules/code-styles/` and header templates in `.clinerules/templates/`
- **Copilot**: Edit files in `.github/copilot/code-styles/` and header templates in `.github/copilot/templates/`

### Adjust Workflows

- **Cline**: Edit files in `.clinerules/workflows/`
- **Copilot**: Edit files in `.github/prompts/`

### Add New Workflows

**For Cline**, create new `.md` files in `.clinerules/workflows/`:

```markdown
# Workflow Name

<task name="workflow-name">
<task_objective>
What this workflow accomplishes
</task_objective>

<detailed_sequence_of_steps>
## Phase 1: ...
1. Step one
2. Step two
</detailed_sequence_of_steps>
</task>
```

**For GitHub Copilot**, create new `.prompt.md` files in `.github/prompts/`:

```yaml
---
mode: agent
description: What this command does
---

# Command Name

## Phase 1: ...
1. Step one
2. Step two
```

---

## Credits

Based on [cc-blueprint-toolkit](https://github.com/croffasia/cc-blueprint-toolkit) by croffasia.

## License

MIT
