# vibecoding-notes

Practical, non-obvious notes for people using AI coding tools day to day — cost tricks, workflow patterns, and things vendor docs don't tell you. Written from real usage, dated so you can tell when a claim might be stale.

## Notes

### Getting started

- [use-the-fleet-or-build-your-own.md](use-the-fleet-or-build-your-own.md) — use the sandraschi fleet (190+ repos) as a reference, or build your own equivalent with the patterns below; plus the fastest way to revive a neglected, half-broken repo: sic your coding agent on the install and let it find the bloopers.

### The thesis

- [ai-dev-is-universal-acid.md](ai-dev-is-universal-acid.md) — the specialist-in-a-box argument, generalized past devops: AI dissolves the learning-curve wall for any tool whose difficulty was mostly a huge memorized surface (Blender's thousand-page docs, iOS/Swift's six-month onboarding) — but not the taste/judgment wall underneath it.
- [the-real-moat-is-tooling-not-prompts.md](the-real-moat-is-tooling-not-prompts.md) — why scripts, SOPs, and organically grown standards (not prompting skill) are the actual force multiplier for solo devs and small seed-funded teams.
- [specialist-in-a-box.md](specialist-in-a-box.md) — why Docker/Kubernetes, Grafana, Traefik, Tailscale, and CI/CD used to require a dedicated devops hire, why AI collapsed that bottleneck, and the operational-judgment cost that didn't collapse with it.

### The three bugbears, now (nearly) automated

- [linting-automated-and-still-worth-watching.md](linting-automated-and-still-worth-watching.md) — linting is basically solved, except for the one cheat: an agent under pressure suppressing a lint error (`noqa`, `type: ignore`, `eslint-disable`) instead of fixing it, to get the gate green faster.
- [testing-coverage-e2e-cua-smoke.md](testing-coverage-e2e-cua-smoke.md) — coverage % is a floor, not a target (watch for assertion-free tests padding it); why you need all three layers — unit, E2E, and CUA smoke tests driving the actual installed app — because each catches failures the others structurally can't.
- [docs-that-dont-drift.md](docs-that-dont-drift.md) — docs are also basically automatable now, with their own cheat: fluent documentation that describes what code is *supposed* to do instead of what it actually does, which is the hardest of the three cheats to catch because it reads exactly like correct documentation.

### Advanced stuff (for now)

*"Advanced" has a short shelf life in this field — file this section under "things that felt like a specialist's job until recently," not "things that will stay hard." Grafana dashboards were a specialist skill two years ago too.*

- [goal-driven-scenario-testing.md](goal-driven-scenario-testing.md) — one level above E2E: state the goal ("order a widget, verify the total") instead of scripting the steps, let an agent plan and self-heal against UI drift, store scenarios as reviewed data with personas layered on top — and don't let the testing agent grade its own homework.

### Patterns we actually use

- [staying-current-without-getting-burned.md](staying-current-without-getting-burned.md) — don't scaffold new repos on a stale framework floor, prefer fast actively-developed tools (Ruff over legacy Python linting, Biome-style over legacy ESLint), actually watch CVE advisories, and give Dependabot-style bots a cooling-off window instead of letting them grab release-day versions.
- [reading-code-is-the-skill-that-survives.md](reading-code-is-the-skill-that-survives.md) — "when not to hand-code" is a shrinking, near-theoretical question now; the skill that has to survive on purpose is reading code fast and accurately. Includes the triage order: run the linter first (modern ruff/biome autofix naked excepts and friends), then spend your reading attention only on what's left.
- [meta-tool-swiss-army-pattern.md](meta-tool-swiss-army-pattern.md) — portmanteau tools collapse operation sprawl inside one tool; a meta-tool collapses sprawl across all your tools (scaffold/wrap/probe/audit/operate). Same fix, two altitudes.
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
- [sonnets-opinion.md](sonnets-opinion.md) — an actual first-person take from Claude Sonnet 5, the model that helped write most of this repo, including where it disagrees with its own thesis and why "prove it, don't trust it" applies specifically to it.

## Why this exists

Most "AI coding tips" content is either vendor marketing or outdated within a month. These notes are dated, sourced where possible, and explicitly call out what's vendor-reported vs. independently verified — because in this space, benchmark tables get cherry-picked constantly.

Contributions welcome via PR if you have a similarly concrete, dated, sourced tip.

## House convention: cite your sources, especially on advanced/fast-moving topics

Any note that leans on an external claim, a named pattern from outside our own fleet, or a fast-moving/"advanced" topic (see [goal-driven-scenario-testing.md](goal-driven-scenario-testing.md) for the template) should end with a **Sources** section: the actual links, not just a claim of authority. Notes describing our own directly-used, verified fleet patterns (bug depot, meta-tool, checkpoint commits) don't need this — the source is "we do this," stated as such. External claims do, because "advanced" topics are exactly the ones most likely to be half-remembered from a headline and wrong in a way that's expensive to inherit silently.
