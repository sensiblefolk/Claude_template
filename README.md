# dotai

AI-powered development template with Claude Code, Task Master, and Cursor integration.

## What is this?

A project template that combines three powerful AI development tools:

- [**Claude Code**](https://docs.anthropic.com/en/docs/claude-code/overview) - Anthropic's CLI for Claude
- [**Task Master**](https://github.com/eyaltoledano/claude-task-master) - Tagged task management system
- [**Cursor**](https://www.cursor.com/) - AI-powered IDE for precise code review workflows (optional)

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

### Planning & Documentation

#### /create-app-design-document

Creates a comprehensive Application Design Document from codebase analysis.

- Analyzes existing codebase for features and architecture
- Asks 5-8 clarifying questions about project stage and business goals
- Updates CLAUDE.md Project Status section with development priorities
- Generates high-level app overview focusing on "what" not "how"
- Saves to `.taskmaster/docs/app-design-document.md`

#### /create-tech-stack

Documents the complete technical stack and development setup.

- Deep analysis of package.json, configs, and code structure
- Asks 4-6 questions about deployment, hosting, and workflow
- Covers languages, frameworks, databases, tools, and infrastructure
- Includes specific versions, configurations, and setup details
- Saves to `.taskmaster/docs/tech-stack.md`

#### /prd

Creates a detailed Product Requirements Document for a new feature.

- Analyzes existing codebase to understand integration points
- Asks 4-6 clarifying questions about goals, users, and scope
- Follows structured format with context and technical sections
- Written for junior developers with clear, actionable requirements
- Saves to `.taskmaster/docs/prd-[feature-name].md`

### Task Management

#### /parse

Converts a PRD into actionable Task Master tasks.

- Creates new feature tag with description
- Switches to the new tag
- Parses PRD into structured, dependency-ordered tasks
- Ready for development workflow with `/next`

#### /next

Shows the next available task in current tag context.

- Finds tasks with satisfied dependencies
- Displays complete task details and implementation plan
- Provides summary and suggests first implementation step
- Respects project's logical development sequence

#### /done

Marks current task as complete and shows next task.

- Reviews task details for completion verification
- Runs relevant tests if applicable
- Sets task status to 'done' in Task Master
- Automatically shows next available task

### Maintenance & Updates

#### /sync-app-design-document

Updates existing app design document after project changes.

- Asks about project stage changes first
- Identifies new, changed, or removed features from codebase
- Preserves accurate existing content, adds new information
- Updates CLAUDE.md Project Status if stage evolved
- Maintains high-level, business-focused perspective

#### /sync-tech-stack

Updates tech documentation after dependency or infrastructure changes.

- Analyzes package.json changes and configuration updates
- Asks about hosting, deployment, and tooling evolution
- Updates versions, tools, and technical specifications
- Preserves accurate content while reflecting current state
- Maintains technical precision with exact versions

#### /sync-rules

Synchronizes Cursor rules to CLAUDE.md Development Rules section.

- Scans all `.cursor/rules/*.mdc` files automatically
- Organizes rules by logical categories
- Updates references with context and applicability
- Ensures Claude Code follows same patterns as Cursor

### Development Support

#### /debug

Systematic debugging process for complex issues.

#### /architect

Comprehensive system design and architecture planning.

#### /ux

Creates comprehensive UX/UI design documentation.

## Tips

### Claude Code vs Cursor

**Use Claude Code by default** for most development work:

✅ **Better for:**

- Long-term project understanding and context retention
- All Task Master AI commands
- Parallel development
- Cheapest plan for extensive usage of Claude Opus

❌ **Limitations:**

- No chat history persistence between sessions
- Less granular control over individual file changes

**Switch to Cursor when you need:**

✅ **Granular code review control:**

- Accept/reject specific diffs on a file-by-file basis
- Visual diff review with inline code navigation
- Restore points and easy change reversal
- Complex refactoring requiring careful code inspection

❌ **Limitations:**

- Becomes slow and unstable with long conversations
- Only supports non-AI Task Master commands
- Project context management is less efficient than in Claude Code
- Requires creating new chats frequently

**Recommended Plans:**

**Claude Pro ($20/month) → Team ($100/month)**

- Start with Pro plan for basic usage
- **Upgrade to Max (5x - $100/month) for large projects** - much higher usage limits, unlocks Claude Opus model for deeper research
- Switch to Max (20x - $200/month) if you hit limits frequently

**Cursor Pro ($20/month)**

- Optional, but essential for granular code review workflows
- Visual diff management and restore points
- Complements Claude Code perfectly for precision editing

### Context Management

- **Claude Code**: Use `/clear` between different tasks to maintain focus
- **Claude Code**: Automatically reads `CLAUDE.md` for project context
- **Both tools**: Task Master state is preserved across sessions

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
