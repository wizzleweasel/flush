<p align="center">
  <img src="https://em-content.zobj.net/source/apple/391/clockwise-vertical-arrows_1f503.png" width="120" />
</p>

<h1 align="center">flush</h1>

<p align="center">
  <strong>archive session, compress context, keep memory</strong>
</p>

<p align="center">
  <a href="https://github.com/wizzleweasel/flush/stargazers"><img src="https://img.shields.io/github/stars/wizzleweasel/flush?style=flat&color=yellow" alt="Stars"></a>
  <a href="https://github.com/wizzleweasel/flush/commits/main"><img src="https://img.shields.io/github/last-commit/wizzleweasel/flush?style=flat" alt="Last Commit"></a>
  <a href="LICENSE"><img src="https://img.shields.io/github/license/wizzleweasel/flush?style=flat" alt="License"></a>
</p>

<p align="center">
  <a href="#before--after">Before/After</a> •
  <a href="#install">Install</a> •
  <a href="#when-to-use">When to Use</a> •
  <a href="#benchmarks">Benchmarks</a>
</p>

<p align="center">
  <strong>🦞 Flush Ecosystem</strong> &nbsp;·&nbsp;
  <strong>flush</strong> <em>archive & compress</em> <sub>(you are here)</sub> &nbsp;·&nbsp;
  <a href="https://github.com/wizzleweasel/throw-rock">throw-rock</a> <em>throw compressed</em> &nbsp;·&nbsp;
  <a href="https://github.com/wizzleweasel/pierced-tongue">pierced-tongue</a> <em>transport layer</em>
</p>

---

Archive session to MemPalace, then compress context to 5% buffer. Keep memory, start fresh.

**Works with:** Hermes Agent ✅ | OpenClaw ✅ | Other Claw Agents ✅

Based on the observation that session archival + context compression dramatically improves agent performance. So we made it a one-line install.

## Before / After

<table>
<tr>
<td width="50%">

### 🗣️ Without Flush (800+ tokens)

> Agent bogs down with huge context. Slow responses. Can't remember old stuff. User repeats everything. Agent confused.

</td>
<td width="50%">

### 🔄 With Flush (context ~5%)

> Context compressed. Memory archived. Agent fast again. Old stuff in MemPalace. Fresh start.

</td>
</tr>
<tr>
<td>

### 🗣️ Normal Session

> "I've been talking to you for hours and you're getting slow. Can you archive our conversation and start fresh while keeping the important stuff?"

</td>
<td>

### 🔄 Flush Mode

> `/flush` → archived 73 messages → compressed to 5% → go fast again.

</td>
</tr>
</table>

**Same agent. 95% less context. Speed come back.**

## Install

Pick your agent. One command. Done.

| Agent | Install |
|-------|---------|
| **Hermes Agent** | `git clone https://github.com/wizzleweasel/flush.git ~/.hermes/skills/flush` |
| **OpenClaw** | `git clone https://github.com/wizzleweasel/flush.git ~/.openclaw/skills/flush` |
| **Claude Code** | `git clone https://github.com/wizzleweasel/flush.git skills/` |
| **Any other** | `git clone https://github.com/wizzleweasel/flush.git` |

Install once. Use `/flush` in any session after that. One command. That it.

## When to Use

Triggers automatically when:
- Context window > 80% full
- User invokes `/flush`
- Switching between major tasks  
- Starting fresh but preserving history

## Benchmarks

| Scenario | Before Flush | After Flush | Savings |
|----------|--------------|-------------|---------|
| Long session | ~15,000 tokens | ~750 tokens | **95%** |
| Response speed | ~5 sec | ~1 sec | **5x faster** |
| Memory recall | Can't find old stuff | Search MemPalace | **Perfect** |

```
┌─────────────────────────────────────┐
│  CONTEXT REDUCTION     ████████ 95% │
│  SPEED INCREASE        ████████ 5x  │
│  MEMORY RETENTION     ████████ 100%│
│  VIBES                 ████████ OOG │
└─────────────────────────────────────┘
```

## How It Works

Three steps. Fast.

1. **Archive** — Save session to MemPalace (long-term memory)
2. **Compress** — Reduce context to ~5% buffer
3. **Restore** — Pull essential context for continuity

### Hermes Agent
```bash
# Step 1: Archive
python ~/.hermes/skills/flush/scripts/flush.py

# Step 2: Compress  
hermes --compress  # or output /compress

# Step 3: Restore
python ~/.hermes/skills/recall/scripts/recall.py "last context"
```

### OpenClaw
```bash
# Step 1: Archive
python ~/.openclaw/skills/flush/scripts/flush.py

# Step 2: Compress
openclaw --compress-context

# Step 3: Restore
openclaw --recall "last context"
```

## Testing

```bash
# Smoke test
python scripts/flush.py --test

# Hermes Agent
hermes --test-skill flush

# OpenClaw
openclaw --test-skill flush
```

---

**Skills compound. Prompts don't.** Flush to archive memory, compress context, go fast again. 🔄