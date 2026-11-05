# Session Brief — <task name>

> Paste this at the START of every AI session. Fill every bracket.
> If you can't fill one, that's what to figure out first.

## 1. Goal (what + why)
GOAL: <one sentence, action + target>
DONE WHEN: <observable, testable success condition>
OUT OF SCOPE: <what this task must NOT touch or do>

## 2. Ground truth (facts, not guesses)
STACK: <language + versions, frameworks + versions, test runner>
FILES: <exact paths of files involved>
RUN: <command to run> · TEST: <command> · LINT: <command if any>

## 3. Constraints (the rules that don't bend)
MUST: <patterns to follow, APIs to keep stable, etc.>
NEVER: <no new deps, don't touch auth, don't change schema...>

## 4. Evidence (pasted, not summarized)
<VERBATIM error text / failing output / relevant code — with line numbers>

## 5. Working agreements (how this session runs)
- Plan first; I approve before you edit
- Diffs not full files (when file > 50 lines)
- If unsure or blocked, say so — do not guess
- Run tests after every change
