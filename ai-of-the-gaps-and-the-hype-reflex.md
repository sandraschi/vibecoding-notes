# "AI of the gaps," and the easy fix for AI's other bad habit: logorrhea

**Dated:** 2026-09-15

## AI of the gaps

Named by analogy to "god of the gaps" — the old habit of pointing at whatever science hadn't explained yet and calling that specific gap permanent, right up until it wasn't. The AI version: citing a current model limitation as if it's a durable, structural fact about AI rather than a snapshot with an expiration date.

The concrete example that should embarrass anyone who said it out loud: "LLMs can't write a good PR description or issue writeup" was a reasonable-sounding claim not long ago — vague summaries, missing context, no sense of what a reviewer actually needs to know. It's a much weaker claim now; a model asked to write a PR description today routinely produces something better-structured than what a rushed human writes at 6pm on a Friday. That's not a marginal improvement, it's a capability that crossed from "notably weak" to "often better than the baseline" within about a year.

**The discipline this implies:** date every capability claim, including the ones already sitting in this repo. "Origination of best-in-class original work is still the real gap" ([ai-dev-is-universal-acid.md](ai-dev-is-universal-acid.md)) and "I don't think I have that calibration reliably yet" for infra judgment calls ([sonnets-opinion.md](sonnets-opinion.md)) are both exactly the kind of claim that ages the way the PR-writing claim did. Hold them as "true as of 2026-09-15," not as settled facts, and expect to have to revisit them — probably sooner than feels comfortable.

## The other bad habit: AI has logorrhea

Left to its own defaults, a model generating a commit message, PR description, issue writeup, or README section reaches for superlatives and volume: "revolutionary," "game-changing," "breakthrough," exclamation points doing the work that specifics should be doing. It's not malicious, it's a reflex — enthusiastic, verbose framing is a common pattern in training data for anything announcement-shaped, and it surfaces by default unless something pushes back on it.

[stars-and-traction-without-being-cringe.md](stars-and-traction-without-being-cringe.md) already covers the reactive fix: lint your own drafts for hype words before you hit send. The cheaper, earlier fix is upstream of that — put the rule directly in the instructions your agent reads before it writes anything, so the first draft doesn't need the cleanup pass at all.

**A rule that actually works, dropped straight into an AGENTS.md / CLAUDE.md-equivalent file:**

> No superlatives in generated commit messages, PR descriptions, issue text, or README copy — ban "revolutionary," "game-changing," "breakthrough," "insane," "10x," and similar. No stacked exclamation points. State what changed and why, in plain declarative sentences. If something is genuinely a big deal, say what it does and let the reader decide it's a big deal — don't tell them it is.

This is a two-sentence addition to a file most agentic setups already read before every session, and it changes the default output instead of requiring anyone to remember to grep for hype words after the fact.

## Why both belong in the same note

They're the same underlying discipline pointed in two directions: don't overclaim what AI can't do (the gaps fallacy), and don't let AI overclaim what it just did (the hype reflex). Both get fixed the same way — write the correction down once, somewhere it actually gets read before the relevant output happens, instead of trusting yourself to catch it by vigilance every time.
