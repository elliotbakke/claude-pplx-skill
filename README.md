# /pplx — Perplexity Search Skill for Claude Code

A Claude Code slash command that turns Claude into a transparent Perplexity AI search proxy with automatic mode selection.

## What it does

Type `/pplx <your question>` in Claude Code to search the web via Perplexity AI. The skill automatically selects the best search mode based on your query:

| Trigger words | Mode | Use case |
|--------------|------|----------|
| "deep research", "comprehensive", "in-depth analysis" | `deep` | Long-form research, multi-source synthesis |
| "reasoning", "step by step", "analyze" | `reasoning` | Complex problems, chain-of-thought |
| "pro", "detailed" | `pro` | Better context, richer answers |
| (default — simple questions) | `standard` | Quick factual lookups |

## Installation

### 1. Install the Perplexity MCP server

This skill requires the [Perplexity MCP server](https://github.com/ppl-ai/modelcontextprotocol) to be configured in Claude Code.

```bash
claude mcp add perplexity -- npx -y @anthropic-ai/perplexity-mcp
```

Or add it manually to your MCP config with your Perplexity API key.

### 2. Install the skill

**Option A: Copy the files manually**

- Copy `commands/pplx.md` to `~/.claude/commands/pplx.md`
- Copy `agents/pplx.md` to `~/.claude/agents/pplx.md`

**Option B: One-liner (macOS/Linux)**

```bash
mkdir -p ~/.claude/commands ~/.claude/agents && \
curl -sL https://raw.githubusercontent.com/elliotbakke/claude-pplx-skill/main/commands/pplx.md -o ~/.claude/commands/pplx.md && \
curl -sL https://raw.githubusercontent.com/elliotbakke/claude-pplx-skill/main/agents/pplx.md -o ~/.claude/agents/pplx.md
```

### 3. Restart Claude Code

The `/pplx` command will now be available in any project.

## Usage

```
/pplx what is the weather in Oslo?
/pplx deep research on AI trends 2025
/pplx reasoning step by step why Bitcoin is rising
```

## Files

| File | Purpose |
|------|---------|
| `commands/pplx.md` | The slash command (what runs when you type `/pplx`) |
| `agents/pplx.md` | The agent definition (handles mode selection and MCP calls) |

## Requirements

- [Claude Code](https://claude.com/claude-code) CLI
- A Perplexity MCP server configured in Claude Code
- Perplexity API key

## License

MIT
