# Compaction Prompt

> Use when a long session must continue but context is bloated.
> Paste into the SAME session. The output becomes the new ground truth —
> carry it into the next session (or SESSION.md) verbatim.

---
Summarize this session so a new agent can continue seamlessly. Include:
1. GOAL and definition of done
2. Current state: what's done (file paths), what's mid-flight (exact step), what's blocked
3. The exact, verbatim text of any unresolved error
4. Decisions made and why (so they aren't re-litigated)
5. Files changed so far (paths only)
6. The immediate next action
Max 30 lines. No conversation history, no back-story.
---

## Grading the output (30-second check)
- ✅ Unresolved error appears VERBATIM (with line numbers) — reject summaries that paraphrase it
- ✅ Every NEVER/MUST constraint is present
- ✅ Mid-flight state includes the exact next step
- ❌ If any are missing, reply: "Redo items <x> — include them verbatim."
