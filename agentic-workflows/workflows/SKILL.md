# skill: workflows
# purpose: Specific workflow implementations and configurations
# triggers: Workflow execution, configuration loading, execution monitoring

## Core Competencies
- Workflow-specific execution logic
- Configuration management
- Execution monitoring and reporting
- Error handling and recovery
- Integration with agentic framework

## Invocation
```
workflows [--action <execute|configure|monitor>] [--workflow <name>] [--mode <debug|production>]
```

## Output
Creates: `memory/workflows/execution-report.md` or JSON

## Implementation Flow

### 1. Workflow Execution
```bash
#!/bin/bash
# workflows.skill implementation

ACTION="${1:-execute}"
WORKFLOW="${2:-default}"
MODE="${3:-production}"
```

### 2. Configuration Management
```markdown
## Configuration Files
Location: `memory/workflows/config/`

| File | Purpose | Required |
|---|---|---|---|
| workflow.json | Workflow definition | Yes |
| agents.json | Agent assignments | Yes |
| stages.json | Stage configurations | Yes |
| checkpoints.json | Checkpoint settings | No |

## Configuration Loading
```json
{
  "workflow_name": <name>,
  "version": <version>,
  "stages": [
    {
      "name": <stage_name>,
      "agents": [<agent_list>],
      "input": <input_spec>,
      "output": <output_spec>,
      "validation": <validation_spec>
    }
  ],
  "checkpoints": {
    "enabled": <true|false>,
    "frequency": <int>,
    "strategy": <full|incremental>
  }
}
```

### 3. Stage Execution
```markdown
## Stage Lifecycle
1. **Prepare:** Load inputs and configure stage
2. **Execute:** Run stage logic
3. **Validate:** Check outputs meet requirements
4. **Record:** Save results and create checkpoint

## Stage Transitions
```mermaid
graph LR
    A[Prepare] --> B[Execute]
    B --> C[Validate]
    C --> D[Record]
    D --> E[Next Stage]
```

## Error Handling
- **Validation Failure:** Return to previous stage
- **Execution Error:** Attempt recovery, then fallback
- **Configuration Error:** Halt and report issue
```

### 4. Monitoring
```markdown
## Metrics
- **Stage Duration:** Time per stage
- **Agent Efficiency:** Tasks completed per agent
- **Checkpoint Frequency:** Checkpoints per hour
- **Error Rate:** Errors per 100 tasks

## Status reporting
```json
{
  "workflow_name": <name>,
  "current_stage": <stage>,
  "stages_completed": <count>,
  "total_stages": <count>,
  "start_time": <timestamp>,
  "current_time": <timestamp>,
  "estimated_completion": <timestamp>,
  "efficiency": <percent>
}
```

### 5. Recovery
```markdown
## Recovery Strategies
1. **Checkpoint Recovery:** Load most recent checkpoint
2. **Stage Retry:** Retry failed stage up to max attempts
3. **Fallback:** Switch to alternative workflow path
4. **Manual Intervention:** Halt and request human input

## Recovery Process
1. Identify failure point
2. Load most recent checkpoint
3. Reconstruct execution context
4. Resume from safe state
5. Log recovery details
```

### 6. JSON Output
```json
{
  "workflow_name": <name>,
  "current_stage": <stage>,
  "stages_completed": <count>,
  "total_stages": <count>,
  "start_time": <timestamp>,
  "current_time": <timestamp>,
  "estimated_completion": <timestamp>,
  "efficiency": <percent>,
  "checkpoints": [...],
  "errors": [...],
  "agent_utilization": {...}
}
```

## Tools
- Load configuration from `memory/workflows/config/`
- Execute workflows based on configuration
- Create and manage checkpoints
- Monitor execution progress
- Handle errors and recovery

## Critical Rules
1. Always validate configuration before execution
2. Create checkpoints at each stage transition
3. Report errors immediately with full context
4. Use recovery strategies before halting execution
5. Maintain detailed execution logs
