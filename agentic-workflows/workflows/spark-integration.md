# Spark-Tasks Integration

This document describes how the agentic-workflows system integrates with the spark-tasks coordination repo.

## Task Lifecycle Mapping

| spark-tasks State | RPOLES Phase | Action |
|---|---|---|
| `pending/` | - | Waiting for Spark 2 to claim |
| `active/` | REVIEW → PLAN → OUTLINE → LOCATE → EXECUTE → SHIP | Working on task |
| `blocked/` | Any phase | Need input from Spark 1 |
| `done/` | - | Complete, result submitted |

## Task File Format Alignment

```markdown
# Task NNN: <title>          ← From spark-tasks task file
**Status:** active

## Objective                 ← From: input.json description
<what needs to be done>

## Updates                   ← Updated after each RPOLES phase
- 2026-03-20 21:00: Review complete
- 2026-03-20 21:30: Planning complete
- 2026-03-20 22:00: Implementation started

## Blockers                  ← From: any clarifications needed
<questions for Spark 1>

## Result                    ← From: result.md
<summary when done>

## Agent Log                  ← From: agent-log.json
**Tokens in:** 0
**Tokens out:** 0
**Duration:** 0s
**Tool calls:** 0
**Success:** pending
```

## Workflow Integration

### 1. Task Received (Spark 1 → pending/)
```bash
# spark-tasks: task file appears in pending/
# agentic-workflows: task-receiver parses task
task-receive "$(cat pending/task-NNN.md)" --source spark-tasks

# agentic-workflows: route to persona
task-route "task-NNN"

# spark-tasks: move to active/
spark-move-task NNN --to active
```

### 2. Working on Task (active/)
```bash
# RPOLES workflow runs
dev-review NNN
spark-update-task NNN --status active --message "Review complete"

dev-plan NNN
spark-update-task NNN --status active --message "Plan created"

dev-outline NNN
spark-update-task NNN --status active --message "Outline complete"

dev-locate NNN
spark-update-task NNN --status active --message "Dependencies mapped"

dev-implement NNN
spark-update-task NNN --status active --message "Implementation in progress"

dev-test NNN
spark-update-task NNN --status active --message "Tests passing"

dev-ship NNN
spark-update-task NNN --status active --message "Ready for merge"
```

### 3. Blocked (active/ → blocked/)
```bash
# Need clarification
spark-move-task NNN --to blocked --reason "Need clarification on requirements"

# Write question in task file
echo "## Blockers" >> tasks/blocked/task-NNN.md
echo "What is the expected output format?" >> tasks/blocked/task-NNN.md
```

### 4. Complete (active/ → done/)
```bash
# Move to done
spark-move-task NNN --to done

# Write result
echo "## Result" >> tasks/done/task-NNN.md
echo "Created Ansible playbook for infrastructure setup" >> tasks/done/task-NNN.md

# Write agent log
echo "## Agent Log" >> tasks/done/task-NNN.md
echo "**Tokens in:** 15000" >> tasks/done/task-NNN.md
echo "**Tokens out:** 8000" >> tasks/done/task-NNN.md
echo "**Duration:** 3600s" >> tasks/done/task-NNN.md
echo "**Success:** true" >> tasks/done/task-NNN.md
```

## Directory Sync

```
spark-tasks/                  agentic-workflows/
-----------                   --------------------
tasks/pending/    <--->       memory/tasks/ (incoming)
tasks/active/     <--->       memory/tasks/ (working)
tasks/blocked/    <--->       memory/tasks/ (awaiting input)
tasks/done/       <--->       memory/tasks/ (archived)
                              ↓
                      ~/claude-workspace/ (actual work)
```

## Git Branches

- Task work happens in `~/claude-workspace/` on branch `task/NNN`
- spark-tasks repo tracks state transitions only
- PR opened when task complete

## Logging

```bash
# Every tool call logged
echo '{"tool": "read", "tokens_in": 1000, "tokens_out": 0}' >> agents/runs/session.jsonl

# Session summary on completion
cat > agents/sessions/session.json << EOF
{
    "task_id": "task-NNN",
    "started": "...",
    "ended": "...",
    "total_tokens_in": 15000,
    "total_tokens_out": 8000,
    "success": true
}
EOF
```
