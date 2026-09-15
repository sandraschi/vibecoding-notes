# Testing: coverage %, real end-to-end, and letting an agent click through your actual UI

**Dated:** 2026-09-15

Like linting, writing tests used to be the chore everyone under-invested in, and agentic coding has made the marginal cost of writing a test low enough that under-testing is now more of a discipline failure than a time-budget one. That's mostly good news. It comes with its own cheats to watch for, same as linting does.

## Coverage percentage: a floor, not a target

Coverage % tells you what got executed during tests, not what got verified. A test that calls a function and asserts nothing meaningful about the result raises coverage without producing any actual protection — and this is a specific failure mode worth naming, because it's the testing equivalent of the lint-suppression cheat: fast to produce, looks like the metric moved, doesn't reduce real risk. An agent asked to "get coverage to 90%" can hit that number with a pile of assertion-free tests just as easily as a human padding a sprint metric can.

Use coverage % as a floor that flags obviously untested code, not as a target you optimize directly. A jump in coverage from a batch of new tests is worth a quick read of what those tests actually assert, not just a glance at the percentage.

## End-to-end tests: the layer unit tests structurally can't cover

Unit tests verify a function does what it claims in isolation. They cannot tell you that the pieces actually work together, that the real network call succeeds, that the UI renders what the backend actually returns. E2E tests exercise the real path a user takes through the real system — and they're the layer most likely to get skipped under time pressure because they're slower and more annoying to write, which is exactly why skipping them is where the actual regressions hide.

If you're testing a webapp, an E2E suite driving a real browser against a real running instance (Playwright and equivalents) catches an entire category of bug that a green unit-test suite will confidently miss: broken routing, a frontend that doesn't match an API contract change, a build that compiles but doesn't actually render.

## CUA smoke tests: the layer above E2E, for anything with a real UI to click through

For a desktop app, a packaged installer, or anything where "does this actually work for a human" matters beyond what a scripted E2E flow captures, a computer-use-agent (CUA) smoke test — an agent literally driving the mouse and keyboard against the real installed app, the way a first-time user would — catches what E2E automation against a dev server can miss: install-time failures, a native window that doesn't render right, a packaging step that silently dropped an asset. Run this as a cold-install check before a release ships, not as a one-time validation you did once and now assume still holds.

This is the same underlying idea as [prove-it-dont-trust-it.md](prove-it-dont-trust-it.md) applied specifically to "does the actual shipped artifact work," not just "does the code that produces it look right."

## The stack, in order of what it catches

1. **Unit tests** — this function does what it claims, in isolation, fast to run, cheap to write, doesn't tell you the whole system works.
2. **E2E tests** — the real user flow works against a real running instance, catches integration and contract breaks unit tests can't see.
3. **CUA smoke tests** — the actual shipped, installed artifact works for a real click-through, catches packaging and install-time failures E2E against a dev server can't see.

None of these three replaces either of the others — they catch different, mostly non-overlapping categories of failure, and a project that only has the cheapest layer (unit tests, high coverage %) can look thoroughly tested while having zero actual protection against the failures that ship most embarrassingly: the thing that doesn't install, the page that doesn't render, the flow that broke between two components that each individually pass their own tests.
