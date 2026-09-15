# Goal-driven scenario testing: stop scripting steps, start stating goals

**Dated:** 2026-09-15

Sits one level above the E2E layer described in [testing-coverage-e2e-cua-smoke.md](testing-coverage-e2e-cua-smoke.md). Traditional E2E automation (Playwright/Selenium/Cypress) scripts exact steps: click this selector, type into that field, assert this value. It's precise and it's brittle — a selector rename or a reflowed page breaks the script even when the actual user flow still works fine.

## The pattern

Instead of scripting the steps, state the goal in natural language and let an agent plan and execute it against the real running app: *"sign in, add the cheapest item to the cart, and verify the total updates."* The agent plans the sequence itself, drives the real browser, observes what actually rendered, corrects its own path if something's moved, and reports whether the goal was actually met — not whether a specific selector was found.

This is meaningfully different from scripted E2E in one important way: it's **self-healing** against small UI drift. A scripted test breaks the moment a button's CSS class changes; a goal-driven agent looking at the rendered page for "the add to cart button" generally doesn't care that the class changed, because it's not looking for the class.

## Treat scenarios as reviewed data, not throwaway prompts

The mature version of this pattern doesn't type the goal fresh into a chat box each run — it stores each scenario as a structured, versioned record, the same way you'd version a test file: an id, the goal itself, the starting state/fixtures needed, which tools/actions the agent is allowed to use, pass/fail criteria, and a budget (time, steps, cost) so a confused agent can't wander indefinitely. Reviewed and committed like any other test, not regenerated ad hoc.

## Layer personas on top for real coverage

Running the same scenario as different synthetic personas — a first-time visitor, a price-sensitive comparison shopper, a returning customer with items already in a wishlist — surfaces cohort-specific breakage a single "happy path" run won't catch. The onboarding flow that works perfectly for a fresh account can still be broken for a returning user with stale session state, and a single generic run of the scenario will never find that.

## The honest caveat: don't let the tester grade its own homework

This is the same problem as [prove-it-dont-trust-it.md](prove-it-dont-trust-it.md), one layer up. As of this writing, the quality and reliability of the testing agent's own judgment is widely cited (by teams actually running this in production) as the current top barrier to trusting the pattern — an agent that plans its own steps and then reports whether it succeeded is grading its own homework, and its self-report can be wrong the same way any agent's "verified" claim can be wrong. Treat the goal-driven agent's pass/fail as a strong first signal that still deserves a real look at what it actually did (a recording, a transcript of its steps, a screenshot of the end state) — not as an unattended release gate on its own, at least not yet.

## Where it fits relative to what you already have

Scripted E2E and goal-driven scenario testing aren't competing — they catch different things. Scripted E2E is precise and cheap to run continuously; goal-driven scenarios are more expensive but survive UI drift and can express "does this actual user journey work" in a way a brittle click-script can't. A reasonable split: keep scripted E2E for your tightest, most frequently-run checks, and use goal-driven scenarios for the higher-level journeys (onboarding, checkout, the flows product actually cares about) where resilience to UI churn matters more than millisecond-level precision.

## Sources

This is a fast-moving, still-forming area — treat the specifics as dated 2026-09-15, not settled fact.

- [Scenario-Based Testing: Maxim's Test Suite for Reliable, Production-Ready AI Agents](https://www.getmaxim.ai/articles/scenario-based-testing-reliable-ai-agents/) — the structured test-case-as-data fields (id, goal, initial_state, allowed_tools, fixtures, criteria, budgets, tags) referenced above.
- [AI Agent Testing Automation: Developer Workflows for 2026 — SitePoint](https://www.sitepoint.com/ai-agent-testing-automation-developer-workflows-for-2026/) — the "sign in, add cheapest item, verify total" style goal example, and the 57%-in-production / 32%-cite-quality-as-top-barrier figures.
- [9 Agentic Design Patterns for Software Testing in 2026 — TestMu AI](https://www.testmuai.com/blog/agentic-design-patterns/)
- [Agentic QA Architecture: Reasoning Loops, Self-Healing DOM & Autonomous Testing — TestQuality](https://testquality.com/agentic-qa-architecture-autonomous-testing-2026/) — the self-healing-against-UI-drift framing.
- [Data-Driven Persona-Conditioned Agents for A/B Test Simulation — arXiv](https://arxiv.org/html/2609.01038v1) — the persona-layering approach.
- [What Is a Synthetic Persona? — FutureAGI](https://futureagi.com/glossary/synthetic-persona/) — synthetic persona definition and use for coverage gaps.
