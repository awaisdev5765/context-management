# Context Management — the skill every AI coder needs

**A universal, open-source skill that teaches any AI coding agent (and any human) how to run AI coding sessions that actually work: perfect briefs, context budgets, handoff documents, and lossless compaction.**

[![Works with](https://img.shields.io/badge/works%20with-Claude%20Code%20·%20Cursor%20·%20Copilot%20·%20ChatGPT%20·%20Gemini%20·%20pi-blue)](#how-to-use)

## Why this exists

Every failed AI coding session fails the same way: missing files, paraphrased errors, stale assumptions, a 200-message chat trying to fix one bug. **The model wasn't the problem. The context was.**

This skill fixes the *process*, so it works on every AI tool — today and in the future.

## How to use

### ⚡ 30-second version (no install needed — works in ANY chat)
1. **Starting a task?** Fill [`templates/SESSION_BRIEF.md`](templates/SESSION_BRIEF.md) and paste it as your first message.
2. **Chat is long and drifting?** Paste [`templates/COMPACTION_PROMPT.md`](templates/COMPACTION_PROMPT.md) — its output is the state you carry into the next chat.
3. **Working across days on a repo?** Keep [`templates/SESSION.md`](templates/SESSION.md) in the repo root and tell every AI: *"Read SESSION.md first."*
4. **Session died mid-task?** SESSION.md IS the recovery — the next agent picks up exactly where this one stopped.

That's it. The templates work on ChatGPT, Claude, Gemini, Copilot, Cursor — anywhere.

### 🔧 Full install (the AI follows the skill automatically)

**pi**
```bash
git clone https://github.com/awaisdev5765/context-management ~/.agents/skills/context-management
```
The skill activates automatically whenever a session is planned, started, continued, or running long.

**Claude Code**
Add to your project's CLAUDE.md:
```
- Follow the context-management skill: see context-management/SKILL.md
```
Or copy SKILL.md into `.claude/skills/context-management/SKILL.md`.

**Cursor / Windsurf**
Paste the rules you want into `.cursor/rules/context-management.mdc` — each Part is self-contained. (Settings → Rules → Add rule also works.)

**ChatGPT / Gemini (browser)**
Paste Part 1 (The Perfect Brief) and Part 5 (Compaction) into Custom Instructions. The skill is modular — each part works alone.

### 🎯 The two habits that matter most
- **Disk is truth** — point the AI at file paths, never re-paste files into the chat.
- **Two failed attempts on the same bug?** Stop. New session + SESSION.md handoff. Pushing through makes it worse.

## What the skill contains

| Part | What | The problem it kills |
|---|---|---|
| 1 | **The Perfect Brief** — 5-block session opener | "It doesn't work" round-trips |
| 2 | **Context Budget** — a 7-tier priority order for files/logs | Codebase dumps that bury the signal |
| 3 | **Fresh / Continue / Compact** — session lifecycle decision rules | "Context rot" from endless sessions |
| 4 | **SESSION.md handoff pattern** — a living doc every agent can read | Losing everything when a session dies |
| 5 | **Compaction prompts** — compress a long session losslessly | Summaries that drop the stack trace |
| 6 | **Anti-patterns** — 7 common failure patterns with fixes | Repeating the same mistakes |
| 7 | **Quick reference card** — the whole skill on one screen | Forgetting it when it matters |

Full skill: [SKILL.md](SKILL.md) · Templates: [`templates/`](templates/)

## Contributing

The skill is deliberately model-agnostic. PRs should follow the same bar: every rule must work identically on ChatGPT, Claude, Gemini, and Copilot. If it only helps one tool, it belongs in that tool's docs, not here.

Ideas welcome: localization, tool-specific install guides, a v1 → v2 migration for the SESSION.md format.

## License

MIT — see [LICENSE](LICENSE).
