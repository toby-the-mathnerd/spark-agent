# Git Checkpointing Methodology

Every agent operation must checkpoint progress to git. This provides:
- Full audit trail of agent actions
- Ability to rollback any change
- Clear handoff points between agents
- Memory hierarchy anchored in git history

## Checkpoint Triggers

1. **Phase Complete:** Each RPOLES phase creates a checkpoint
2. **File Boundaries:** Major file changes create checkpoints
3. **Before Risky Operations:** Always checkpoint before destructive changes
4. **Handoff Points:** Before passing to another agent/persona

## Checkpoint Format

```bash
git add <affected-files>
git commit -m "[<agent>] <phase>: <concise description>

<details about what was done>

Agent: <agent-name>
Task: <task-id-or-description>
Next: <what comes next>"
```

## Checkpoint Categories

- `[rpoles-review]` - Review phase complete
- `[rpoles-plan]` - Plan approved
- `[rpoles-outline]` - Outline created
- `[rpoles-locate]` - Dependencies mapped
- `[rpoles-execute]` - Implementation complete
- `[rpoles-ship]` - Ready for merge
- `[persona:<name>]` - Cross-persona work
