# dotai

AI-powered development template with Claude Code, Task Master, and Cursor integration.

## What is this?

A project template that combines three powerful AI development tools:

- [**Claude Code**](https://docs.anthropic.com/en/docs/claude-code/overview) - Anthropic's CLI for Claude. Requires Pro subscription, or Max for research mode with Opus model
- [**Task Master**](https://github.com/eyaltoledano/claude-task-master) - Tagged task management system
- [**Cursor**](https://www.cursor.com/) (optional) - AI-powered IDE with custom rules

## Getting Started

### Launch Claude Code

```bash
claude
```

### Create App Design Document

```bash
/create-app-design-document
```

Describe what your app does - its purpose, features, and target users.

### Define Tech Stack

```bash
/create-tech-stack
```

Choose your technologies - framework, database, hosting, etc.

### Write Product Requirements

```bash
/prd
```

Create detailed requirements for your first feature.

### Parse Requirements into Tasks

```bash
/parse
```

Convert your PRD into actionable development tasks.

### Start Development

```bash
/next
```

Get your first task and start coding!

### Complete Tasks

```bash
/done
```

Mark tasks complete as you finish them.

## How It Works

Claude Code understands your project through:

- **CLAUDE.md** - Auto-loaded project context and rules
- **Task Master** - Manages tasks through MCP integration
- **Natural language** - Just describe what you want to do

You don't need to memorize commands. Simply ask Claude to:

- "Create a new feature tag for authentication"
- "Show me the next task"
- "Mark this task as complete"
- "What tasks are left in this feature?"

## Commands

### Initial Setup

#### /create-app-design-document

Create high-level application design documentation.

- **Always asks about project stage first** (Pre-MVP, MVP, Production, Enterprise)
- Updates project status in CLAUDE.md
- Focuses on business value and user benefits
- Saves to `.taskmaster/docs/app-design-document.md`

#### /create-tech-stack

Document technical implementation details.

- Analyzes package.json, configs, and code structure
- Documents exact versions and dependencies
- Covers frontend, backend, database, and infrastructure
- Saves to `.taskmaster/docs/tech-stack.md`

### Task Management

#### /prd

Create a Product Requirements Document for new features.

- Analyzes existing codebase for context
- Asks clarifying questions about the feature
- Creates structured PRD with context and requirements
- Saves to `.taskmaster/docs/prd-[feature-name].md`

#### /parse

Convert PRD into Task Master tasks.

- Creates new feature tag
- **Switches to the tag** (critical step)
- Parses PRD into structured tasks
- Ready for development with `/next`

#### /next

Get the next available task.

#### /done

Complete the current task.

### Maintenance & Updates

#### /sync-app-design-document

Update existing app design after changes.

#### /sync-tech-stack

Update tech documentation after changes.

#### /sync-rules

Sync Cursor rules to `CLAUDE.md`.

### Research

#### /debug

Systematic debugging process.

#### /architect

Deep architectural planning for complex features.

#### /ux

Create UX/UI design documentation.

## Tips

### Context Management

- Use `/clear` between different tasks to maintain focus
- Claude automatically reads `CLAUDE.md` for project context
- Task Master state is preserved across sessions

### Quick Commands

- "What's next?" - Get the next task
- "Show task 2.1" - View specific task details
- "Mark as done" - Complete current task
- "Create auth feature tag" - New feature context
- "Switch to payments tag" - Change context

### Creating Custom Commands

Create your own slash commands by adding them to `.claude/commands/`

### Multi-task and Multi-feature Development

Work on multiple tasks within the same feature or across different features:

```bash
# Multi-task development (same feature)
"Show me all tasks in the current tag"
"Show task 2.1" - Review specific task
"Mark as done" - Complete task and move to next

# Multi-feature development
"Switch to the payments tag and show me what's next"
"Create a new tag for mobile development"
"Show me all tags with their progress"
```

### Parallel Development with Git Worktrees

```bash
# Create worktrees for parallel development
git worktree add ../project-api feature/api
git worktree add ../project-components feature/components

# Run Claude Code in each worktree with different tags
cd ../project-api && claude    # Terminal 1: API work
cd ../project-components && claude     # Terminal 2: Components work
```

### Troubleshooting

```bash
# Check current tag
"What tag am I on?"

# Fix task file sync
"Regenerate task files"

# Configure AI models
task-master models --setup
```

## Key Files & Project Structure

### Core Files

- `.taskmaster/tasks/tasks.json` - Tagged task database (auto-managed)
- `.taskmaster/state.json` - Current tag context
- `.taskmaster/config.json` - AI model configuration
- `.taskmaster/docs/prd-<tag>.md` - Product Requirements Documents per tag
- `.taskmaster/tasks/*.md` - Individual task files (auto-generated)

### Claude Code Integration Files

- `CLAUDE.md` - Auto-loaded context for Claude Code
- `.claude/settings.json` - Claude Code tool allowlist and preferences
- `.claude/commands/` - Custom slash commands for repeated workflows
- `.mcp.json` - MCP server configuration

### Directory Structure

```
project/
├── .taskmaster/
│   ├── tasks/              # Tagged task files
│   │   ├── tasks.json      # Task database
│   │   ├── task-1.md      # Individual tasks
│   │   └── task-2.md
│   ├── docs/              # Documentation
│   │   ├── app-design-document.md
│   │   ├── tech-stack.md
│   │   └── prd-<tag>.md
│   ├── reports/           # Analysis reports
│   ├── templates/         # PRD templates
│   ├── state.json         # Current tag context
│   └── config.json        # AI models config
├── .claude/
│   ├── settings.json      # Claude Code config
│   └── commands/         # Custom commands
├── .cursor/              # Cursor IDE rules
│   └── rules/           # Coding standards
├── .mcp.json            # MCP configuration
└── CLAUDE.md            # Project context
```

## License

MIT
