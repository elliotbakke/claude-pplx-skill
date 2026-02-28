# /pplx — Free Perplexity Search in Claude Code (No API Credits)

A Claude Code slash command that gives you Perplexity AI search **without using API credits**. It works by controlling your browser via Chrome's remote debugging — so you search through Perplexity's web UI instead of their paid API.

## Why this exists

Perplexity's API costs money per query. Their Pro subscription gives you unlimited searches on the website, but the API is billed separately. This skill is a workaround: it automates your browser to search Perplexity's web interface, so you get the same results for free — using the subscription you already pay for.

**TL;DR:** If you have Perplexity Pro, you're already paying for unlimited searches. This lets Claude Code use those searches instead of burning API credits.

## What it does

Type `/pplx <your question>` in Claude Code to search the web via Perplexity. The skill automatically selects the best search mode based on your query:

| Trigger words | Mode | Use case |
|--------------|------|----------|
| "deep research", "comprehensive", "in-depth analysis" | `deep` | Long-form research, multi-source synthesis |
| "reasoning", "step by step", "analyze" | `reasoning` | Complex problems, chain-of-thought |
| "pro", "detailed" | `pro` | Better context, richer answers |
| (default — simple questions) | `standard` | Quick factual lookups |

## Prerequisites

This skill is the slash command layer. It requires the **Perplexity MCP server** to do the actual searching:

> **[perplexity-mcp-free](https://github.com/elliotbakke/perplexity-mcp-free)** — Set up the MCP server first. It handles Chrome automation, Playwright, and the connection to perplexity.ai.

Follow the setup instructions in that repo, then come back here to install the `/pplx` command.

## Installation

### 1. Set up the MCP server

Follow the instructions at **[perplexity-mcp-free](https://github.com/elliotbakke/perplexity-mcp-free)** to get the Perplexity MCP server running.

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
- [perplexity-mcp-free](https://github.com/elliotbakke/perplexity-mcp-free) MCP server (set up first)
- Perplexity Pro subscription (for unlimited web searches)

**No Perplexity API key needed.**

## License

MIT
