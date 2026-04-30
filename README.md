# Flush 🔄

**Session archival and context compression for AI agents.** Free. Open source. MIT licensed.

Archive conversations to long-term memory (MemPalace) and compress context to a 5% buffer for fresh starts.

Skills compound. Prompts don't.

## Install

### Hermes Agent
```bash
git clone https://github.com/wizzleweasel/flush.git ~/.hermes/skills/flush
```

### OpenClaw
```bash
git clone https://github.com/wizzleweasel/flush.git ~/.openclaw/skills/flush
```

### Other Claw Agents
```bash
git clone https://github.com/wizzleweasel/flush.git
# Copy skills/ directory to your agent's skills path
```

## What It Does

| Step | Action | Result |
|------|--------|--------|
| 1 | Archive | Session saved to MemPalace |
| 2 | Compress | Context reduced to ~5% |
| 3 | Restore | Essential context reloaded |
| 4 | Confirm | User notified |

## When to Use

Triggers automatically when:
- Context window > 80% full
- User invokes `/flush`
- Switching between major tasks
- Starting fresh but preserving history

## How It Works

Each skill is a `SKILL.md` file following the [Agent Skills](https://agentskills.io) open standard:

```yaml
---
name: flush
description: "Archive session to MemPalace and compress context. Use when: user invokes /flush; context window is full; starting fresh but preserving history"
---
```

The description tells agents **when** to use the skill. The body provides full workflow — steps, examples, and output format.

Works across **Hermes Agent, OpenClaw, Claude, ChatGPT, Copilot, Cursor, Windsurf** — any tool that supports the Agent Skills standard or MCP.

## Quality

Reviewed against agent skill best practices:

- **Clear triggers** — "Use when:" terms for reliable discovery
- **Agent-first** — Methodology only, no explanations agents already know
- **Concise** — Workflow only, no fluff
- **Output contracts** — Declared steps for composability

## Catalog

1 skill for session management:

| Skill | Description |
|-------|-------------|
| flush | Archive session to MemPalace, compress context to 5% buffer |

## Test

```bash
# Hermes Agent
hermes --test-skill flush

# OpenClaw
openclaw --test-skill flush

# Generic
python scripts/flush.py --test
```

---

**Skills compound. Prompts don't.** Use flush to preserve context while starting fresh.