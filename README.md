# Cline Blueprint Workflow

A Cline workflow adaptation of [cc-blueprint-toolkit](https://github.com/croffasia/cc-blueprint-toolkit) for structured, AI-assisted feature development.

## Overview

This workflow provides four commands for blueprint-driven development:

| Command | Purpose |
|---------|---------|
| `/brainstorm` | Facilitate structured feature planning sessions |
| `/generate-prp` | Create comprehensive Product Requirements & Plans |
| `/execute-prp` | Implement features from PRP specifications |
| `/execute-task` | Execute individual tasks from task breakdowns |

## Setup

### 1. Copy to Your Project

Copy the `.clinerules` directory to your project root:

```bash
cp -r .clinerules /path/to/your/project/
```

### 2. Create Output Directories

Create the documentation output directories:

```bash
mkdir -p docs/brainstorming docs/prps docs/tasks
```

### 3. Verify Structure

Your project should now have:

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
│   │   ├── header-javascript.js
│   │   ├── header-typescript.ts
│   │   ├── header-csharp.cs
│   │   └── header-java.java
│   └── code-styles/
│       ├── code-style-javascript.md
│       ├── code-style-typescript.md
│       ├── code-style-csharp.md
│       └── code-style-java.md
├── docs/
│   ├── brainstorming/
│   ├── prps/
│   └── tasks/
└── ... your project files
```

## Usage

### Start a Brainstorming Session

```
/brainstorm
```

Guides you through structured feature discovery:
- Progressive questioning (one question at a time)
- Context discovery and requirements gathering
- Solution exploration with trade-off analysis
- Outputs to `docs/brainstorming/YYYY-MM-DD-feature-name.md`

### Generate a PRP

```
/generate-prp
```

Then describe your feature or provide a user story. The workflow will:
- Analyze your codebase for similar patterns
- Ask clarifying questions
- Research external documentation if needed
- Generate a comprehensive PRP in `docs/prps/feature-name.md`
- Create a task breakdown in `docs/tasks/feature-name.md`

### Execute a PRP

```
/execute-prp docs/prps/feature-name.md
```

Implements the feature following the PRP:
- Reads and follows all specifications
- Studies reference files before coding
- Mirrors existing patterns
- Runs validation commands
- Iterates until all checks pass

### Execute Individual Tasks

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

## Workflow Sequence

For new features, follow this sequence:

```
1. /brainstorm          → Explore and plan the feature
2. /generate-prp        → Create detailed implementation blueprint
3. /execute-prp         → Implement simple features in one pass
   OR
3. /execute-task        → Implement complex features task by task
```

## Templates

### Brainstorming Session Template
Used by `/brainstorm` to document:
- Context & problem statement
- Brainstormed options with pros/cons
- Decision outcome and rationale
- Implementation plan and action items
- Risks and dependencies

### PRP Document Template
Used by `/generate-prp` to create:
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

## Code Styles

Language-specific coding standards are provided in `.clinerules/code-styles/`:

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

All header templates include:
- **Author**: Developer name
- **Date**: Creation date
- **AI Generated**: Flag indicating AI assistance
- **AI Client**: Tool used (Cline, Claude Code, Cursor, etc.)
- **AI Model**: Model used (claude-3-opus, gpt-4, etc.)
- **Copyright**: Standard copyright notice

Example header (JavaScript):
```javascript
/**
 * @file        user-service.js
 * @description User management service
 *
 * @author      John Doe
 * @date        2025-01-13
 *
 * @ai-generated  true
 * @ai-client     Cline
 * @ai-model      claude-3-opus
 *
 * @copyright   Copyright (c) 2025 Acme Corp
 *              All rights reserved.
 */
```

### Using Headers in Workflows

Reference the appropriate header template in your PRPs and task breakdowns:

```markdown
### Implementation Details
- Use header template: `.clinerules/templates/header-typescript.ts`
- Follow code style: `.clinerules/code-styles/code-style-typescript.md`
```

## Customization

### Modify Templates

Edit files in `.clinerules/templates/` to match your team's documentation standards.

### Adjust Workflows

Edit files in `.clinerules/workflows/` to:
- Add project-specific validation commands
- Include additional research steps
- Modify questioning approaches

### Add New Workflows

Create new `.md` files in `.clinerules/workflows/` following the structure:

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

### Add New Code Styles

To add a code style for another language:

1. Create `code-style-{language}.md` in `.clinerules/code-styles/`
2. Create `header-{language}.{ext}` in `.clinerules/templates/`

Header template must include:
```
- File name
- Description
- Author
- Date
- AI Generated flag
- AI Client
- AI Model
- Copyright notice
- Version
```

## Credits

Based on [cc-blueprint-toolkit](https://github.com/croffasia/cc-blueprint-toolkit) by croffasia.

## License

MIT
