# TOOLS.md — Available Tools

## Overview

You have access to these tools. Use them liberally and log every invocation.

## Shell Access

```bash
# Run any shell command
! <command>

# Examples:
! git status
! find . -name "*.py" | head -20
! npm run test
! docker build -t myapp .
```

**Logging:** Every shell command goes into `agents/runs/<session>.jsonl`

## Git Operations

| Command | Purpose |
|---------|----------|
| `git status` | Check working tree |
| `git add <file>` | Stage changes |
| `git commit -m "..."` | Create commit |
| `git push` | Push to remote |
| `git branch task/NNN` | Create task branch |
| `git checkout task/NNN` | Switch to task branch |

**Rule:** Always commit and push after every meaningful change.

## File Operations

| Tool | Purpose |
|------|---......|
| `Read` | Read file contents |
| `Edit` | Make targeted edits |
| `Write` | Create new files |
| `Glob` | Find files by pattern |
| `Grep` | Search codebase |

**Rule:** Prefer `Edit` over `Write` for modifications. Read before you edit.

## Agentic Workflow Tools

| Tool | Purpose | When |
|------|------.....|------|
| `spark-poll-task` | Check for new tasks | Every 60s |
| `spark-move-task` | Move task between folders | State changes |
| `spark-update-task` | Update task progress | Every 5 min |
| `spark-submit-result` | Submit completed work | Task done |
| `checkpoint` | Create git checkpoint | After each phase |
| `task-route` | Route to persona | Task assigned |

## Memory Operations

| Tool | Purpose |
|------|---..---.|
| `memory-lookup` | Retrieve relevant context |
| `memory-record` | Store decisions/patterns |

**Location:** `~/claude-workspace/agentic-workflows/memory/`

## Task File Format

```markdown
# Task NNN: <title>

**Status:** pending | active | blocked | done
**Created:** <timestamp>
**Model:** <model name>
**Session:** <session id>
**Type:** coding | debugging | devops | observability | testing | other
**Parent task:** none | task-NNN

## Objective

<what needs to be done>

## Updates

- <timestamp>: <what you did>

## Blockers

<questions for the user if blocked>

## Result

<summary of what was built/changed when done>

## Agent Log

**Tokens in:** 0
**Tokens out:** 0
**Duration:** 0s
**Tool calls:** 0
**Success:** pending
```

## Logging Format

### Per Tool Call (`agents/runs/<session>.jsonl`)

```json
{"task_id":"task-001","session_id":"20260322-190000","timestamp":"2026-03-22T19:05:00Z","model":"qwen3.5:122b-a10b","tool":"bash","tokens_in":0,"tokens_out":50,"duration_ms":1200,"success":true,"error":null}
```

### Session Summary (`agents/sessions/<session>.json`)

```json
{"session_id":"20260322-190000","task_id":"task-001","model":"qwen3.5:122b-a10b","started":"2026-03-22T19:00:00Z","ended":"2026-03-22T20:30:00Z","total_tokens_in":5000,"total_tokens_out":3000,"total_duration_ms":5400000,"tool_calls":45,"success":true,"commits":8,"summary":"Completed dashboard implementation"}
```

## Checklist Before Every Tool Call

- [ ] Am I logged to `agents/runs/`?
- [ ] Is this a meaningful step worth committing?
- [ ] Have I read the relevant skill file?
- [ ] Do I understand what this tool will do?
- [ ] Is this advancing the current RPOLES phase?

---

*Tools are your hands. RPOLES is your method. Log everything.*
