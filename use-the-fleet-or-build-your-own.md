# Use the sandraschi fleet, or build your own version of it

**Dated:** 2026-09-15

Everything in this repo so far is extracted from running one specific thing: a personal fleet of 190+ small repos, each wrapping one existing tool or device (Blender, a robot, Plex, Vienna transit, whatever) in the same five-layer shape — an agent-callable tool server, a web dashboard, a desktop app, and in-app AI chat. You don't need to adopt that fleet to get value from the patterns in this repo, but if you want to see the patterns applied at scale instead of just described, that's what it's for.

**Entry point:** [github.com/sandraschi/sandraschi](https://github.com/sandraschi/sandraschi) — the profile repo doubles as the fleet's front door. Start at [WHY_FLEET.md](https://github.com/sandraschi/sandraschi/blob/main/WHY_FLEET.md) for the plain-language pitch, [MCP_CATALOG.md](https://github.com/sandraschi/sandraschi/blob/main/MCP_CATALOG.md) for the full repo-by-category index, and [DEV_STACK.md](https://github.com/sandraschi/sandraschi/blob/main/DEV_STACK.md) if you want the technical internals (stack, standards, CI, patterns library).

## If you'd rather build your own equivalent

Don't try to build the whole thing on day one — that's building the meta-layer before you have the sprawl it solves (see [meta-tool-swiss-army-pattern.md](meta-tool-swiss-army-pattern.md)). The realistic path:

1. **Wrap one tool you actually use**, end to end, to whatever shape feels right for you.
2. **Notice what you keep redoing** the second and third time you wrap another tool — that's your signal for what belongs in a shared standard, not a fresh decision each time.
3. **Write the standard down once** the third repeat happens, not the first — see [the-real-moat-is-tooling-not-prompts.md](the-real-moat-is-tooling-not-prompts.md).
4. **Only then** consider a meta-tool or named macros to operate the growing set as a fleet instead of by hand.

The shape you converge on doesn't need to look like this one. The load-bearing idea isn't "five layers" specifically, it's "one tool, one job, a written standard for what 'done' looks like, applied consistently" — see [loosely-coupled-integrations.md](loosely-coupled-integrations.md).

## The trick that makes reviving old repos actually fast: sic your agent on the install

Every dev with more than a handful of side projects has the same graveyard: repos that worked six months ago, whose README now lies slightly (a dependency bumped, a config format changed, an install script assumes a tool version you no longer have). Manually debugging someone else's — or worse, your own past self's — stale install instructions used to be a genuinely miserable hour of "why is this failing" archaeology.

**The current move: point your coding agent at the repo and just say "get this running."** Let it clone-or-open the repo, attempt the documented install, read the actual error when it fails, and iterate — bump the dependency, fix the path, patch the outdated flag — the same debugging loop you'd do by hand, except it doesn't get bored on attempt four and it reads the traceback faster than you do. For a repo that's merely neglected rather than architecturally broken, this routinely goes from "abandoned, I'll deal with it someday" to "actually running" in a few minutes instead of an afternoon.

Two things make this trustworthy instead of reckless:

- **[Prove it, don't trust it.](prove-it-dont-trust-it.md)** "I fixed the install" needs to end with the thing actually running and you looking at real output — not the agent's summary of what it believes it fixed.
- **Write down what was actually wrong.** Once the agent finds the real install blooper (a pinned version that no longer resolves, a renamed env var, a Windows-path assumption that broke on this machine), that's a [bug depot](bug-depot-pattern.md) entry, not a one-time fix — the next stale repo you revive six months from now is disproportionately likely to have the exact same rot.

This is also, not coincidentally, the single highest-leverage use of an agent for the "graveyard of old repos" problem specifically: it turns "I should really get around to reviving that" from a mental-load line item into a five-minute ask.
