---
name: flush
description: "Archive session to MemPalace and compress context to 5% buffer. Use when: user invokes /flush; needing to archive conversation; context window is full; starting fresh but preserving history; switching tasks and need clean slate"
version: 1.2.0
author: Wicak + Hermes
license: MIT
metadata:
  hermes:
    tags: [memory, session, mempalace, compress, flush]
    related_skills: [recall]
  openclaw:
    tags: [memory, session, archive, compress]
    skill_type: session_management
  claw:
    standard_version: "1.0"
    required_tools: [file_write, shell_exec]
---

# Flush 🔄

Archive the current session to long-term memory (MemPalace) and compress active context to a ~5% buffer for a fresh start.

## How to Use

1. **Archive** — Save session to persistent memory store
2. **Compress** — Reduce context to minimal buffer  
3. **Restore** — Pull essential context for continuity
4. **Confirm** — Notify user of completion

## When Agents Should Auto-Trigger

- Context window > 80% full
- User explicitly requests `/flush`
- Switching between major tasks
- Before long-running operations that need clean state

## Hermes Agent

### Step 1 — Archive to MemPalace

```bash
python ~/.hermes/skills/flush/scripts/flush.py
```

Or via Hermes tools:
```python
from hermes_tools import terminal

terminal(command="/home/runner/workspace/hermes-agent/.venv/bin/python /home/runner/workspace/hermes-data/skills/flush/scripts/flush.py")
```

### Step 2 — Compress Context

Output `/compress` literal text (Hermes gateway intercepts this).

Or via terminal:
```bash
hermes --compress
```

### Step 3 — Restore Context

```bash
python ~/.hermes/skills/recall/scripts/recall.py "last conversation context"
```

## OpenClaw

### Step 1 — Archive Session

```bash
python ~/.openclaw/skills/flush/scripts/flush.py
```

Script should:
1. Locate active session file
2. Pipe into memory store (MemPalace-compatible)
3. Print: `archived N messages -> M memories saved`

### Step 2 — Compress Context

```bash
openclaw --compress-context
```

### Step 3 — Restore Context

```bash
openclaw --recall "last conversation"
```

## Generic Claw Agent

### Required Capabilities
- **File Write** — Save archives
- **Shell Exec** — Run scripts
- **Memory Store** — Persistent storage
- **Context Mgmt** — Compress/reset context

### Minimal Implementation

```python
def flush_skill():
    # 1. Archive
    result = shell_exec("python /path/to/flush.py")
    if result.exit_code != 0:
        return f"Error: {result.stderr}"
    
    # 2. Compress
    compress_context()
    
    # 3. Restore
    context = recall_memory("last conversation")
    
    # 4. Confirm
    return "Memory flushed. Archived to memory store. Context compressed."
```

## Configuration

### Hermes Agent
```yaml
# ~/.hermes/config.yaml
memory:
  store: mempalace
  path: ~/.hermes/mempalace
```

### OpenClaw
```yaml
# ~/.openclaw/config.yaml
session:
  archive: true
  memory_store: mempalace
```

## Scripts

### `scripts/flush.py`

Archive script (MemPalace-compatible):

```python
#!/usr/bin/env python3
"""Archive session to MemPalace."""
import os
import sys
from datetime import datetime

def archive_session(session_path, output_dir):
    os.makedirs(output_dir, exist_ok=True)
    
    if not os.path.exists(session_path):
        print(f"Error: Session not found: {session_path}", file=sys.stderr)
        return False
    
    timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
    output = os.path.join(output_dir, f"archive_{timestamp}.jsonl")
    
    with open(session_path, 'r') as src, open(output, 'w') as dst:
        dst.write(src.read())
    
    print(f"archived session -> {output}")
    return True

if __name__ == "__main__":
    session = sys.argv[1] if len(sys.argv) > 1 else "session.jsonl"
    output = sys.argv[2] if len(sys.argv) > 2 else "./archives"
    success = archive_session(session, output)
    sys.exit(0 if success else 1)
```

## Pitfalls

- ❌ **Hardcoded paths** — Use `CLAW_HOME` env var
- ❌ **Platform assumptions** — Check `CLAW_PLATFORM` (telegram, cli, discord)
- ❌ **Session detection** — Check `CLAW_SESSION_ID`, don't assume recent = active
- ✅ **Error handling** — Always check exit codes
- ✅ **Stderr for errors** — Keep error streams separate

## Testing

```bash
# Hermes Agent
hermes --test-skill flush

# OpenClaw
openclaw --test-skill flush

# Generic
python scripts/flush.py --test
```

---

**Skills compound. Prompts don't.** Apply this skill whenever you need to preserve context while starting fresh.