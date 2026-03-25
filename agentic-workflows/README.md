# Agentic Workflow System

A comprehensive framework for multi-agent development workflows with built-in memory, checkpointing, and repeatable Lobster workflows.

## Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                         Task Receiver                                │
│                    (from Spark/Openclaw)                            │
└───────────────────────────┬─────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────────┐
│                          Task Router                                 │
│              (route to appropriate persona)                         │
└──┬────────────┬──────────────┬──────────────┬──────────────────┬───┘
   │            │              │              │                  │
   ▼            ▼              ▼              ▼                  ▼
┌──────┐   ┌────────┐   ┌────────┐   ┌──────────┐   ┌─────────────┐
│Arch. │   │ Developer│   │   QA   │   │ Security │   │ Performance │
└──┬───┘   └───┬────┘   └───┬────┘   └────┬─────┘   └─────┬───────┘
   │           │            │             │               │
   └───────────┴────────────┴─────────────┴───────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────────┐
│                        Checkpoint System                             │
│              (git-based audit trail)                                │
└─────────────────────────────────────────────────────────────────────┘
```

## Personas

### Architect
- System design and analysis
- Architecture Decision Records (ADRs)
- Design validation

### Developer (RPOLES)
1. **Review** - Analyze requirements
2. **Plan** - Create implementation plan
3. **Outline** - Detailed implementation outline
4. **Locate** - Find dependencies and patterns
5. **Execute** - Implement code
6. **Ship** - Prepare for merge

### QA
- Test planning and generation
- Validation and reporting
- Quality assurance

### Security
- Threat modeling
- Code security review
- Automated scanning
- Security hardening

### Performance
- Performance analysis
- Benchmarking
- Optimization
- Validation

## Lobster Workflows

Repeatable workflow generators for common tasks:

| Workflow | Purpose |
|---|---|
| `lobster-ansible-playbook` | Generate Ansible playbooks |
| `lobster-dockerfile` | Generate Dockerfiles |
| `lobster-cicd` | Generate CI/CD pipelines |
| `lobster-k8s` | Generate Kubernetes manifests |

## Memory Hierarchy

| Level | Location | Lifetime |
|---|---|---|
| Task | `memory/tasks/` | 7 days |
| Design | `memory/designs/` | 1 year |
| Persona | `memory/personas/` | Permanent |
| Knowledge | `memory/knowledge/` | Permanent |
| Context | `memory/context/` | Session |

## Checkpointing

Every phase creates a git checkpoint:

```bash
checkpoint --phase <phase-name> --description "<description>" [--next "<next step>"]
```

Example:
```bash
checkpoint --phase review --description "Requirements analyzed" --next "Proceed to planning"
```

## Skills Catalog

See `skills/SKILLS_CATALOG.md` for the complete list of 34 skills.

## Quick Start

1. Receive task from openclaw spark
2. Task is routed to appropriate persona
3. Persona executes their methodology
4. Checkpoints are created at each phase
5. Results are handed off or merged

## Directory Structure

```
agentic-workflows/
├── memory/               # Memory hierarchy
│   ├── tasks/           # Task-specific memory
│   ├── designs/         # Design documents
│   ├── personas/        # Persona-specific data
│   ├── knowledge/       # Permanent knowledge
│   ├── context/         # Session context
│   └── status/          # Status reports
├── skills/              # Skill definitions
│   ├── personas/        # Persona skills
│   ├── lobster/         # Lobster workflows
│   └── coordination/    # Coordination skills
├── workflows/           # Methodology docs
│   ├── rpoles-methodology.md
│   └── checkpointing.md
└── spark-tasks/         # Inter-spark communication (submodule)
```
