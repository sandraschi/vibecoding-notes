# Documentation: also basically automatable, also has a lazy-LLM cheat mode

**Dated:** 2026-09-15

Docs are the third classic dev bugbear (with linting and testing) that agentic coding has mostly solved for the boring part: generating a README, writing docstrings, producing a changelog entry, keeping an API reference in sync with the actual function signatures. All of that is now cheap enough that "we didn't have time to document it" is a much weaker excuse than it used to be.

## The cheat mode: documentation that describes intent, not behavior

The lint-suppression cheat and the assertion-free-test cheat both have a documentation equivalent: prose that describes what the code is *supposed* to do, generated fluently and confidently, without being checked against what the code *actually* does. This is arguably the hardest of the three cheats to catch, because a suppression comment and a trivial test are both visible in a diff — a docstring that's subtly wrong reads exactly like a docstring that's right, right up until someone relies on it.

The failure is specific: an agent writing docs from the function name, the surrounding context, and a general sense of what code like this usually does, instead of from what this code actually does in the cases that matter (error paths, edge cases, the parameter that isn't quite what its name implies). The result is fluent, plausible, and wrong in exactly the places where being wrong costs the most — because the reader trusts the docs precisely when they haven't read the implementation.

## What keeps docs honest

- **Generate reference docs from the code, not alongside it.** Docstrings compiled into an API reference structurally can't drift from the signature the way a hand-maintained separate doc page can — the source of truth and the doc are the same artifact. Prefer this wherever the tooling supports it.
- **Treat a docstring/README claim about behavior the same as a test assertion: it needs to be checked against the actual code, not accepted because it reads fluently.** This is the direct documentation analogue of [prove-it-dont-trust-it.md](prove-it-dont-trust-it.md) — "this function raises ValueError on empty input" is a checkable claim, not decoration, and should get checked before it's trusted.
- **Watch for content-free documentation as its own antipattern**, distinct from wrong documentation. A tool description, error message, or README section that's technically present but says nothing a reader couldn't already guess ("this function processes the input and returns the result") passes a "does it have docs" checklist while providing zero actual value — worth naming explicitly so it doesn't get treated as done just because a docs field is non-empty.
- **Re-verify docs when the code they describe changes, as part of the same change**, not as a follow-up ticket that quietly never happens. Doc drift compounds the same way a stale linter or a skipped test suite does — the gap between what's written and what's true grows invisibly until someone trusts the wrong sentence at the wrong moment.

## The honest summary

Linting has the noqa cheat, testing has the assertion-free-coverage cheat, documentation has the fluent-but-unverified cheat. All three share the same shape: a fast, plausible-looking way to satisfy the metric without doing the actual underlying work, and all three are more likely to appear under time or token pressure — which describes most agentic coding sessions by default. The fix for all three is the same instinct: check the claim against the actual code before trusting that the metric moving means the real thing happened.
