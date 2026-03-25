# skill: agentic-workflows
# purpose: Core agentic workflow patterns and capabilities
# triggers: Workflow execution, checkpointing, task coordination

## Core Competencies
- Workflow orchestration across multiple agents
- Checkpoint management and recovery
- Task delegation and routing
- Status tracking and reporting
- Memory management and persistence

## Invocation
```
agentic-workflows [--action <execute|checkpoint|recovery>] [--workflow <name>]
```

## Output
Creates: `memory/workflows/workflow-execution.md` or JSON

## Implementation Flow

### 1. Workflow Execution
```bash
#!/bin/bash
# agentic-workflows.skill implementation

ACTION="${1:-execute}"
WORKFLOW="${2:-default}"
```

### 2. Memory Management
```markdown
## Memory Hierarchy
1. **Short-term:** Active task context
2. **Medium-term:** Task metadata and status
3. **Long-term:** Agent capabilities and preferences
4. **Permanent:** Git checkpoints and history

## Memory Access Patterns
| Type | Location | TTL | Access Pattern |
|---|---|---|---|
| Active | memory/tasks/current/ | Task duration | Read/Write |
| Metadata | memory/tasks/history/ | 30 days | Read |
| Capabilities | memory/personas/ | Permanent | Read |
| Checkpoints | memory/checkpoints/ | Permanent | Read/Write |
```

### 3. Checkpoint Management
```markdown
## Checkpoint Strategy
- **Before major transitions** (route, handoff, state change)
- **After significant completion** (阶段性完成)
- **On error or interruption**
- **Periodically during long workflows**

## Checkpoint Contents
- Current task state
- Agent context and working memory
- Pending operations
- Error state for recovery

## Recovery Process
1. Load most recent checkpoint
2. Reconstruct agent state
3. Resume from last safe state
4. Reconcile with current task context
```

### 4. Task Routing
```markdown
## Routing Table
| Task Type | Primary Agent | Backup Agent | Priority |
|---|---|---|---|---|
| coding | developer | architect | medium |
| testing | qa | developer | high |
| coordination | orchestrator | all | critical |
| devops | devops | architect | high |

## Routing Priority
1. **Critical:** System failures, security issues
2. **High:** Testing, deployment
3. **Medium:** Development, planning
4. **Low:** Documentation, cleanup
```

### 5. State Transition
```markdown
## Valid State Transitions
```
pending → active → reviewing → completed
pending → blocked → (retry/resolve) → active
active → blocked → (retry/resolve) → active
```

## State Persistence
```json
{
  "current_state": <state>,
  "previous_states": [...],
  "transitions": [
    {"from": <from>, "to": <to>, "timestamp": <time>, "agent": <agent>}
  ],
  "metadata": {...}
}
```

### 6. Workflow Patterns
```markdown
## Common Patterns
1. **Linear:** Sequential stages with clear handoffs
2. **Branching:** Parallel execution with merge points
3. **Feedback:** Iterative refinement with review loops
4. **Fallback:** Error recovery with alternative paths
```

### 7. JSON Output
```json
{
  "workflow_name": <name>,
  "current_state": <state>,
  "active_agents": [...],
  "pending_tasks": [...],
  "completed_stages": [...],
  "checkpoints": [...],
  "memory_usage": {...},
  "efficiency_metrics": {...}
}
```

## Tools
- Read/write to `memory/` hierarchy
- Create and manage git checkpoints
- Query task state from `memory/tasks/`
- Access agent capabilities from `memory/personas/`

## Critical Rules
1. Always create checkpoints before state transitions
2. Document all routing decisions
3. Preserve context during handoffs
4. Report status in both markdown and JSON formats
5. Use git for permanent state management
