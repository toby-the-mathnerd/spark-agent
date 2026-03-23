# skill: testing
# purpose: Create and maintain test suites
# triggers: Task type = "testing"

## RPOLES Integration

Testing tasks use a **focused RPOLES flow** — the emphasis is on Review (understanding
what to test), Plan (test strategy), and Implementation (writing tests).

| Phase | Skill | Output |
|-------|-------|--------|
| Review | dev-review | Coverage requirements understood |
| Plan | dev-plan | Test strategy, scope defined |
| Outline | dev-outline | Test structure, cases mapped |
| Locate | dev-locate | Existing tests, patterns found |
| Implement | dev-implement | Test cases written |
| Test | — | Tests run as part of implementation |
| Ship | dev-ship | Tests committed, CI updated |

## Phase-Specific Actions

### REVIEW — Understand Test Requirements

```bash
# 1. Read task requirements
# 2. Identify what needs testing
# 3. Determine coverage goals
# 4. Note any specific test scenarios
```

**Key questions:**
- What's being tested? (unit, integration, e2e)
- What's the coverage target?
- Are there specific scenarios to cover?
- Any existing tests to extend?

**Output:** Test requirements in task file

```markdown
## Test Requirements

**Target:** [component/module]

**Test Types:**
- Unit tests: [coverage]
- Integration tests: [coverage]
- E2E tests: [coverage]

**Specific Scenarios:**
- Scenario 1: [description]
- Scenario 2: [description]

**Coverage Target:** [X%]
```

### PLAN — Design Test Strategy

```bash
# 1. Define test categories
# 2. Plan test cases per feature
# 3. Identify fixtures/setup needed
# 4. Determine mock/stub requirements
```

**Output:** Test plan in task file

```markdown
## Test Plan

**Categories:**
- Unit: [files/functions to test]
- Integration: [interfaces to test]
- E2E: [flows to test]

**Test Cases:**
| Case | Type | Description |
|------|------|---...--|
| 1 | unit | [what] |
| 2 | integration | [what] |

**Fixtures Needed:**
- Fixture 1: [description]
- Fixture 2: [description]

**Mocks/Stubs:**
- Mock 1: [what, behavior]
```

### OUTLINE — Test Structure

```bash
# 1. Define test file structure
# 2. Plan test organization
# 3. Note dependencies between tests
```

**Output:** Outline in task file

```markdown
## Test Structure

**Files to Create:**
| File | Purpose | Cases |
|------|---------|-------|
| tests/test_feature.py | Feature tests | 1,2,3 |
| tests/test_utils.py | Utility tests | 4,5 |

**Test Organization:**
- Setup: [fixtures]
- Tests: [grouped by feature]
- Teardown: [cleanup]
```

### LOCATE — Find Existing Tests

```bash
# Check existing tests
find ~/claude-workspace/ -name "test_*.py" -o -name "*_test.py" | head -20

# Review test patterns
grep -r "def test_" ~/claude-workspace/tests/ --include="*.py" | head -10

# Check test config
ls ~/claude-workspace/tests/
cat ~/claude-workspace/pyproject.toml | grep -A 10 "\[tool.pytest\]"
```

**Output:** Existing test patterns identified

### IMPLEMENT — Write Test Cases

```bash
# 1. Create test fixtures
# 2. Write test cases
# 3. Run tests after each batch
# 4. Fix any failures
# 5. Commit incrementally

git add .
git commit -m "[task/NNN] test: add [feature] tests"
git push
```

**Common patterns:**

```python
# Example: Unit test
def test_function_output():
    result = function(input)
    assert result == expected

# Example: Integration test
def test_api_endpoint():
    response = client.get("/api/endpoint")
    assert response.status_code == 200
    assert "key" in response.json()

# Example: Fixture
@pytest.fixture
def sample_data():
    return {"key": "value"}
```

### SHIP — Commit Tests

```bash
# 1. Ensure all tests pass
# 2. Verify coverage meets target
# 3. Update CI if needed
# 4. Document in task file
# 5. Move task to done/
```

## Test Type Patterns

### Unit Tests
```python
import pytest

def test_addition():
    assert add(2, 3) == 5

def test_division_by_zero():
    with pytest.raises(ZeroDivisionError):
        divide(1, 0)
```

### Integration Tests
```python
def test_database_connection():
    db = Database()
    db.connect()
    assert db.is_connected()
    db.close()
```

### E2E Tests
```python
def test_user_login_flow():
    page = browser.new_page()
    page.goto("/login")
    page.fill("#username", "testuser")
    page.fill("#password", "secret")
    page.click("#login-btn")
    assert page.url == "/dashboard"
```

## Artifacts

| Artifact | Location | When |
|---------|---..----|---..---|
| Test files | tests/ | Implement |
| Fixtures | tests/conftest.py | Implement |
| Coverage report | coverage.html | Test |
| CI config | .github/workflows/ | Ship |

## Checkpoints

```bash
checkpoint --phase review --description "Test requirements understood" --next "Proceed to planning"
checkpoint --phase outline --description "Test structure defined" --next "Proceed to locate"
checkpoint --phase locate --description "Existing patterns identified" --next "Proceed to implement"
checkpoint --phase implement --description "Test cases written" --next "Proceed to ship"
checkpoint --phase ship --description "Tests committed, coverage met" --next "Task complete"
```

## Success Criteria

- [ ] Test cases cover all scenarios
- [ ] Coverage target met
- [ ] All tests pass
- [ ] Tests follow existing patterns
- [ ] Documentation updated
- [ ] Task file complete with Result + Agent Log

---

*Testing is quality RPOLES. Review→Plan→Outline→Locate→Implement→Ship.*
