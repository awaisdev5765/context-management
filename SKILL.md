---
name: context-management
description: Use this skill whenever an AI coding session is being planned, started, continued, or is running long. Covers how to brief AI agents effectively, what context to include or exclude, when to start fresh vs continue, how to write handoff/continuity documents, and how to compress long sessions without losing critical state. Applies to every AI coding tool (Claude Code, Cursor, Copilot, ChatGPT, Gemini, pi) and every programming task.
---

# Context Management for AI Coding Sessions

This skill has two audiences:

1. **You (the AI agent)** — actively manage context on every task. This file tells you how.
2. **The human** — the templates in this file are theirs to reuse. Offer them when a session is going wrong.

The core principle: **context is the scarcest resource in an AI session.** Wasted tokens, stale assumptions, and missing files cause most failed AI coding sessions — not model intelligence.

---

## Part 1 — The Perfect Brief (session start)

When the human starts a task, check their brief against this checklist. If items are missing, ask for them **before** doing anything else — one clarifying question at minute zero saves ten failed iterations.

A complete brief has **five blocks**, in this order:

### 1. Goal (what + why)
```
GOAL: Make the checkout button submit the order via the existing /api/orders endpoint.
DONE WHEN: Clicking checkout creates an order in the database and redirects to /orders/success.
```
- State the **definition of done**, not the task description. "Add a search bar" is not a goal. "Search filters the visible list by title as the user types" is.
- Include what is **explicitly out of scope** — agents over-deliver by default.

### 2. Ground truth (facts, not guesses)
```
STACK: React 18 + Vite, TypeScript, Tailwind, zod. Tests: vitest.
FILES: src/components/CheckoutButton.tsx, src/api/orders.ts
RUN: npm run dev (localhost:5173) · TEST: npm test · LINT: npm run lint
```
- Exact file paths, exact commands. Anything the agent would otherwise hallucinate.
- **Version numbers matter.** "Node 20, Tailwind v3" prevents an agent from writing v4-only syntax.

### 3. Constraints (the rules that don't bend)
```
MUST: keep existing API responses unchanged; follow the error handling pattern in src/api/orders.ts
NEVER: install new dependencies; touch auth code; modify the DB schema
```
- Every silent assumption an agent makes costs a review cycle. Surface them here.

### 4. Evidence (pasteds, not summaries)
- Paste the **actual error text**, the actual file content, the actual failing test output.
- Never paraphrase errors. "It doesn't work" wastes a round trip; the stack trace resolves it.
- Trim to the relevant part — but never trim line numbers from stack traces.

### 5. Working agreements (how the session runs)
```
- Make a plan before editing; I approve before you write files.
- Show diffs, not full files, when a file is over 50 lines.
- If blocked or unsure, say so instead of guessing.
- Run the test suite after every change.
```

---

## Part 2 — Context Budget: what to include, what to cut

When assembling context (files, logs, conversation), apply this priority order. Include top-down until you approach your budget; cut bottom-up.

| Priority | Include | Why |
|---|---|---|
| 🔴 1 | Current error / failing output | The thing being fixed |
| 🔴 2 | The file(s) being edited | Full content, always |
| 🟠 3 | Interfaces the edited code touches (types, exports, API shapes) | Signatures only — not bodies |
| 🟠 4 | The one pattern to imitate (an existing well-done example) | Agents imitate, they don't infer style |
| 🟡 5 | Relevant config (tsconfig, package.json deps) | Only the sections in play |
| 🟡 6 | Recent commit messages on these files | Prevents re-doing rejected approaches |
| ⚪ 7 | Everything else | Summarize to one line or drop |

### Hard rules
- **Never include a whole directory dump.** The agent reads what it needs; dumping files buries the real signal and *lowers* output quality.
- **Past conversation is not free.** In long sessions, old messages are stale context. Compress aggressively (Part 5).
- **File paths over file contents** when you're just orienting: `src/api/orders.ts` may be all the agent needs to decide it doesn't need it.
- **One example beats ten instructions.** If the codebase has an established pattern, paste 10 lines of it instead of describing it.

---

## Part 3 — Session lifecycle: fresh vs continue vs compact

Run this decision check whenever a session is long, drifting, or starting a new subtask:

### Start FRESH when:
- The new task only shares a repo with the old one (different file, different goal)
- The current session has had **2+ failed fix attempts** on the same error — old wrong hypotheses poison every subsequent guess
- Context usage is high and the old content is mostly resolved discussion
- You're switching feature branches or switching task type (bug → feature)

### CONTINUE when:
- The same file/problem is mid-flight and the agent has working knowledge loaded
- Undoing and re-briefing would cost more than the stale context costs

### COMPACT when:
- The session is long but the work is genuinely continuous — see Part 5

**Rule of thumb:** context rot is real. When the agent starts contradicting things it said earlier, ignoring instructions, or "forgetting" constraints — start fresh with a handoff document. Do not push through.

---

## Part 4 — Handoff documents (the SESSION.md pattern)

This is the single highest-leverage habit in AI coding. Maintain a `SESSION.md` in the repo root that any agent can read to become fully oriented in ~10 seconds.

### Template
```markdown
# SESSION — <project name>
Updated: <date>          Branch: <branch>

## Project
One paragraph: what this is, stack, how to run/test.

## Current state
- ✅ DONE: <what works, with file paths>
- 🔨 IN PROGRESS: <task, file, exact step where it stopped>
- ❌ BLOCKED: <problem, error text, attempts so far>

## Decisions made (do not relitigate)
- <Decision> — because <reason> (<date>)

## Next steps (in order)
1. <next concrete action>
2. ...

## Gotchas
- <Weird thing about this codebase the next agent must know>
```

### Rules for the agent
- **Update SESSION.md proactively** whenever you finish a meaningful step, make a decision, or get blocked — don't wait to be asked.
- When starting work on a repo with a SESSION.md: **read it first**, and never re-derive information it contains.
- When finishing a session: leave the file accurate even if the task is incomplete. A handoff is the deliverable when you're cut off mid-task.
- Decisions section is append-only. If a decision is reversed, add "REVERSED: <date>" — don't delete history.

---

## Part 5 — Compaction: compressing a long session without losing state

When a session must continue but the context is bloated, produce a compaction summary **and then treat it as the new ground truth**.

### Compaction prompt (agent-agnostic)
```
Summarize this session so a new agent can continue seamlessly. Include:
1. GOAL and definition of done
2. Current state: what's done (file paths), what's mid-flight, what's blocked
3. Exact error text of any unresolved error
4. Decisions made and why (so they aren't re-litigated)
5. Files changed so far (paths only)
6. The immediate next action
Max 30 lines. No conversation history, no back-story.
```

### What compaction must preserve (in order of importance)
1. **Unresolved errors, verbatim** — a paraphrased stack trace is a new failure
2. **Decisions and their reasons** — agents relitigate anything unexplained
3. **Mid-flight state** — "checkout.tsx: refactor is half done, step 3 of 4"
4. **Constraints** — every NEVER, verbatim

### What compaction must drop
- Superseded attempts ("tried X, didn't work" → keep one line, not the whole exchange)
- Old file contents (the file on disk is the truth; the chat is not)
- Greetings, apologies, re-statements of the task

---

## Part 6 — Anti-patterns (refuse these politely)

| Anti-pattern | Why it fails | Do instead |
|---|---|---|
| "Here's my whole codebase, add a feature" | Signal buried in noise; agent fixes the wrong layer | Brief format from Part 1 |
| "It doesn't work" (no error text) | Guarantees a guess | Paste the verbatim error |
| 200-message session on one bug | Context rot; earlier wrong hypotheses dominate | Fresh session + handoff |
| "Fix it like my last project" (no code) | Agents can't see other projects | Paste the one exemplar file |
| Re-pasting corrected files again and again | Chat history diverges from disk | Point at file paths; disk is truth |
| Skipping the plan approval | Agent builds the wrong thing confidently | Plan-first agreement (Part 1.5) |
| "Continue" with no goal restated | Agent invents the goal | Restate goal in one line each session |

---

## Part 7 — Quick reference card

**Starting a task:** Goal + Done-when + Stack/paths + Constraints + Verbatim evidence + Working agreement.
**Deep in a task:** disk is truth → errors verbatim → one exemplar → compact every ~50 exchanges.
**Switching tasks:** handoff document → fresh session.
**Blocked twice on the same error:** stop guessing, bisect or write a minimal repro, new session.
**Finishing:** update SESSION.md — the next agent thanks you.

---

*This skill is agent-agnostic: it applies identically to Claude Code, Cursor, GitHub Copilot, ChatGPT, Gemini, Windsurf, Aider, pi, or any future tool. The principles are model-independent because context economics are model-independent.*
