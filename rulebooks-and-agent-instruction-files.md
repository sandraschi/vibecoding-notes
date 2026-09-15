# Rulebooks and agent instruction files: a very moving target

**Dated:** 2026-09-15

A year ago, using an AI coding tool seriously meant hand-typing an increasingly long, increasingly defensive instruction file — a `.cursorrules`, a `CLAUDE.md`, whatever your tool called it — full of corrections for things a competent human colleague wouldn't need told once: "don't use Linux commands in PowerShell," "never put in Unicode emojis or em dashes," "ALWAYS read the rulebook at the start of chat," and a slowly growing pile of similar rules, each one a scar from a specific incident. Some dev shops apparently ran this seriously enough to have something like a dedicated rulebook specialist — a real, if slightly absurd, job title for a moment in time. That detail alone tells you how much manual correction the tools needed not that long ago.

## The moving target problem, stated plainly

Two things kept changing at once, which is what made this genuinely hard to keep up with rather than just tedious:

1. **The wrapper format itself churns.** `.cursorrules` gives way to `AGENTS.md`, which coexists with tool-specific files, which coexists with structured "skills" systems that are neither a flat rules file nor a prompt. Time invested in mastering one format's quirks doesn't fully transfer to the next one.
2. **The content needed inside the wrapper shrinks as models improve** — see [ai-of-the-gaps-and-the-hype-reflex.md](ai-of-the-gaps-and-the-hype-reflex.md). A rule you wrote to correct a real, painful limitation a year ago can quietly become dead weight (or, worse, actively wrong guidance) once the underlying model no longer has that limitation. Nobody prunes rulebooks as diligently as they add to them.

## What actually persists across the churn

The wrapper format is not the durable part. The **content categories** are, even as their specific wording and the file they live in keeps changing:

- **Platform/environment gotchas** — shell syntax mismatches, path conventions, tool invocation quirks specific to your OS or toolchain.
- **Output hygiene** — the ASCII/no-emoji/no-em-dash family of rules from [llm-output-hygiene.md](llm-output-hygiene.md), plus the anti-hype rule from [ai-of-the-gaps-and-the-hype-reflex.md](ai-of-the-gaps-and-the-hype-reflex.md).
- **Safety gates** — what requires explicit confirmation before happening (destructive ops, pushes, anything touching shared state), independent of which tool is asking.
- **Workflow sequencing** — "read the standard before coding," "checkpoint before a batch edit," the process-level rules from [checkpoint-commits-and-bak-files.md](checkpoint-commits-and-bak-files.md) and [fix-the-gate-you-find.md](fix-the-gate-you-find.md).
- **Personal/house style** — tone, verbosity, how you want disagreement expressed, project-specific conventions.

Maintain these as your actual portable ruleset, mentally separate from whatever file format currently holds them. When the format changes again (it will), you're migrating content you already have, not starting over.

## The practical habit: prune as often as you add

Since a rulebook accumulates scars and rarely sheds them, periodically re-read your own instruction file and ask, for each rule, "is this still true, or did the underlying tool get better since I wrote this?" A rule correcting a limitation that no longer exists isn't neutral — it's clutter that makes the file longer to read (costing the model's attention on every session) and occasionally actively wrong (a workaround for a bug that's since been fixed can produce worse behavior than doing nothing). Treat rulebook maintenance the same way [staying-current-without-getting-burned.md](staying-current-without-getting-burned.md) treats dependencies: additions get watched in, but staleness needs actively removing, not just tolerating.

A real, slightly embarrassing example is the easiest way to see why this can't be a someday chore: a rulebook can end up with an entry like "always use FastMCP 2.1" sitting at rule #25, quietly telling every future session to scaffold against exactly the stale floor that [staying-current-without-getting-burned.md](staying-current-without-getting-burned.md) warns against — self-inflicted, because the rule was correct when written and nobody revisited it after the framework moved on. The fix isn't "be more careful next time," it's cadence: **treat `.cursorrules`/`AGENTS.md` weeding as a weekly task**, not an occasional one, precisely because tool versions, model capabilities, and your own conventions all move fast enough that a month of silence is enough for a rule to flip from correct to actively wrong.

## The honest summary

The rulebook specialist job was funny because it was real, and it was real because the tools genuinely needed that much hand-holding for a while. The job (or the manual effort, if you were doing it yourself) is shrinking for the same reason PR-writing got good — the underlying capability moved. What doesn't go away is having *some* place your accumulated hard-won rules live, portable across whatever the current file format happens to be, actively pruned instead of only ever appended to.
