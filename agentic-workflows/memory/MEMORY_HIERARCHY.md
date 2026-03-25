# Memory Hierarchy System

This directory structure implements a multi-level memory system for agentic workflows.

## Memory Levels

### Level 1: Task Memory (Ephemeral)
**Location:** `memory/tasks/<task-id>/`
**Lifetime:** Task duration + 7 days
**Contents:**
- `input.json` - Original task specification
- `review.md` - Requirements analysis
- `plan.md` - Implementation plan
- `outline.md` - Detailed outline
- `dependencies.md` - Dependency map
- `test-report.md` - Test results
- `handoff.md` - Handoff documentation
- `routing.json` - Task routing info
- `.status` - Current status
- `.assigned_to` - Current agent/persona
- `.current_phase` - Current RPOLES phase

### Level 2: Design Memory (Semi-Persistent)
**Location:** `memory/designs/<task-id>/`
**Lifetime:** 1 year or until feature deprecated
**Contents:**
- `design.md` - Architecture design
- `validation.md` - Architectural validation
- `threat-model.md` - Security threat model
- `perf-analysis.md` - Performance analysis

### Level 3: Persona Memory (Persistent)
**Location:** `memory/personas/<persona>/`
**Lifetime:** Permanent
**Contents:**
- `inbox/` - Incoming tasks
- `handoffs/` - Received handoffs
- `completed/` - Completed work
- `patterns.md` - Known patterns
- `preferences.md` - Persona preferences

### Level 4: Knowledge Memory (Permanent)
**Location:** `memory/knowledge/`
**Lifetime:** Permanent
**Contents:**
- `patterns/` - Code patterns
- `decisions/` - ADRs and decisions
- `lessons/` - Lessons learned
- `templates/` - Reusable templates

### Level 5: Context Memory (Session)
**Location:** `memory/context/`
**Lifetime:** Current session
**Contents:**
- `current_task` - Currently active task
- `active_agents` - Running agents
- `environment` - Environment state

## Memory Operations

### Lookup
```bash
# Lookup task memory
memory-lookup --task <task-id> [--level <1-5>]

# Lookup by keyword
memory-lookup --keyword <keyword> [--category <category>]

# Lookup related tasks
memory-lookup --related <task-id>
```

### Record
```bash
# Record decision
memory-record --category decisions --tags "arch,auth" \
    --content "Using JWT for session management"

# Record pattern
memory-record --category patterns --tags "python,api" \
    --content "FastAPI endpoint pattern"
```

### Archive
```bash
# Archive completed task
memory-archive <task-id>

# Move to cold storage
memory-archive --cold <task-id>
```

## Memory Retention Policy

| Level | Retention | Action After |
|-------|---|---|
| Task | 7 days | Move to cold storage |
| Design | 1 year | Archive or delete |
| Persona | Permanent | Keep |
| Knowledge | Permanent | Review quarterly |
| Context | Session | Delete on exit |
