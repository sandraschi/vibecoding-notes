# vibecoding-notes

Practical, non-obvious notes for people using AI coding tools day to day — cost tricks, workflow patterns, and things vendor docs don't tell you. Written from real usage, dated so you can tell when a claim might be stale.

## Notes

### The thesis

- [the-real-moat-is-tooling-not-prompts.md](the-real-moat-is-tooling-not-prompts.md) — why scripts, SOPs, and organically grown standards (not prompting skill) are the actual force multiplier for solo devs and small seed-funded teams.

### Patterns we actually use

- [named-macros-as-ops-for-agents.md](named-macros-as-ops-for-agents.md) — turn recurring chores into a named macro that expands into a written procedure, so the bar stays the same every time instead of drifting per session.
- [bug-depot-pattern.md](bug-depot-pattern.md) — one symptom-first file that remembers every bug that cost you more than a few minutes, so you (or an agent) stop rediscovering it.
- [prove-it-dont-trust-it.md](prove-it-dont-trust-it.md) — why "tests pass, verified" from an agent is a claim, not evidence, and how to make proof a committed artifact instead of a sentence.
- [loosely-coupled-integrations.md](loosely-coupled-integrations.md) — snap small single-purpose tools together with a thin optional link instead of merging them into a monolith.
- [checkpoint-commits-and-bak-files.md](checkpoint-commits-and-bak-files.md) — cheap insurance (checkpoint commits, timestamped backups) before letting an agent touch many files at once.
- [fix-the-gate-you-find.md](fix-the-gate-you-find.md) — a pre-existing broken build/lint/test gate becomes your problem the moment you need it green to verify your own change.
- [llm-output-hygiene.md](llm-output-hygiene.md) — an LLM has no clock or map, never let it guess a date or location; normalize generated prose to plain ASCII at the boundary, not by hoping the prompt holds.

### Cost and tooling

- [ai-subscription-rotation.md](ai-subscription-rotation.md) — round-robin cheap-tier AI subscriptions instead of paying for one premium plan, plus how to fold a cheap/open model like DeepSeek into the rotation without getting burned by peak pricing.

### Getting found (without being cringe about it)

- [run-your-own-discord-guild.md](run-your-own-discord-guild.md) — wrap your Discord bot in an MCP server so your coding agent can triage support questions and draft moderation, instead of you doing it by hand at 2am.
- [stars-and-traction-without-being-cringe.md](stars-and-traction-without-being-cringe.md) — what actually gets a solo repo noticed, why hype-word linting your own release notes works, and what doesn't work.
- [demo-videos-that-dont-lie.md](demo-videos-that-dont-lie.md) — the bar a demo video needs to clear to be trustworthy, and a tooled pattern for narrating against real output instead of a rehearsed script.

### Reference

- [bibliography.md](bibliography.md) — curated, commented link list: which AI-coding YouTubers to actually trust, which benchmark sites are independent vs. vendor-fed, and the one rule that separates the two.

## Why this exists

Most "AI coding tips" content is either vendor marketing or outdated within a month. These notes are dated, sourced where possible, and explicitly call out what's vendor-reported vs. independently verified — because in this space, benchmark tables get cherry-picked constantly.

Contributions welcome via PR if you have a similarly concrete, dated, sourced tip.
