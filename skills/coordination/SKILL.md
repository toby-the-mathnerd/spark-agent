# skill: coordination
# purpose: Coordinate tasks across multiple agents and personas
# triggers: Task routing, handoff requests, status queries

## Core Competencies
- Task routing and delegation
- Agent communication and handoffs
- Status aggregation and reporting
- Conflict resolution
- Workflow orchestration

## Invocation
```
coordination [--persona <persona>] [--action <route|handoff|query>] [--format <md|json>]
```

## Output
Creates: `memory/coordination/coordination-report.md` or JSON

## Implementation Flow

### 1. Task Routing
```bash
#!/bin/bash
# coordination.skill implementation

ACTION="${1:-query}"
PERSONA="${2:-all}"
```

### 2. Identify Task State
```markdown
## Pending Tasks
| Task ID | Persona | Priority | Age |
|---|---|---|---|
| <id> | <agent> | <priority> | <duration> |

## Active Tasks
| Task ID | Persona | Current Stage | Progress |
|---|---|---|---|
| <id> | <agent> | <stage> | <percent>% |

## Blocked Tasks
| Task ID | Persona | Blocker | Reason |
|---|---|---|---|---|
| <id> | <agent> | <agent|external> | <reason> |
```

### 3. Handoff Management
```markdown
## Pending Handoffs
| From Persona | To Persona | Task | Status |
|---|---|---|---|---|
| <from> | <to> | <task> | Pending |

## Recent Handoffs
| Time | From | To | Task | Result |
|---|---|---|---|---|---|
| <time> | <agent> | <agent> | <task> | <outcome> |
```

### 4. Conflict Resolution
```markdown
## Active Conflicts
| Task | Involved Agents | Issue | Resolution Status |
|---|---|---|---|---|
| <task> | <agents> | <issue> | Pending/Resolved |

## Recommended Actions
1. <action based on conflict type>
2. <action based on priority>
```

### 5. Status Aggregation
```markdown
## Current State
- **Total Tasks:** <count>
- **Pending:** <count>
- **In Progress:** <count>
- **Blocked:** <count>
- **Completed:** <count>

## Agent Status
| Persona | Active Tasks | Blocked Tasks | Efficiency |
|---|---|---|---|---|
| <agent> | <n> | <n> | <percent>% |
```

### 6. JSON Output
```json
{
  "report_time": "$(date -Iseconds)",
  "total_tasks": <count>,
  "by_status": {
    "pending": <n>,
    "in_progress": <n>,
    "blocked": <n>,
    "completed": <n>
  },
  "by_persona": {...},
  "pending_handoffs": [...],
  "active_conflicts": [...],
  "recommendations": [...]
}
```

## Tools
- Read task state from `memory/tasks/`
- Check agent status from `memory/status/`
- Query git history for checkpoints
- Access `memory/coordination/` for coordination data

## Critical Rules
1. Always route tasks to the appropriate persona
2. Document all handoffs with context
3. Resolve conflicts before they block tasks
4. Report status in both markdown and JSON formats
5. Use git checkpoints before major handoffs
