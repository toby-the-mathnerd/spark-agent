# skill: coding
# purpose: Implement new features and code changes
# triggers: Task type = "coding"

## RPOLES Integration

Coding tasks use the **full RPOLES flow**:

| Phase | Skill | Output |
|-------|-------|--------|
| Review | dev-review | Requirements analyzed, ambiguities identified |
| Plan | dev-plan | Implementation phases, checkpoints defined |
| Outline | dev-outline | File-by-file implementation plan |
| Locate | dev-locate | Dependencies mapped, patterns found |
| Implement | dev-implement | Code written |
| Test | dev-test | Tests created/updated |
| Ship | dev-ship | PR ready, changes staged |

## Phase-Specific Actions

### REVIEW — Understand the Task

```bash
# 1. Read the task file
cat ~/spark-tasks/tasks/pending/task-NNN.md

# 2. Extract requirements
grep -A 20 "## Objective" task-file.md

# 3. Check for related work
grep -r "<key-concept>" ~/claude-workspace/ --include="*.py" --include="*.ts" | head -20

# 4. Document ambiguities in task file
```

**Output:** Updated task file with clarifications needed (if any)

### PLAN — Design the Approach

```bash
# 1. Break into phases
# 2. Define checkpoints after each phase
# 3. Estimate effort per phase
# 4. Identify dependencies
```

**Output:** Plan document in task file under "## Plan"

```markdown
## Plan

### Phase 1: Foundation
- Create base structure
- Set up configuration
- Checkpoint: foundation-done

### Phase 2: Core Implementation
- Implement main logic
- Add error handling
- Checkpoint: core-done

### Phase 3: Integration
- Connect to existing systems
- Add API endpoints
- Checkpoint: integration-done
```

### OUTLINE — File-by-File Blueprint

```bash
# 1. List all files to create/modify
# 2. For each file, define changes
# 3. Note dependencies between files
```

**Output:** Outline in task file

```markdown
## Outline

| File | Action | Changes | Depends On |
|------|--------|---------|---|
| src/new-feature/__init__.py | create | New package | - |
| src/new-feature/handler.py | create | Main logic | foundation-done |
| tests/test_new_feature.py | create | Test suite | core-done |
```

### LOCATE — Find Dependencies

```bash
# Find related code
grep -r "import <module>" ~/claude-workspace/ --include="*.py"

# Check existing patterns
find ~/claude-workspace/ -name "*pattern*" -o -name "*template*"

# Review similar implementations
ls ~/claude-workspace/src/ | grep -E "feature|handler|service"
```

**Output:** Dependency map in task file

### IMPLEMENT — Write the Code

**Rule:** One phase at a time. Commit after each phase.

```bash
# 1. Create task branch
git checkout -b task/NNN

# 2. Implement Phase 1
# 3. Commit
git add .
git commit -m "[task/NNN] Phase 1: Foundation complete"
git push

# 4. Update task file
# 5. Repeat for each phase
```

**Output:** Code on task branch, task file updated

### TEST — Validate Implementation

```bash
# 1. Create/update tests
# 2. Run test suite
# 3. Fix any failures
# 4. Verify coverage
```

**Output:** Passing tests, coverage report in task file

### SHIP — Prepare for Merge

```bash
# 1. Final commit
# 2. Open PR
# 3. Update task file with Result section
# 4. Move task to done/
```

**Output:** PR open, task in done/

## Common Patterns

### New Feature
1. Create package/module structure
2. Define interface/contract
3. Implement core logic
4. Add error handling
5. Write tests
6. Document usage

### Bug Fix
1. Reproduce the bug
2. Identify root cause
3. Fix the issue
4. Add test to prevent regression
5. Verify fix

### Refactor
1. Document current behavior
2. Create tests for current behavior
3. Make structural changes
4. Verify tests still pass
5. Document changes

## Artifacts

| Artifact | Location | When |
|----------|-----------|---...|
| Task branch | git | After claim |
| Code files | ~/claude-workspace/ | During implement |
| Tests | ~/claude-workspace/tests/ | During test |
| PR | GitHub | When done |
| Task file | spark-tasks/tasks/done/ | When done |

## Checkpoints

After each RPOLES phase, create a git checkpoint:

```bash
checkpoint --phase review --description "Requirements analyzed" --next "Proceed to planning"
checkpoint --phase plan --description "Implementation plan created" --next "Proceed to outline"
checkpoint --phase outline --description "Implementation outline complete" --next "Proceed to locate"
checkpoint --phase locate --description "Dependencies mapped" --next "Proceed to implement"
checkpoint --phase implement --description "Phase N complete" --next "Proceed to next phase or test"
checkpoint --phase test --description "Tests passing" --next "Proceed to ship"
checkpoint --phase ship --description "PR open, ready for review" --next "Task complete"
```

## Success Criteria

- [ ] Code follows existing patterns
- [ ] Tests cover new functionality
- [ ] Documentation updated
- [ ] No regressions introduced
- [ ] PR has clear description
- [ ] Task file complete with Result + Agent Log

---

*Coding is RPOLES in action. Review→Plan→Outline→Locate→Implement→Test→Ship.*
