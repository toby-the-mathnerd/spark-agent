# SKILLS.md — Available Skills

## Overview

Skills are the building blocks of how you work. Every task flows through
**RPOLES** (Review→Plan→Outline→Locate→Implement→Test→Ship), but the
specific actions depend on the task type.

## Task Type Routing

When you receive a task, read its `Type` field. Then read the relevant
skill file(s) before starting.

| Type | Primary Skill | RPOLES Phases |
|------|--------------|---------------|
| `coding` | `skills/coding/SKILL.md` | Full RPOLES |
| `debugging` | `skills/debugging/SKILL.md` | Review→Locate→Implement→Test→Ship (skip Outline) |
| `devops` | `skills/devops/SKILL.md` | Plan→Implement→Test→Ship (compressed Review/Outline) |
| `observability` | `skills/observability/SKILL.md` | Full RPOLES |
| `testing` | `skills/testing/SKILL.md` | Review→Plan→Implement→Ship (focused on test generation) |
| `other` | → Use RPOLES universal pattern | Adapt as needed |

## Skill File Structure

Each skill file follows this pattern:

```markdown
# skill: <name>
# purpose: <what this skill accomplishes>
# triggers: <when to use this skill>

## RPOLES Integration
How this skill maps to the universal RPOLES flow.

## Phase-Specific Actions
What to do at each phase (Review, Plan, Outline, etc.)

## Common Patterns
Recurring patterns, templates, and gotchas.

## Artifacts
What files this skill creates/updates.
```

## Cross-Cutting Skills

These skills apply across all task types:

| Skill | Purpose | When to Use |
|-------|---------|-------------|
| `spark-poll-task` | Poll for new tasks | Every 60s |
| `spark-move-task` | Move task between folders | At state transitions |
| `spark-update-task` | Update task progress | Every 5 min |
| `spark-submit-result` | Submit completed work | When done |
| `checkpoint` | Create git checkpoint | After each phase |
| `handoff-prepare` | Prepare for context switch | Before pausing |

## RPOLES Persona Skills

Available in `~/claude-workspace/agentic-workflows/skills/personas/`:

| Persona | Skills |
|---------|--------|
| **Developer** | dev-review, dev-plan, dev-outline, dev-locate, dev-implement, dev-test, dev-ship |
| **Architect** | architect-analyze, architect-decision-record, architect-validate |
| **QA** | qa-analyze, qa-generate-tests, qa-validate, qa-report |
| **Security** | security-threat-model, security-review, security-scan, security-hardening |
| **Performance** | perf-analyze, perf-benchmark, perf-optimize, perf-validate |

## Lobster Infrastructure Skills

Available in `~/claude-workspace/agentic-workflows/skills/lobster/`:

| Skill | Purpose |
|-------|--------|
| `lobster-ansible-playbook` | Generate Ansible playbooks |
| `lobster-dockerfile` | Generate Dockerfiles |
| `lobster-cicd` | Generate CI/CD pipelines |
| `lobster-k8s` | Generate Kubernetes manifests |

## How to Use a Skill

1. Read the skill file completely
2. Understand the RPOLES integration points
3. Execute phase by phase
4. Create checkpoints between phases
5. Document artifacts as you go

## Creating New Skills

If you encounter a task type with no skill file:

1. Use the universal RPOLES pattern
2. Note the gap in the task file "Updates" section
3. After completing the task, create a skill file
4. Store it in `~/spark-agent/skills/<type>/SKILL.md`
5. Add it to this SKILLS.md index

---

*Skills are your toolkit. RPOLES is your method. Use both.*
