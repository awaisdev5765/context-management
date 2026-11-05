# Context Management — the skill every AI coder needs

**A universal, open-source skill that teaches any AI coding agent (and any human) how to run AI coding sessions that actually work: perfect briefs, context budgets, handoff documents, and lossless compaction.**

[![Works with](https://img.shields.io/badge/works%20with-Claude%20Code%20·%20Cursor%20·%20Copilot%20·%20ChatGPT%20·%20Gemini%20·%20pi-blue)](#install)

## Why this exists

Every failed AI coding session fails the same way: missing files, paraphrased errors, stale assumptions, a 200-message chat trying to fix one bug. **The model wasn't the problem. The context was.**

This skill fixes the *process*, so it works on every AI tool — today and in the future.

## What it gives you

| Part | What | The problem it kills |
|---|---|---|
| 1 | **The Perfect Brief** — 5-block session opener | "It doesn't work" round-trips |
| 2 | **Context Budget** — a 7-tier priority order for files/logs | Codebase dumps that bury the signal |
| 3 | **Fresh / Continue / Compact** — session lifecycle decision rules | "Context rot" from endless sessions |
| 4 | **SESSION.md handoff pattern** — a living doc every agent can read | Losing everything when a session dies |
| 5 | **Compaction prompts** — compress a long session losslessly | Summaries that drop the stack trace |
| 6 | **Anti-patterns** — 7 common failure patterns with fixes | Repeating the same mistakes |
| 7 | **Quick reference card** — the whole skill on one screen | Forgetting it when it matters |

## Install

### pi
```bash
git clone https://github.com/YOUR_USER/context-management ~/.agents/skills/context-management
```
That's it — the skill activates automatically when relevant.

### Claude Code
Copy `SKILL.md` content into a project `CLAUDE.md` (or reference it there), or place it in your `.claude/skills/context-management/SKILL.md`.

### Cursor / Windsurf / any rules-based tool
Copy the rules you want into `.cursor/rules/context-management.mdc` — each Part is self-contained.

### ChatGPT / Gemini / any chat AI
Paste the compaction prompt (Part 5) and the brief template (Part 1) into custom instructions. The skill is modular — each part works alone.

## The 60-second version

1. **Brief every task**: Goal + Done-when + Stack/paths + Constraints + verbatim errors + working agreement
2. **Disk is truth** — point at file paths, don't re-paste files
3. **Two failed attempts on the same bug?** Stop. New session + handoff document.
4. **Keep a `SESSION.md`** in every repo — the next agent reads it and is oriented in seconds
5. **Compact long sessions** with the Part 5 prompt — preserve errors verbatim, decisions, and mid-flight state

## Contributing

The skill is deliberately model-agnostic. PRs should follow the same bar: every rule must work identically on ChatGPT, Claude, Gemini, and Copilot. If it only helps one tool, it belongs in that tool's docs, not here.

Ideas welcome: localization, tool-specific install guides, a v1 → v2 migration for the SESSION.md format.

## License

MIT — see [LICENSE](LICENSE).
