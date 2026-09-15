# Hand-coding withers. Reading code is the skill that has to survive.

**Dated:** 2026-09-15

"When should you write code by hand instead of delegating to an agent" is a shrinking question, and it's shrinking fast enough that a note answering it goes stale within months of being written. That's not a controversial claim anymore — it's closer to a lived fact for anyone doing this daily. A year of not hand-writing code is a completely normal sentence to say out loud now, where two years ago it would have sounded like a confession.

That's fine. Hand-coding fluency atrophying isn't the risk. The risk is a different skill atrophying alongside it by accident, because nobody named it as something to protect on purpose: **reading code fast and accurately.**

## Why reading is the one that has to survive

Every practice in this repo that keeps agentic coding safe — [prove it, don't trust it](prove-it-dont-trust-it.md), [fix the gate you find](fix-the-gate-you-find.md), the whole premise of reviewing a diff before it ships — collapses to zero if you can't actually read what got produced fast enough to notice when it's wrong. Writing skill and reading skill used to be trained together as a side effect of the same activity; once you stop writing by hand, reading stops being a free byproduct and becomes something you have to maintain on purpose, or it quietly degrades right when you need it most.

The failure mode is specific and easy to miss in yourself: you get faster at *accepting* diffs and slower at *actually parsing* them, because acceptance doesn't require full comprehension and nothing forces the distinction to surface — until the one time it does, expensively.

## What keeping the skill sharp actually looks like

Not "occasionally hand-write something for practice" — that's treating it as a nostalgia exercise, and it doesn't transfer to the actual bottleneck, which is reading speed and accuracy under real velocity, not writing ability.

What does transfer:

- **Actually read every diff before accepting it**, at the speed you can genuinely comprehend, not the speed that feels efficient. If that speed feels uncomfortably slow compared to how fast the agent produced the change, that gap is the whole point — closing it by skimming faster doesn't close it, it just hides it.
- **Read unfamiliar codebases on purpose, regularly**, not only when forced to by a bug. Orienting quickly in code you didn't write and don't remember is a distinct skill from reading your own recent output, and it's the one that degrades fastest from disuse — it's also, not coincidentally, exactly the skill "prove it, don't trust it" requires when the code in question came from an agent instead of your past self.
- **Do code review for other people's (or other agents') output even when you're not writing much yourself.** Review is reading-skill practice with a built-in accountability loop — you have to form and state an opinion, not just pattern-match "looks fine."

## Triage order: let the linter go first

Reading skill is precious enough that you shouldn't spend it on things a tool already catches for free. Ruff, Biome, and their peers got genuinely excellent — the mechanical categories (a naked `except:` swallowing every exception, an unused import, an obviously-wrong type, inconsistent formatting) are exactly what modern linters find and, for a growing share of them, autofix in the same pass. That's not skimming past a real risk, it's not spending scarce human attention re-deriving what a deterministic tool already solved.

So the actual order:

1. **Run the linter, let it autofix what it can.** Naked excepts, unused imports, formatting drift, a dozen other mechanical smells — that's the linter's job, not a reading exercise for you.
2. **Read what's left with the attention you saved.** Once the mechanical noise is gone, what remains in the diff is disproportionately the stuff a linter *can't* catch — wrong business logic, a subtly incorrect assumption, a race condition, a fix that solves the symptom instead of the cause. That's where your reading skill actually needs to go, and it's a much smaller, much higher-signal set of lines than "the whole diff."

Getting this order backwards — reading everything with equal attention, mechanical and substantive together — is how reading skill gets spent on the wrong things and feels exhausting for less signal than it should produce. Let the deterministic tool triage first; save your judgment for what only judgment can catch.

This only holds if the linter itself is current. Ruff, Biome, and their peers ship new rules and new autofixes on a fast cadence — a check that didn't exist or wasn't autofixable a couple of quarters ago routinely does now. A pinned, stale linter version quietly hands categories of mechanical noise back to your reading budget that a current one would have caught for free. Update the linter, not just your dependencies, on the same cadence — it's the cheapest possible way to keep buying back reading attention over time.

## The honest caveat

This isn't a claim that hand-coding skill is worthless or that everyone should feel fine never doing it again — plenty of domains (safety-critical, deeply performance-sensitive, or just genuinely enjoyable as craft) still reward it, and losing it entirely has real costs for those cases. It's a narrower claim: for most day-to-day delegated coding work, hand-writing is the skill that's optional now, and reading is the one that isn't, and treating both as equally optional is how the actually load-bearing one erodes without anyone noticing until it's needed under pressure.
