# skill: debugging
# purpose: Find and fix bugs
# triggers: Task type = "debugging"

## RPOLES Integration

Debugging uses a **compressed RPOLES flow** — you still go through all phases, but
Outline is often skipped since you're fixing existing code rather than creating new structure.

| Phase | Skill | Output |
|-------|-------|--------|
| Review | dev-review | Bug understood, reproduction steps identified |
| Plan | dev-plan | Fix approach, affected files identified |
| Outline | — | Often skipped — fix is targeted |
| Locate | dev-locate | Root cause found, related code mapped |
| Implement | dev-implement | Bug fixed |
| Test | dev-test | Regression test added |
| Ship | dev-ship | Fix committed, PR open |

## Phase-Specific Actions

### REVIEW — Understand the Bug

```bash
# 1. Read bug report
# 2. Identify symptoms and expected behavior
# 3. Note any error messages, stack traces
# 4. Document reproduction steps
```

**Key questions:**
- What's the observed behavior?
- What's the expected behavior?
- When does it happen? (conditions, inputs)
- How often does it happen? (always, intermittent)

**Output:** Bug analysis in task file

```markdown
## Bug Analysis

**Symptoms:**
- Error message: "..."
- Fails when: [conditions]
- Frequency: always/intermittent

**Expected Behavior:**
- Should: [description]

**Reproduction Steps:**
1. [step 1]
2. [step 2]
3. [step 3]
```

### PLAN — Design the Fix

```bash
# 1. Hypothesize root causes
# 2. Identify investigation approach
# 3. List potentially affected files
# 4. Plan verification steps
```

**Output:** Fix plan in task file

```markdown
## Fix Plan

**Hypothesized Causes:**
1. [cause 1] - investigating
2. [cause 2] - backup theory

**Investigation Approach:**
1. Add logging at key points
2. Run reproduction case
3. Trace execution flow
4. Pinpoint root cause

**Potentially Affected Files:**
- src/module/handler.py
- src/module/utils.py
```

### LOCATE — Find Root Cause

```bash
# 1. Search for error message in codebase
grep -r "error-message" ~/claude-workspace/

# 2. Trace execution path
# 3. Add debugging logs if needed
# 4. Run reproduction case

# 5. Identify the actual root cause
```

**Output:** Root cause identified, documented in task file

### IMPLEMENT — Apply the Fix

```bash
# 1. Make minimal change to fix the bug
# 2. Avoid refactoring unrelated code
# 3. Commit the fix
git add .
git commit -m "[fix] [task/NNN] Fix: <what was fixed>"
git push
```

**Rule:** Fix the bug, don't rewrite everything.

### TEST — Validate the Fix

```bash
# 1. Run reproduction case — should now pass
# 2. Run existing test suite — ensure no regressions
# 3. Add regression test for this bug
```

**Output:** Regression test added, all tests passing

```markdown
## Regression Test

**Test Case:** [description]

```python
def test_bug_fix():
    # Setup reproduction case
    # Verify expected behavior
    assert result == expected
```
```

### SHIP — Deliver the Fix

```bash
# 1. Update task file with fix description
# 2. Open PR with clear description
# 3. Move task to done/
```

## Common Bug Patterns

### Null/Undefined Errors
- Check for missing null checks
- Verify data flow
- Add defensive programming

### Logic Errors
- Review conditional logic
- Check loop boundaries
- Verify algorithm correctness

### Integration Issues
- Check API contracts
- Verify data serialization
- Review error handling

### Race Conditions
- Check async/sync boundaries
- Review locking mechanisms
- Verify ordering guarantees

## Artifacts

| Artifact | Location | When |
|-----.----|-----.------|---.----|
| Bug analysis | task file | Review |
| Root cause | task file | Locate |
| Fix | code | Implement |
| Regression test | tests/ | Test |
| PR | GitHub | Ship |

## Checkpoints

```bash
checkpoint --phase review --description "Bug analyzed, reproduction steps identified" --next "Proceed to investigation"
checkpoint --phase locate --description "Root cause identified" --next "Proceed to fix"
checkpoint --phase implement --description "Bug fixed" --next "Proceed to test"
checkpoint --phase test --description "Fix validated, regression test added" --next "Proceed to ship"
checkpoint --phase ship --description "Fix committed, PR open" --next "Task complete"
```

## Success Criteria

- [ ] Bug reproduced and understood
- [ ] Root cause identified
- [ ] Fix is minimal and targeted
- [ ] Regression test added
- [ ] No new bugs introduced
- [ ] Task file complete with Result + Agent Log

---

*Debugging is targeted RPOLES. Review→Plan→Locate→Implement→Test→Ship.*
