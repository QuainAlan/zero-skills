# zero-skills Quick Reference

Quick guide for using zero-skills with Claude Code.

## Installation (Choose One)

### Project-Level (This Repo Only)
```bash
# Already set up in .claude/skills/zero-skills/
# Works automatically when you open this project
```

### Personal-Level (All Projects)
```bash
mkdir -p ~/.claude/skills
git clone https://github.com/zeromicro/zero-skills.git ~/.claude/skills/zero-skills
```

## Usage

### Automatic (Recommended)
Just work with go-zero files:
- Open `.api` or `.proto` files
- Claude loads zero-skills automatically
- Ask questions naturally

### Manual Invocation
```
/zero-skills
/zero-skills Create a REST API
/zero-skills How do I implement rate limiting?
```

### Check If Loaded
```
What skills are available?
```

## Quick Commands

| Command | Description |
|---------|-------------|
| `/zero-skills` | Load skill for go-zero help |
| `/zero-skills [query]` | Load skill with specific question |
| Ask "What skills are available?" | Check loaded skills |

## Pattern Guides (Load On Demand)

| Guide | When to Use |
|-------|-------------|
| [rest-api-patterns.md](references/rest-api-patterns.md) | REST APIs, handlers, middleware |
| [rpc-patterns.md](references/rpc-patterns.md) | gRPC services, service discovery |
| [database-patterns.md](references/database-patterns.md) | SQL, MongoDB, Redis, caching |
| [resilience-patterns.md](references/resilience-patterns.md) | Circuit breakers, rate limiting |
| [troubleshooting/common-issues.md](troubleshooting/common-issues.md) | Debugging errors |
| [best-practices/overview.md](best-practices/overview.md) | Production hardening |

## Key Principles

### ✅ Always Do
- Handler → Logic → Model separation
- Use `httpx.Error()` for HTTP errors
- Load config with `conf.MustLoad`
- Pass `ctx` through all layers
- Generate code with `goctl`

### ❌ Never Do
- Put business logic in handlers
- Hard-code configuration
- Skip error handling
- Bypass ServiceContext injection

## Common Workflows

### Create REST API
1. Define `.api` file with types and routes
2. Generate: `goctl api go -api user.api -dir .`
3. Implement logic in `internal/logic/`
4. Test endpoints

### Add Database
1. Create table schema
2. Generate model: `goctl model mysql datasource -url="..." -table="users" -dir="./model"`
3. Inject into ServiceContext
4. Use in logic layer

### Implement Middleware
1. Create in `internal/middleware/`
2. Register in `.api` or routes
3. Implement auth/validation
4. Handle errors

## Integration with Other Tools

| Tool | Purpose | Command/Usage |
|------|---------|---------------|
| **mcp-zero** | Execute goctl commands | Claude calls automatically |
| **ai-context** | Quick workflows | GitHub Copilot integration |
| **goctl** | Code generation | `goctl api go`, `goctl model`, etc. |

## Advanced Features

### With mcp-zero Installed
```
You: Create a user API with database
```
Claude uses zero-skills (knowledge) + mcp-zero (execution)

### Custom Skills
Create in `.claude/skills/myproject-gozero/` for project-specific patterns

### Subagent Analysis
```
Analyze this go-zero project for issues
```
Uses Explore agent to check architecture compliance

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Skill not loading | Check: `What skills are available?` |
| Not auto-triggering | Invoke manually: `/zero-skills` |
| Need specific pattern | Ask: "Show me REST API middleware patterns" |
| Want to analyze project | Say: "Analyze this go-zero project" |

## Learning Path

1. **New to go-zero?** → [Official Quick Start](https://go-zero.dev/docs/quick-start)
2. **Building APIs?** → [references/rest-api-patterns.md](references/rest-api-patterns.md)
3. **Adding database?** → [references/database-patterns.md](references/database-patterns.md)
4. **Production ready?** → [best-practices/overview.md](best-practices/overview.md)

## Links

- **Skill docs**: [SKILL.md](SKILL.md)
- **Claude Code guide**: [getting-started/claude-code-guide.md](getting-started/claude-code-guide.md)
- **go-zero docs**: [go-zero.dev](https://go-zero.dev)
- **Examples**: [skill-patterns/](skill-patterns/)

## Tips

💡 Be specific: "Create a user API with authentication" > "Help me"
💡 Reference files: ".api files" or "REST API" trigger automatic loading
💡 Use mcp-zero: Combine knowledge (zero-skills) + execution (mcp-zero)
💡 Create custom skills: Extend for project-specific patterns
💡 Check examples: See [skill-patterns/](skill-patterns/) for advanced usage

---

**Need help?** Just ask Claude: "How do I [task] with go-zero?"
