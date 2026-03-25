# Skills Catalog

Complete inventory of skills needed for the agentic workflow system.

## Core Infrastructure Skills

### 1. `checkpoint`
- **Purpose:** Create git checkpoint with proper commit message
- **Trigger:** Before any significant change, after each phase
- **Input:** Changes to commit, phase name, description
- **Output:** Committed checkpoint with metadata

### 2. `task-receiver`
- **Purpose:** Parse incoming task from openclaw spark
- **Trigger:** New task arrives
- **Input:** Raw task specification
- **Output:** Structured task with requirements, constraints, priority

### 3. `task-router`
- **Purpose:** Route tasks to appropriate persona
- **Trigger:** Task parsed and categorized
- **Input:** Structured task
- **Output:** Assigned persona + priority queue position

### 4. `memory-lookup`
- **Purpose:** Retrieve relevant context from memory hierarchy
- **Trigger:** Task starts or needs context
- **Input:** Task type, keywords, affected components
- **Output:** Relevant history, patterns, decisions

### 5. `memory-record`
- **Purpose:** Store decisions and patterns for future use
- **Trigger:** Important decision made, pattern identified
- **Input:** Decision/context, category, tags
- **Output:** Stored memory entry

## Persona: Architect Skills

### 6. `architect-analyze`
- **Purpose:** High-level system analysis and design
- **Trigger:** New feature or major change
- **Input:** Requirements, constraints
- **Output:** System design document, component relationships

### 7. `architect-decision-record`
- **Purpose:** Create ADR (Architecture Decision Record)
- **Trigger:** Major architectural decision made
- **Input:** Decision, alternatives considered, rationale
- **Output:** ADR document

### 8. `architect-validate`
- **Purpose:** Validate implementation against architecture
- **Trigger:** Before shipping
- **Input:** Implementation, design document
- **Output:** Alignment report, gaps identified

## Persona: Developer Skills (RPOLES)

### 9. `dev-review`
- **Purpose:** Analyze and clarify task requirements
- **Trigger:** Task assigned to Developer
- **Input:** Task specification
- **Output:** Requirements summary, clarifying questions

### 10. `dev-plan`
- **Purpose:** Create implementation plan
- **Trigger:** Requirements clear
- **Input:** Requirements, system context
- **Output:** Step-by-step implementation plan

### 11. `dev-outline`
- **Purpose:** Create detailed implementation outline
- **Trigger:** Plan approved
- **Input:** Implementation plan, affected files
- **Output:** File-by-file implementation outline

### 12. `dev-locate`
- **Purpose:** Find dependencies and existing patterns
- **Trigger:** Outline created
- **Input:** Outline, file list
- **Output:** Dependency map, pattern references

### 13. `dev-implement`
- **Purpose:** Write actual code
- **Trigger:** All prerequisites complete
- **Input:** Outline, dependencies, patterns
- **Output:** Implemented code

### 14. `dev-test`
- **Purpose:** Create/update tests
- **Trigger:** Code implemented
- **Input:** Code, requirements
- **Output:** Test coverage

### 15. `dev-ship`
- **Purpose:** Prepare for merge/handoff
- **Trigger:** Tests pass
- **Input:** Code, tests, changelog
- **Output:** Staged changes, PR ready

## Persona: QA Skills

### 16. `qa-analyze`
- **Purpose:** Analyze requirements for test coverage
- **Trigger:** Requirements received
- **Input:** Requirements, specifications
- **Output:** Test plan, coverage map

### 17. `qa-generate-tests`
- **Purpose:** Create test cases
- **Trigger:** Test plan approved
- **Input:** Test plan, code
- **Output:** Test suite

### 18. `qa-validate`
- **Purpose:** Run validation suite
- **Trigger:** Code ready for QA
- **Input:** Code, test suite
- **Output:** Test results, defects

### 19. `qa-report`
- **Purpose:** Generate quality report
- **Trigger:** Validation complete
- **Input:** Test results, coverage
- **Output:** Quality report, recommendations

## Persona: Security Skills

### 20. `security-threat-model`
- **Purpose:** Create threat model for changes
- **Trigger:** New feature or change
- **Input:** Design, data flows, inputs
- **Output:** Threat model, risk assessment

### 21. `security-review`
- **Purpose:** Code security review
- **Trigger:** Code ready for review
- **Input:** Code, dependencies
- **Output:** Security findings, recommendations

### 22. `security-scan`
- **Purpose:** Run automated security scans
- **Trigger:** Before ship
- **Input:** Code, dependencies, configs
- **Output:** Scan results, vulnerabilities

### 23. `security-hardening`
- **Purpose:** Apply security improvements
- **Trigger:** Issues identified
- **Input:** Findings, code
- **Output:** Hardened code

## Persona: Performance Skills

### 24. `perf-analyze`
- **Purpose:** Analyze performance characteristics
- **Trigger:** New feature or change
- **Input:** Code, expected load, requirements
- **Output:** Performance analysis, bottlenecks

### 25. `perf-benchmark`
- **Purpose:** Create and run benchmarks
- **Trigger:** Code ready
- **Input:** Code, baseline
- **Output:** Benchmark results

### 26. `perf-optimize`
- **Purpose:** Apply performance improvements
- **Trigger:** Bottlenecks identified
- **Input:** Code, analysis
- **Output:** Optimized code

### 27. `perf-validate`
- **Purpose:** Validate performance meets requirements
- **Trigger:** Optimization complete
- **Input:** Code, requirements, benchmarks
- **Output:** Performance validation report

## Lobster Workflow Skills

### 28. `lobster-ansible-playbook`
- **Purpose:** Generate Ansible playbook
- **Trigger:** Infrastructure task received
- **Input:** Target hosts, desired state, variables
- **Output:** Ansible playbook + inventory

### 29. `lobster-dockerfile`
- **Purpose:** Generate Dockerfile
- **Trigger:** Containerization task
- **Input:** Base image, dependencies, app type
- **Output:** Dockerfile + .dockerignore

### 30. `lobster-cicd`
- **Purpose:** Generate CI/CD pipeline
- **Trigger:** Pipeline task
- **Input:** Language, tests, deployment target
- **Output:** Pipeline configuration

### 31. `lobster-k8s`
- **Purpose:** Generate Kubernetes manifests
- **Trigger:** K8s deployment task
- **Input:** Service spec, replicas, resources
- **Output:** K8s manifests

## Coordination Skills

### 32. `handoff-prepare`
- **Purpose:** Prepare work for handoff between agents
- **Trigger:** Agent needs to pass to another
- **Input:** Current state, next steps
- **Output:** Handoff package

### 33. `conflict-resolve`
- **Purpose:** Resolve conflicts between agent actions
- **Trigger:** Conflict detected
- **Input:** Conflicting changes
- **Output:** Resolution plan

### 34. `status-aggregate`
- **Purpose:** Aggregate status across agents
- **Trigger:** Status query
- **Input:** All agent states
- **Output:** Unified status report

## Spark Agent Task-Type Skills

The spark-agent system uses task-type skills that encode RPOLES as the universal
methodology. Each skill maps to a task type and describes how to apply RPOLES.

### 35. `coding` (spark-agent)
- **Purpose:** Implement new features and code changes
- **RPOLES:** Full flow (Review→Plan→Outline→Locate→Implement→Test→Ship)
- **Location:** `~/spark-agent/skills/coding/SKILL.md`
- **Output:** Code on task branch, PR open

### 36. `debugging` (spark-agent)
- **Purpose:** Find and fix bugs
- **RPOLES:** Compressed (Review→Plan→Locate→Implement→Test→Ship, skip Outline)
- **Location:** `~/spark-agent/skills/debugging/SKILL.md`
- **Output:** Bug fixed, regression test added

### 37. `devops` (spark-agent)
- **Purpose:** Infrastructure, deployment, system configuration
- **RPOLES:** Compressed (Review→Plan→Locate→Implement→Test→Ship)
- **Location:** `~/spark-agent/skills/devops/SKILL.md`
- **Output:** Infrastructure deployed, documented

### 38. `observability` (spark-agent)
- **Purpose:** Build dashboards, monitoring, metrics systems
- **RPOLES:** Full flow with focus on data visualization
- **Location:** `~/spark-agent/skills/observability/SKILL.md`
- **Output:** Dashboard deployed, alerts configured

### 39. `testing` (spark-agent)
- **Purpose:** Create and maintain test suites
- **RPOLES:** Focused (Review→Plan→Outline→Locate→Implement→Ship)
- **Location:** `~/spark-agent/skills/testing/SKILL.md`
- **Output:** Test coverage, CI updated

## Spark Agent Integration Skills

### 40. `task-executor` (spark-agent)
- **Purpose:** Master execution skill that orchestrates RPOLES for any task type
- **Trigger:** Task claimed, ready to begin work
- **Location:** `~/spark-agent/skills/integration/task-executor.skill`
- **Output:** Coordinated RPOLES execution with phase checkpoints

---

## RPOLES as Universal Methodology

All task types follow RPOLES as their core execution pattern:

| Phase | Coding | Debugging | DevOps | Observability | Testing |
|-------|--------|---.------|------.--|-----...-----|---..----|
| Review | ✓ | ✓ | ✓ | ✓ | ✓ |
| Plan | ✓ | ✓ | ✓ | ✓ | ✓ |
| Outline | ✓ | (skip) | (skip) | ✓ | ✓ |
| Locate | ✓ | ✓ | ✓ | ✓ | ✓ |
| Implement | ✓ | ✓ | ✓ | ✓ | ✓ |
| Test | ✓ | ✓ | ✓ | ✓ | (as impl) |
| Ship | ✓ | ✓ | ✓ | ✓ | ✓ |

The task-type skills in `~/spark-agent/skills/` describe how to apply RPOLES
for each task type, while the persona skills in `agentic-workflows/skills/personas/`
provide the detailed implementation of each RPOLES phase.
