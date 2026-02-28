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

## How it works

1. Chrome runs with `--remote-debugging-port=9222` (allows external control)
2. A Playwright MCP server connects to that Chrome instance
3. When you run `/pplx`, Claude types your query into perplexity.ai and reads the response
4. The result is passed back to you — no API key needed

## Installation

### 1. Set up Chrome with remote debugging

Chrome needs to start with the `--remote-debugging-port=9222` flag. Add it to your Chrome shortcut or start script:

**Windows:**
```
"C:\Program Files\Google\Chrome\Application\chrome.exe" --remote-debugging-port=9222
```

**macOS:**
```bash
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --remote-debugging-port=9222
```

### 2. Install the Playwright MCP server

```bash
claude mcp add perplexity -- npx -y @anthropic-ai/playwright-mcp
```

Or use any Playwright-based MCP that connects to your Chrome instance.

### 3. Install the skill

**Option A: Copy the files manually**

- Copy `commands/pplx.md` to `~/.claude/commands/pplx.md`
- Copy `agents/pplx.md` to `~/.claude/agents/pplx.md`

**Option B: One-liner (macOS/Linux)**

```bash
mkdir -p ~/.claude/commands ~/.claude/agents && \
curl -sL https://raw.githubusercontent.com/elliotbakke/claude-pplx-skill/main/commands/pplx.md -o ~/.claude/commands/pplx.md && \
curl -sL https://raw.githubusercontent.com/elliotbakke/claude-pplx-skill/main/agents/pplx.md -o ~/.claude/agents/pplx.md
```

### 4. Restart Claude Code

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
- Chrome running with `--remote-debugging-port=9222`
- A Playwright-based MCP server connected to Chrome
- Perplexity Pro subscription (for unlimited web searches)

**No Perplexity API key needed.**

## License

MIT
