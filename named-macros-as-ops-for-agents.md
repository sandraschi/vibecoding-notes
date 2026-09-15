# Turn recurring chores into named macros your agent can run as a pipeline

**Dated:** 2026-09-15

If you maintain more than a handful of repos or projects, you eventually accumulate a mental checklist for "assess whether this is worth fixing," "bring this up to current standards," "check if this is even worth keeping." The problem: that checklist lives in your head, gets re-derived slightly differently every time, and can't be handed to an agent except as a wall of ad-hoc instructions typed fresh each session.

## The pattern: utterance → procedure, not utterance → vibes

Give each recurring chore a short name that expands, deterministically, into a written multi-phase procedure — with phase gates, not just a suggestion to "be thorough."

A small real example (four macros covering a fleet of 190+ small repos, one maintainer):

| You say | It means |
|---|---|
| `drift` | Read-only triage across everything — which projects need attention, no edits made |
| `fakefind <project>` | Is this actually working, or does it just look like it does? Report only |
| `qualitycheck <project>` | Should this project exist at all? Strategic verdict, not a lint pass |
| `assfix <project>` | The full mechanical pass — assess, fix, lint, docs, package, ship |

Two things make this work instead of degrading into "please be thorough" theater:

1. **The checklist is written down once, centrally**, and the macro just routes to it. Every session reads the same standard instead of the agent (or you) improvising a slightly different bar each time.
2. **Read-only triage is separate from mutation.** `drift` and `qualitycheck` never edit anything — cheap to run often, safe to run on things you're not sure about yet. Only `assfix` mutates, and only after you've decided (via the cheap read-only step) that it's worth the cost.

## Why this beats "just describe what you want each time"

A fresh prose instruction every session means the bar silently drifts — a slightly different phrasing gets a slightly different depth of review, and you can't tell in advance which. A named macro pointing at one written procedure gives you the same bar every time, and — just as important — gives you a queue: "12 done, 38 to go" means something concrete instead of "I should get around to cleaning these up someday."

## The frugality rule that keeps this from becoming its own problem

The full heavy pass (`assfix`-equivalent) is expensive — token cost, time, risk of touching more than you meant to. Don't run it on everything reflexively:

- Run the cheap, read-only triage first, always. Decide with that data whether the expensive pass is warranted.
- One project through the full pipeline before starting the next — don't batch the expensive step across many projects in one sitting. That's how you get inconsistent damage instead of consistent quality (see [checkpoint-commits-and-bak-files.md](checkpoint-commits-and-bak-files.md)).
- If a macro is being invoked for something trivial ("assfix this to change a comment"), that's a sign the tool is being used as a magic word instead of matched to the actual task. Match the tool to the task, every time.

## Adapting this with almost no infrastructure

You don't need a plugin system to get the core benefit. A folder of dated, versioned checklist files plus a personal convention ("when I say X, read file Y and follow it") gets you 90% of the value. The infrastructure (skills, slash commands, whatever your tool calls them) is a convenience for triggering the procedure, not the source of its value — the written, centralized procedure is.
