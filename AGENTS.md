# AGENTS.md — Spark 2 Operational Rules

This file contains Spark 2 specific operational rules.
Coordination protocol lives in ~/spark-tasks/AGENTS.md (deprecated — now removed).

## Startup Sequence
At the start of every session:
1. Read ~/spark-agent/SOUL.md
2. Read ~/spark-agent/SKILLS.md
3. Read ~/spark-agent/TOOLS.md
4. Check ~/spark-tasks/tasks/pending/ for work

## Skill Routing
After reading the task objective, load the relevant skill:
- coding → ~/spark-agent/skills/coding/SKILL.md
- debugging → ~/spark-agent/skills/debugging/SKILL.md
- devops → ~/spark-agent/skills/devops/SKILL.md
- observability → ~/spark-agent/skills/observability/SKILL.md
- testing → ~/spark-agent/skills/testing/SKILL.md
- investigation → read rpoles-methodology.md

Full persona skills and RPOLES workflows:
~/spark-agent/agentic-workflows/skills/personas/
~/spark-agent/agentic-workflows/workflows/rpoles-methodology.md

## Git Rules — CRITICAL
- NEVER create branches in ~/spark-tasks/ — always commit directly to main
- ~/spark-tasks/ is the coordination repo — no branches, no PRs
- Only create branches in ~/claude-workspace/<project>/ for code work
- Before any commit in ~/spark-tasks/, verify: git branch --show-current
- Always push after every commit to ~/spark-tasks/

## File Output Rules — CRITICAL
Never create files in ~/spark-tasks/ root.
Only STATUS.md, README.md belong there.

Put deliverables here:
- Reports, plans, analysis → ~/spark-tasks/docs/
- Scripts and tools → ~/spark-tasks/scripts/
- Code projects → ~/claude-workspace/<project-name>/
- Test data → ~/spark-tasks/scripts/tests/data/

Always include the full output path in the task Result section.

## Repository Rules — CRITICAL
- ~/spark-tasks/ is already cloned — never clone it again
- Never add spark-tasks as a submodule anywhere
- Never clone spark-tasks inside claude-workspace
- Never create files in ~/spark-tasks/tasks/ — that is Spark 1's job
- Never modify poll_tasks.py or watch_tasks.py unless task explicitly requires it

## Task File Naming — CRITICAL
Format: YYYY-MM-DD-HH-MM-task-NNN.md
Get current time: date +'%Y-%m-%d-%H-%M'
Never use ISO 8601 format with T or Z in filenames.

## Definition of Done
A task is NOT done until ALL of these are true:
- All required files exist on disk (verify with ls -la)
- All tests written, committed, and passing (verify with pytest)
- Everything committed to main in ~/spark-tasks/ (verify with git log)
- Everything pushed to remote (verify with git status + git push)
- Only then call task_done

## Verification Checklist — Run Before EVERY task_done
1. bash: ls -la <every required output file>
2. bash: python3 -m pytest <test file> -v (if tests required)
3. bash: git -C ~/spark-tasks branch --show-current (must show main)
4. bash: git -C ~/spark-tasks log --oneline -3
5. bash: git -C ~/spark-tasks status (must be clean)
6. bash: git -C ~/spark-tasks push

Calling task_done without passing this checklist is a CRITICAL FAILURE.

## Result Section Format — CRITICAL
Every completed task Result section MUST include:

**Skill used:** <which RPOLES skill was loaded>
**Phases completed:** <which RPOLES phases were executed>
**Files created:**
- <full path to every file created or modified>

**Tests:** <pass/fail count, or none required>
**Commits:** <list of commit hashes and messages>
**Summary:** <2-3 sentences describing what was actually built>

A Result that just says "Task completed" is a CRITICAL FAILURE.

## Commit Rules
- Never go more than 5 minutes without committing if actively working
- If a task has no updates for 10 minutes, write a status update to the task file
- All code goes in ~/claude-workspace/ not in spark-tasks

## Exploration Rules
Before reading or writing any file:
1. Always start with a directory listing to confirm paths exist:
   bash: ls -la <parent directory>
2. Never guess a path — verify it exists first
3. If a path doesn't exist after 2 attempts, use find:
   bash: find ~ -name "<filename>" 2>/dev/null
4. Map the full directory structure ONCE at the start of a task:
   bash: find ~/spark-tasks -type f -name "*.py" | head -30
   bash: find ~/spark-tasks -type d | head -20
5. Do not repeat directory listing calls for the same path

## Blocked Task Requirements
When calling task_blocked the question field MUST include:
1. What the task objective was
2. What was attempted (specific commands/files)
3. What error or problem occurred (exact error message)
4. What specific input or decision is needed from Toby

A task_blocked call with a vague or empty question is a CRITICAL FAILURE.
