# go-zero Skills for AI Agents

English | [简体中文](README_CN.md)

This is an [Agent Skill](https://anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills) containing structured knowledge and patterns for AI coding assistants to help developers work effectively with the [go-zero](https://github.com/zeromicro/go-zero) framework.

## What is a Skill?

Skills are folders of instructions, scripts, and resources that AI agents discover and load dynamically to perform better at specific tasks. This skill teaches AI agents how to generate production-ready go-zero microservices code.

## Purpose

This skill enables AI agents (Claude, GitHub Copilot, Cursor, etc.) to:
- Generate accurate go-zero code following framework conventions
- Understand the three-layer architecture (Handler → Logic → Model)
- Apply best practices for microservices development
- Troubleshoot common issues efficiently
- Build production-ready applications

## Agent Skill Structure

Following the [Agent Skills Spec](https://github.com/anthropics/skills/blob/main/spec/agent-skills-spec.md) and [Claude Code skills documentation](https://code.claude.com/docs/en/skills):

```
zero-skills/
├── SKILL.md                    # Entry point with YAML frontmatter
├── QUICKSTART.md               # Quick reference card
├── getting-started/            # Getting started guides
│   └── claude-code-guide.md    # Using zero-skills with Claude Code
├── references/                 # Detailed pattern documentation
│   ├── rest-api-patterns.md    # REST API development patterns
│   ├── rpc-patterns.md         # gRPC service patterns
│   ├── database-patterns.md    # Database operations
│   └── resilience-patterns.md  # Resilience and fault tolerance
├── best-practices/             # Production recommendations
├── troubleshooting/            # Common issues and solutions
├── skill-patterns/             # Advanced skill examples (templates)
│   ├── analyze-project.md      # Explore agent example
│   ├── generate-service.md     # Argument passing example
│   └── plan-architecture.md    # Plan agent example
└── examples/                   # Demo projects and verification
```

## Using This Skill

### With Claude Code (Recommended)

Claude Code natively supports the [Agent Skills specification](https://agentskills.io/). This skill is optimized for Claude Code with advanced features:

#### Project-Level Installation (Git Submodule)
Add zero-skills to your project for automatic discovery:

```bash
# Add as git submodule
git submodule add https://github.com/zeromicro/zero-skills.git .claude/skills/zero-skills

# Or clone directly
git clone https://github.com/zeromicro/zero-skills.git .claude/skills/zero-skills
```

Claude Code automatically discovers skills in `.claude/skills/` directories.

#### Personal-Level Installation
To use across all your projects, install to your personal skills directory:

```bash
## Clone to personal skills directory
git clone https://github.com/zeromicro/zero-skills.git ~/.claude/skills/zero-skills
```

#### Usage in Claude Code
- **Automatic**: Claude loads the skill when you work with go-zero files (`.api`, `.proto`, `go.mod` with go-zero)
- **Manual**: Type `/zero-skills` to invoke directly for go-zero guidance
- **With arguments**: `/zero-skills Create a user management API` for specific tasks
- **Check availability**: Ask "What skills are available?" to see if it's loaded

#### Advanced Features
- **Dynamic context**: Skills can execute shell commands to gather live project data
- **Subagents**: Use `context: fork` for isolated analysis or planning tasks
- **Tool restrictions**: `allowed-tools` ensures safe, read-only operations
- See [skill-patterns/](skill-patterns/) for advanced patterns and templates

### With Claude Desktop

Add to `claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "zero-skills": {
      "command": "node",
      "args": ["/path/to/skill-server.js", "/path/to/zero-skills"]
    }
  }
}
```

### With GitHub Copilot

Use [ai-context](https://github.com/zeromicro/ai-context) which provides concise workflow instructions that reference this skill. Add to `.github/copilot-instructions.md`:

```markdown
# go-zero Development Context

Follow go-zero patterns from https://github.com/zeromicro/zero-skills

Key principles:
- Three-layer architecture (Handler → Logic → Model)
- Use goctl for code generation
- See ai-context for workflows
```

### With Cursor/Windsurf/Other IDEs

Reference the skill in your project rules:
2. **Windsurf**: Add to `.windsurfrules`
3. **Other**: Include relevant pattern files from `references/` in your context

## Integration with go-zero AI Ecosystem

zero-skills is part of a three-tool ecosystem for AI-assisted go-zero development:

| Tool | Purpose | Size | Best For |
|------|---------|------|----------|
| **[ai-context](https://github.com/zeromicro/ai-context)** | Workflow instructions and decision trees | ~5KB | GitHub Copilot, Cursor, Windsurf |
| **zero-skills** (this repo) | Comprehensive knowledge base | ~40KB | Claude Code, deep learning, reference |
| **[mcp-zero](https://github.com/zeromicro/mcp-zero)** | Runtime tools (execute goctl commands) | MCP Server | Claude Desktop/Code for code generation |

### How They Work Together

```
┌─────────────────────────────────────────────────────────────┐
│                     AI Assistant                            │
│  (Claude Code, GitHub Copilot, Cursor, etc.)               │
└────────────┬─────────────────────┬──────────────────────────┘
             │                     │
             ├─ Workflow Layer ────┤
             │  ai-context         │  "What to do" - Quick decisions
             │  (~5KB)             │  Loaded for every interaction
             │                     │
             ├─ Knowledge Layer ───┤
             │  zero-skills        │  "How & Why" - Detailed patterns
             │  (~40KB)            │  Loaded when needed
             │                     │
             └─ Execution Layer ───┘
                mcp-zero             "Do it" - Run goctl commands
                (MCP Server)          Generate actual code files
```

### Usage Scenarios

**Scenario 1: GitHub Copilot User**
- Uses: `ai-context` (loaded via `.github/copilot-instructions.md`)
- Benefits: Quick inline suggestions, workflow guidance
- Limitation: No code execution, manual goctl commands

**Scenario 2: Claude Code User (Best Experience)**
- Uses: `zero-skills` (this repo) + `mcp-zero` tools
- Benefits:
  - Deep knowledge from pattern guides
  - Automatic code generation via goctl
  - Dynamic context with live project data
  - Subagent workflows for complex tasks
- Invocation: `/zero-skills` or automatic when working with go-zero

**Scenario 3: Cursor/Windsurf User**
- Uses: `ai-context` (in project rules) + links to `zero-skills`
- Benefits: IDE-native experience with go-zero guidance

See [Claude Code Guide](getting-started/claude-code-guide.md) for detailed integration instructions and best practices.

## Quick Links

- 📖 **[SKILL.md](SKILL.md)** - Main skill entry point and navigation
- ⚡ **[QUICKSTART.md](QUICKSTART.md)** - Quick reference card
-  **[go-zero Quick Start](https://go-zero.dev/docs/quick-start)** - Official go-zero framework tutorial
- 💡 **[Claude Code Guide](getting-started/claude-code-guide.md)** - Using zero-skills with Claude Code
- 🎯 **[Advanced Examples](skill-patterns/)** - Subagents, dynamic context, etc.

## Contributing

Contributions are welcome! Please ensure:
- Examples are complete and tested
- Patterns follow official go-zero conventions
- Content is structured for AI consumption
- Include both correct (✅) and incorrect (❌) examples
- Follow the [Agent Skills specification](https://agentskills.io/)

## License

MIT License - Same as go-zero framework
