# RPOLES Methodology

The RPOLES workflow is the core methodology for the Developer persona. Each agent specializes in one phase.

## Phase 1: REVIEW
**Agent:** `dev-reviewer`
**Responsibilities:**
- Analyze incoming task from spark/openclaw
- Identify technical requirements and constraints
- Flag ambiguities for clarification
- Check for security/performance implications
- Output: Requirements summary + clarifying questions

**Exit Criteria:** Requirements are clear and documented

## Phase 2: PLAN
**Agent:** `dev-planner`
**Responsibilities:**
- Break down task into implementation steps
- Identify affected files and components
- Estimate complexity and risks
- Create milestone checkpoints
- Output: Implementation plan with checkpoints

**Exit Criteria:** Plan is approved, git checkpoint created

## Phase 3: OUTLINE
**Agent:** `dev-outliner`
**Responsibilities:**
- Create file-by-file implementation outline
- Define function/class signatures
- Document interfaces and data flows
- Create test strategy outline
- Output: Detailed implementation outline

**Exit Criteria:** Outline is approved, git checkpoint created

## Phase 4: LOCATE
**Agent:** `dev-locator`
**Responsibilities:**
- Find existing code patterns to follow
- Locate relevant dependencies and imports
- Identify reusable components
- Map dependencies and imports
- Output: Dependency map + file locations

**Exit Criteria:** All dependencies identified, git checkpoint created

## Phase 5: EXECUTE
**Agent:** `dev-implementer` (can spawn sub-implementers by file/module)
**Responsibilities:**
- Implement code per the outline
- Follow existing code patterns
- Create/update tests alongside code
- Self-review against requirements
- Output: Implemented code + tests

**Exit Criteria:** Code implemented and passing local validation, git checkpoint created

## Phase 6: SHIP
**Agent:** `dev-shipping`
**Responsibilities:**
- Run final validation suite
- Create changelog entry
- Stage for commit with proper message
- Create PR or prepare for handoff
- Output: Ready-to-merge changes

**Exit Criteria:** Changes are staged and documented
