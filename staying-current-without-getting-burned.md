# Staying current without getting burned

**Dated:** 2026-09-15

Two failure modes sit on opposite ends of the same axis: freezing on old tool versions until you're quietly accumulating both technical debt and unpatched CVEs, versus auto-updating to whatever shipped an hour ago and inheriting a regression the rest of the world hasn't found yet. Neither extreme is the goal. The actual skill is picking a sane point in between, on purpose, instead of defaulting to whichever extreme your tooling's settings happen to encourage.

## Don't scaffold new work on a stale floor

If you're starting something new, start it on the current version of your stack, not whatever version a tutorial or an old template happens to pin. A brand-new project built on an old major version of your core framework is stale on day one — you've inherited someone else's technical debt before writing a line of your own code. Concretely: if your framework has moved from, say, a 2.x to a 3.x line with real improvements, don't scaffold new repos against the old line just because that's the version in muscle memory or in a copy-pasted template. Check the current floor before starting, not after you've built three months of work on the wrong one.

## Prefer the fast, actively-developed tool over the legacy default

Linting is the clearest example right now: **Ruff** for Python has genuinely displaced the old Flake8-plus-plugins-plus-pylint stack for most use cases — it's dramatically faster, actively developed, and closing the feature gap month over month. The equivalent shift on the JS/TS side is away from legacy ESLint toward faster Rust-based tooling (Biome and similar) for the same reason: speed and active development compound over time, and a linter that's slow enough to feel like friction is a linter people quietly stop running. Don't keep the legacy default out of inertia once a faster, actively-maintained alternative has clearly won — see [reading-code-is-the-skill-that-survives.md](reading-code-is-the-skill-that-survives.md) for why a current, capable linter matters more than it sounds like it should.

## Actually watch CVE news for what you depend on

"The build passed" and "nothing in this dependency tree has a disclosed vulnerability this week" are different facts, and only one of them gets checked automatically by most setups. Subscribe to security advisories for your core dependencies, or at minimum run a periodic audit (`npm audit`, `pip-audit`, your ecosystem's equivalent) instead of only reacting when something breaks the build. A clean build has never once implied a clean security posture.

## Don't let automated dependency bots grab brand-new releases on day one

Dependabot-style tools defaulting to "open a PR the moment a new version exists" sounds like staying current. In practice it means you're often the first wave testing a release that hasn't had time for the community to find its regressions, its supply-chain issues, or its "this broke half of downstream users" bugs. A cooling-off window — a few days between release and when your automation is allowed to propose the bump — costs you almost nothing in freshness and buys real protection: by the time your bot proposes the update, if something's wrong, someone else has usually already found it and said so loudly.

**The balance, stated plainly:** new projects start current, tools get replaced when a clearly better one has proven itself, dependencies get watched for disclosed vulnerabilities continuously, and automated version bumps wait a few days past release day before landing in your queue. None of those four rules contradict each other — they're all the same underlying judgment call (current is good, bleeding-edge-by-default is not) applied at different points in the pipeline.
